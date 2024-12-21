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
curl -L -o reads.tar.gz https://ndownloader.figshare.com/files/14418248
tar xvf reads.tar.gz
mv sub/SRR2584866* .
rm -rf sub reads.tar.gz # we can delete other files

# After using the above commands, you should have the following files:
# Reference genome: ecoli_rel606_reference.fasta.gz
# Sequencing reads: SRR2584866_1.trim.sub.fastq and SRR2584866_2.trim.sub.fastq
```

## Map reads on a reference genome
```
# Assuming you are inside the tutorial-bwa folder
# Build Burrows Wheeler index of the reference genome
./bwa/bwa index ecoli_rel606_reference.fasta.gz

# Align reads
./bwa/bwa mem ecoli_rel606_reference.fasta.gz SRR2584866_1.trim.sub.fastq SRR2584866_2.trim.sub.fastq > alignments.sam
```

## Inspection of SAM file
The SAM file contains information about each read's alignment to the reference genome. Let us open and check `alignments.sam`. Here is a [summary image](https://www.samformat.info/images/sam_format_annotated_example.5108a0cd.jpg) that conveys what all the columns in this file mean. 

## Visualization using a Genome Browser
Using [IGV](https://igv.org), we can also visualize the alignment file. This allows us to visually inspect read alignments. We will need to reformat the `alignments.sam` to binary format and sort the read alignments based on their alignment positions before we can upload the file to IGV.

We will need one more tool called [Samtools](https://anaconda.org/bioconda/samtools) for this. One can install Samtools from [source](https://github.com/samtools/samtools#building-samtools) or by using package managers such as [conda](https://anaconda.org/bioconda/samtools).

```
# In the following commands, give the complete path to samtools where you installed it
samtools view -hSbo alignments.bam alignments.sam
samtools sort alignments.bam > alignments.sorted.bam
samtools index alignments.sorted.bam
```

Now, we have all the files that we need for alignment visualization using IGV. First uncompress the reference genome `ecoli_rel606_reference.fasta.gz` and upload it using `Genome` -> `Local File` upload option. Next, upload `alignments.sorted.bam` using `Tracks` -> `Local File`. 

Finally, in the search textbox, type any coordinate range that you wish to visually inspect. Zoom in to any region, say `CP000819.1:1736399-1737202`, which implies that you wish to inspect alignments in the interval `1736399-1737202` on the reference genome. What all do you see?
