# Barcode Generator

Generate barcode sequences for multiplexed sequencing given some constraints.

## Requirements

- Python 2.7

## Usage

```
usage: generate-barcodes [-h] --length LENGTH --min-dist MIN_DIST --count
                         COUNT [--max-stretch MAX_STRETCH] [--input INPUT]

optional arguments:
  -h, --help            show this help message and exit
  --length LENGTH, -l LENGTH
                        length of barcode
  --min-dist MIN_DIST, -d MIN_DIST
                        minimum edit distance
  --count COUNT, -c COUNT
                        number of barcodes
  --max-stretch MAX_STRETCH, -s MAX_STRETCH
                        max stretch of the same nucleotide
  --input INPUT, -i INPUT
                        (optional) list of already-designed barcodes to extend
```

## Methodology

This script takes a brute force approach to generating the barcode sequences.
Random nucleotide sequences are generated and only those satisfying the
constraints are kept until the number of "good" barcodes reaches that specified
by `--count`. Because of this approach, it is possible that the script will
stall. There is an "ascii spinner" animation that turns whenever a new barcode
is found. If this doesn't happen for a while then the script has probably
stalled.

- `--length` - length of the barcode in nucleotides.

- `--count` - number of barcodes to attempt to generate.

- `--min-dist` - the minimum edit distance (Hamming distance) between any two
  barcodes. This is used to create "error correcting" barcodes that are
  resistant to sequencing errors. Increasing this parameter makes it possible
  to generate more resilient barcodes but decreases the number of possible
  barcodes.

- `--input` - an (optional) list of barcodes to extend. Constraints are not
  checked for input barcodes.

- `--max-stretch` - maximum number of the same nucleotide in a barcode. Useful
  if the sequencing technology is sensitive to runs of the same nucleotide.


## Examples

```bash
# Generate 5 barcodes of length 10 bp, with a minimum of 5 
# distance (Hamming) from any other barcode and a maximum stretch
# of 1 of the same nucleotide in a row.

bin/generate-barcodes \
  --length 10 \
  --min-dist 5 \
  --max-stretch 1 \
  --count 5

# Generate 100 barcodes of length 10, with a minimum of 10
# distance (Hamming) from any other barcode and a maximum
# stretch of 1 of the same nucleotide in a row.

# THIS WILL STALL!
# There is no combination of barcodes that # can satisfy
# these requirements. Generally, the script will stall for
# a few seconds in this situation. In this case, lessen the
# constraints or increase the length of the barcode

bin/generate-barcodes \
  --length 10 \
  --min-dist 20 \
  --max-stretch 1 \
  --count 100

# Same as above but generate barcodes of length 20
# instead of 10

bin/generate-barcodes \
  --length 20 \
  --min-dist 20 \
  --max-stretch 1 \
  --count 100

# (This will succeed but the barcodes are really long!)
```
