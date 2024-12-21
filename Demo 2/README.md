# Application of Burrows Wheeler Index: Genome resequencing

## Background
- [How do sequencing instruments read DNA](https://nanoporetech.com/platform/technology)
- [Mutations in a human genome](https://www.genome.gov/about-genomics/educational-resources/fact-sheets/human-genomic-variation)
- [Genome resequencing](https://training.galaxyproject.org/training-material/topics/sequence-analysis/images/mapping/mapping.png)

## Install and Prepare BWA
Let us install an alignment tool [BWA](https://github.com/lh3/bwa) using the commands below. `BWA` stands for Burrows-Wheeler Aligner. It aligns the given set of reads (from the target genome) to the given reference genome.
```
mkdir tutorial-bwa
cd tutorial-bwa
git clone https://github.com/lh3/bwa.git
cd bwa
make
```

## Download reference genome and a set of reads
Now that we have installed BWA, we need to download a reference genome and a set of reads generated using a DNA sequencer. For this tutorial, we will be downloading publicly available data from Escherichia coli (E. coli) bacterial species. This data includes both the reference genome of Escherichia coli (E. coli) and a set of reads.

```
# Come back to the tutorial-bwa folder and use the following commands
curl -L -o ecoli_rel606_reference.fasta.gz ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/017/985/GCA_000017985.1_ASM1798v1/GCA_000017985.1_ASM1798v1_genomic.fna.gz
curl -L -o sub.tar.gz https://ndownloader.figshare.com/files/14418248
tar xvf sub.tar.gz
mv sub/ data/trimmed_fastq_small
rm sub.tar.gz
```

## Map reads on a reference genome

## Inspection of BAM file

## Visualization using a Genome Browser
