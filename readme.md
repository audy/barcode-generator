# Barcode Generator

Generate barcode sequences for multiplexed sequencing given some constraints.

(c) 2014 Austin G. Davis-Richardson
LICENSE = MIT v. 3

## Usage

'''
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
'''
