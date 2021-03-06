
# VirusFriends: discover viral sequences in the NCBI SRA!
![Phage Friends!](images/friends.png)

### Please cite our work! 
DOI:DOI 10.17605/OSF.IO/Z4BCN 
Virus Discovery Project: https://osf.io/4cn3j/

## It's always sunny when you have phage friends, too

![virus friends](images/phagefriends2.png)

## VirusFriends 
Is an implementation to discover viruses that are slightly related to already known ones. The idea is to use the genomes of known viruses as anchors to expand the viral sequence space. 

## Why VirusFriends?
It's being estimated that there are 3x10^31 viral particles in the world, but only ~9,500 viral genomes have being described at a genomic level. This means there is a huge amount of viruses to be discovered! 

VirusFriends is a bioinformatics tool that discovers viruses in Whole Shotgun Sequence metagenomic samples in the Sequence Read Archive.  In addition to identification and quantification of known viruses in metagenomes, VirusFriends also allows for identification of novel viruses in metagenomic samples. VirusFriends uses Magic-BLAST to screen metagenomes from the SRA for presence of reads that map to the NCBI Viral RefSeq database or a custom user-specified reference database. For a given reference, statistics are output that include read coverage, and numbers of reads mapped at various levels of sequence identity. Novel viruses are identified by de-novo assembly and iteratively searching for reads that map to the 5’ and 3’ ends of a given contig to extend the contig’s length.

## What is VirusFriends?

This is an implementation that is inpired on work developed on previous NCBI-hackatons as part of the Virus Discovery Project, the natural histor of this work is: SIDEARM --> Virome Sniff --> ViruSpy --> EndoVir --> VirusFriends

VirusFriends is the latest stage of the [Virus Discovery Project] (https://osf.io/4cn3j/) developed at several NCBI-sponsored hackathons 

### Pipeline 

![VirusFriends Pipeline](images/Workflow.png)
Step 1. Screen a set of SRA datasets for viral reference genomes and keep the "very good" hits and "weak hits"

Input: [a list of SRA ids] [a fasta file with the viral database]
Output: sam files, fasta files for weak viral hits, stats about number of hits, identity, etc ... for strong and weak hits

Step 2: Weak hits go into denovo assembly, viral motifs search and extension of the contigs
Input: [fasta file of weak hits]
Output: enriched contigs, weakly related to known viruses

### How does this relate to previous work?

Our hackathon project is build on the shoulders of many other good projects. The closest relative to this project is [EndoVir](https://github.com/NCBI-Hackathons/EndoVir/tree/master) and our relationship to this project can be seen in the figure below. This project also has deeper roots in [ViruSpy](https://github.com/NCBI-Hackathons/ViruSpy/tree/master), [Virus Domains](
https://github.com/NCBI-Hackathons/Virus_Domains/tree/master), and [Virus_Detection_SRA](https://github.com/NCBI-Hackathons/Virus_Detection_SRA/tree/master). An overview of this history can be seen [here](https://osf.io/4cn3j/) and our relationship to EndoVir can be seen below.

![endovir and virusfriends](images/EndoVir_VirusFriends.png)


## Test Datasets

### HIV-spiked metagenome

### Ebola metagenome 

## Use Cases

### crAssphage

### Picobirnavirus

### VirusFriends with any nucleotides database
  
## Quick Start Guide ##
To get started, a working directory needs to be created and the appropriate databases need to be put in place. Currently, these steps are best handled by running the setup.sh script in the root directory of VirusFriends. The setup.sh script installs a list of tools required to run VirusFriends. 
`bash setup.sh -I`
To list the list of tools that will be installed run 
`bash setup -L`

To run VirusFriends
`python3 src/virusfriends.py --inputs SRR5150787 -intype srr`

This will create a directory called SRR5150787 in the VirusFriends/analysis directory which will contain the initial results from magicblast in the form of a sam file. SPAdes will assemble any weakly matching reads into contigs.fasta in the asm folder. From there, the rpstblastn and bud pipelines will start.

### Dependencies ###

VirusFriends require a set of tools, most of these tools are installed using the setup.sh script if they are already not in your path. There are three dependencies that are not installed by setup.sh script currently, but required to run VirusFriends 
  * **git version 2.7.4** 
  * **Python 3.5**
  * **Pysam 0.13**
  * **Samtools 1.7**
  * **Biopython**
  
### Installing <this software> from Github

1. `git clone https://github.com/NCBI-Hackathons/VirusFriends.git`
  
The follwing tools are downloaded and installed by setup.sh file if not already installed and in your path
* **Megahit v1.1.2**
* **Blast 2.7**
* **SPAdes v3.11.1**
* **Sra-toolkit v.2.8.2**
* **MagicBlast v1.3.0**

## Authors

* **Taylor G. O’Connell** (https://github.com/taylor-oconnell)
* **Kyle Levi** (https://github.com/KyleLevi)
* **Carrie Ganote** (https://github.com/cganote)
* **Bhavya Papudeshi** 
* **Sean Benler** (https://github.com/sean-bam)
* **Ana Cobian** (https://github.com/yinacobian)
* **Rob Edwards** (https://github.com/linsalrob)
* **Ben Busby** (https://github.com/DCGenomics)
* **Jan Piotr Buchmann** 
