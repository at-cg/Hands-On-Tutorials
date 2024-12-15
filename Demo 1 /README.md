# Compressed index of 400k SARS-CoV-2 genomes

This demo has been adapted from [Heng Li's blog](https://lh3.github.io/2021/05/17/an-fm-index-of-400k-sars-cov-2-genomes)

## You will need
- Internet connectivity
- Laptop with Linux OS
- Knowledge of basic linux commands
- `gcc` for compiling C code

## Downloading dataset
Create a separate folder (e.g., WinterSchool-Demo-1) for this demo. Go inside this folder. Download 400K SARS-CoV-2 genomes from [Zenodo](https://zenodo.org/records/4771285) using the commands below:

```
mkdir WinterSchool-Demo-1
cd WinterSchool-Demo-1
wget -O sars-cov-2_genomes.fa.xz https://zenodo.org/records/4771285/files/sars-cov-2_2021-05-15.fa.xz?download=1

# uncompress the file; this can take a few minutes; install xz-utils is you don't have unxz 
unxz sars-cov-2_genomes.fa.xz

# check size of uncompressed file
du -sh sars-cov-2_genomes.fa
```

## Downloading & installing software
Download and install [ropebwt3](https://github.com/lh3/ropebwt3)
```
git clone https://github.com/lh3/ropebwt3
cd ropebwt3
make
./ropebwt3  #do you see the help page?
```

## Downloading index

Next, we will come back to the directory where we had downloaded the dataset. Building a compressed index for 400K genomes may take significant time on a laptop (you are welcome to try at home). For now we will directly download the index from [Zenodo](https://zenodo.org/records/4771285).
```
cd ..
# Download index
wget -O sars-cov-2_genomes_index.fmd https://zenodo.org/records/4771285/files/sars-cov-2.fmd?download=1

# How big is the index file?
```

## Using Index
### Get statistics of BWT
```
./ropebwt3/ropebwt3 stat sars-cov-2_genomes_index.fmd

# What do you see?
# What is the total sum length of all genome sequences?
# How many runs are there in the Burrows Wheeler Transform? How does it compare to the total sum length?
```

### Check if the index is lossless
Can we recover genome sequences back from the index?
```
./ropebwt3/ropebwt3 get sars-cov-2_genomes_index.fmd 1
./ropebwt3/ropebwt3 get sars-cov-2_genomes_index.fmd 2
./ropebwt3/ropebwt3 get sars-cov-2_genomes_index.fmd 3
...
```

### Pattern matching using index

