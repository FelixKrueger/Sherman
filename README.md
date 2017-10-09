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

## Credits

Sherman was written by Felix Krueger, as part of the [Babraham Bioinformatics](https://www.bioinformatics.babraham.ac.uk/projects/sherman/) group.
