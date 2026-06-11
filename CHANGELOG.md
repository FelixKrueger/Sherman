## Unreleased

### Added

- New option `--amplicon_bedfile <file>` (paired-end only): instead of sampling random fragments, simulate reads for the fixed amplicon loci listed in a 4-column, tab-delimited, 0-based half-open BED (chromosome, start, end, strand). Read 1 starts at each amplicon start and read 2 ends at each amplicon end, sampled equally across all amplicons. Truth-set coordinates are correct for both strands, and the bedfile is validated (4 columns, valid strand, `start < end`, amplicon ≥ read length, within-contig). Resolves [#13](https://github.com/FelixKrueger/Sherman/issues/13).
- New option `--bwa_ending`: for paired-end reads, name read IDs `xxx/1` and `xxx/2` (BWA-style) instead of the default `xxx_R1` / `xxx_R2`, for compatibility with BWA-based aligners. Addresses [#5](https://github.com/FelixKrueger/Sherman/issues/5).

### Fixed

- **`--truth_set` coordinates are now correct for all read orientations** ([#15](https://github.com/FelixKrueger/Sherman/issues/15)). Previously the logged positions could be off by one (forward reads) or grossly mismapped onto the wrong fragment end / strand (reverse-complemented reads), so a large fraction of `positional_changes.txt` positions landed on reference A/T bases. Positions are now derived per read from a genomic anchor plus a travel direction, and are correct for single-end and paired-end, both strands, both mates, directional and `--non_directional`, uniform and context-specific conversion. The simulated reads themselves are unchanged.
- **Context-specific conversion (`-CG`/`-CH`) no longer crashes without `--truth_set`** — the `POS_CHANGE` writes are now properly guarded.
- **Paired-end fragments no longer straddle contig boundaries** on multi-contig genomes, which previously produced reads from the wrong contig and a `--truth_set` crash (`Argument "" isn't numeric`). Such fragments are now rejected and resampled.

## 11-07-2022: Sherman Version v0.1.9 released

- Added option `--truth_set` to write out a file 'positional_changes.txt' containing chromosome, position and C-context (tab-delimited). More [here](https://github.com/FelixKrueger/Sherman/pull/9). 
 
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
