# Sherman
## A simple Bisulfite FastQ Read Simulator (BiQRS)


Sherman can simulate ungapped high-throughput datasets for bisulfite sequencing (BS-Seq) or standard experiments. It allows the user to introduce various 'contaminants' into the sequences, such as basecall errors, SNPs, adapter fragments etc., in order to evaluate the influence of common problems observed in many Next-Gen Sequencing experiments. For more specific information please refor to the [Sherman User Manual](Sherman_User_Manual.md).

- Generate any number of sequences
- Generate either completely random sequences or use genomic sequences (genome can be specified)
- Generates single-end or paired-end data
- Adjustable bisulfite conversion rate from 0-100% for either all cytosines or cytosines in CH and CG context individually
- Generate directional or non-directional libraries
- Generate sequences in base-space or SOLiD color-space format
- Adjustable default Phred quality score (Sanger encoding, Phred+33 format)
- Sequences can have constant Phred qualities throughout the read or can have quality scores following an exponential decay curve, which will eventually result in basecall errors (note that this is handled slightly different for base- and color-space data)
- Introduce a variable number of random SNPs into each read
- Introduce a fixed amount of adapter sequence at the 3' end of all sequences
- Introduce a variable amount of adapter sequence at various positions at the 3' end of reads
- Write out a truth set of introduced bisulfite conversions ('positional_changes.txt'), with genomic coordinates that are correct for both strands and both mates
- Simulate **amplicon** libraries from fixed loci supplied as a BED file (`--amplicon_bedfile`)
- Optionally use BWA-style `/1` and `/2` paired-end read-name suffixes (`--bwa_ending`)

## Quick start

```bash
# Random single-end reads, 90% bisulfite conversion
./Sherman --length 50 --number_of_seqs 100000 --conversion_rate 90

# Genomic paired-end reads from a genome folder, with a truth set of converted positions
./Sherman --genome_folder /path/to/genome --length 100 --number_of_seqs 1000000 \
          --paired_end --conversion_rate 99 --truth_set

# Context-specific conversion (different rates for CpG and non-CpG cytosines)
./Sherman --genome_folder /path/to/genome -l 100 -n 1000000 --paired_end -CG 80 -CH 2

# Amplicon mode: simulate reads for fixed loci listed in a 4-column BED (chr, start, end, strand)
./Sherman --genome_folder /path/to/genome -l 100 -n 100000 --paired_end \
          --amplicon_bedfile amplicons.bed --conversion_rate 95 --truth_set
```

The genome folder should contain one or more FastA files (`.fa`/`.fasta`). Output is written as
`simulated.fastq` (single-end) or `simulated_1.fastq` / `simulated_2.fastq` (paired-end).

## Notable options

| Option | Description |
| --- | --- |
| `-l/--length <int>` | Read length |
| `-n/--number_of_seqs <int>` | Number of reads (or read pairs) to generate |
| `--genome_folder <path>` | Extract reads from a real genome instead of random sequence |
| `--paired_end` | Generate paired-end data (`simulated_1/2.fastq`) |
| `-cr/--conversion_rate <0-100>` | Uniform bisulfite conversion rate for all cytosines |
| `-CG / -CH <0-100>` | Context-specific conversion rates (CpG vs non-CpG); used together |
| `--non_directional` | Reads can originate from any of the four bisulfite strands |
| `--truth_set` | Write `positional_changes.txt` (chromosome, position, context) of every converted cytosine |
| `--amplicon_bedfile <file>` | Amplicon mode (paired-end): simulate reads for fixed loci from a 4-column, 0-based half-open BED |
| `--bwa_ending` | Use `xxx/1` and `xxx/2` paired-end read names (instead of `xxx_R1` / `xxx_R2`) for BWA-based aligners |

Run `./Sherman --help` for the full list of options. For more detailed information please refer to the
[Sherman User Manual](Sherman_User_Manual.md).

## Sherman_Nanopore

This version of Sherman doesn't do anyting particularly clever but it allows a maximum sequence length of 300,000 bp and therefore also a lot of SNPs (e.g 15% error rate and read lengths of 10000 bp). It also does't mind if the reference sequence contains `Ns` (which Sherman normally rejects). This version does not have the option --truth_set.

## Credits

Sherman was written by Felix Krueger, as part of the [Babraham Bioinformatics](https://www.bioinformatics.babraham.ac.uk/projects/sherman/) group, now maintained at Altos Labs, Cambridge Institute.
