## 16-10-2018: Sherman Version v0.1.8 released

- Fixed the coordinates of extracted paired-end sequences
- Fixed the chromosomal extraction of sequence for paired-end files


## 11-08-2014: Version 0.1.7 released

- Fixed a 1-off length issue that might have occurred for some sequences with variable length adapter contamination

## 09-09-2013: Version 0.1.6 released

- Fixed several bugs with the length of the quality string that were inadvertently introduced in previous versions. Sequence and quality strings should now have the same length again, and the genomic coordinates of single-end reads are being shown correctly

## 24-07-2013: Version 0.1.5 released

- Sequences are no longer 1bp longer than specified in `--CR 0` mode

- Quality scores are no longer 1bp longer than the sequences

## 12-07-2013: Version 0.1.4 released

- During context specific cytosine conversion, for simplicity Sherman assumed that a C at the last position was in CH context. This did however cause a weird blip in the M-bias plots of simulated data at the end or read 1 and at the start of read 2. To account for this, Sherman does now determine the sequence context of the last position in a read correctly

## 18-12-2012: Version 0.1.3 released

 - Changed the third line of basespace FastQ reads to be a `+` only. This saves disk space and prevents crashing other programs such as Cutadapt

## 05-09-2012: Version 0.1.2 released

- Reads simulated from existing genomes will have their genomic coordinates printed into the read ID line in addition to the read count to keep IDs unique

## 09-01-2012: Version 0.1.1 released

- The bisulfite conversion rate can now be any float number between 0 and 100% (instead of integers only)

- Improved handling of input genomes containing DNA ambiguity characters or `\r` line endings

- Fixed a bug while generating non-directional paired-end libraries. This feature is now working as intended.

## 15-07-2011: Version 0.1 released
- Initial release
- All basic functions working
