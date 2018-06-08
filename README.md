# Microbiota-amplicon-bioinformatics

Bioinformatics pipelines for microbial amplicon sequence data (demultiplexed, paired-end reads), sequenced on the Illumina MiSeq platform.

***

## README.md table of contents

1.1 Bacteria_16S  
1.2 Fungi_ITS

***

## 1.1 Bacteria_16S

*in progress*

***

## 1.2 Fungi_ITS  
Fungi amplicon processing pipeline (MiSeq paired-end demultiplexed reads)

### Before you start

#### i. /raw_data  
Make a new directory /raw_data in your working/data directory.  
Add all your raw sequence data to this directory.  

#### ii. primerR.fa  
In your working directory, make primerR.fa file listing the sequence of the reverse primer used in fasta format (excluding any adapter sequence).  

e.g. for ITS2 marker:  
> \>ITS4  
> TCCTCCGCTTATTGATATGC  

### General notes for the pipeline document
The Fungi_ITS document contains two versions of the full pipeline:  

i. Full pipeline including step-by-step commentary.  

ii. Compiled command lines (without full comments for each step) are provided/reprinted at the end of the document. These include limited comments to indicate when manual intervention is required. Once you are familiar with each of the individual steps, the compiled command lines can be run in the indicated blocks. (n.b. For re-runs of data where the options (such as trimming lengths and subsampling values) have already been established, these can be entered in advance and all lines up to the blastn search step run as one block, and all subsequent steps run as a second block of commands).  

### Pipeline history  
Developed September 2017 (M Hoggard)  
Github master branch established June 2018

### Fungi-specific processing  
This pipeline does not merge forward and reverse reads. Due to varying lengths of ITS regions, some ITS sequences may be too long for the overlap and these sequences will be lost if reads are merged (i.e. you might filter out some taxa which have long ITS regions).   

When using only forward reads (with the potential for some amplicons to be shorter than the read length), it is necessary to trim any retained reverse primer-binding regions. Sequences for fungi with shorter ITS regions than the read length will include the primer region + sequence for the adapter + random junk sequence. This needs to be timmed. This timming of the reverse primer region is handled by some of the awk and -search_oligodb commands included below.

### Linux/Windows conflicts  
Pipeline developed in a windows environment (but has also been tested in a Linux (Ubuntu) environment).  

Some commands (such as the custom awk commands) *may* not work properly on some platforms due to differences in how different versions of awk runs - monitor that the outputs are as expected.

### usearch manual  
http://www.drive5.com/usearch/

### References  
If you use this pipeline you should cite all of these Edgar references (the first one is for the program (usearch), and the rest are for specific processing steps), the taxonomy reference database you used, and preferably this pipeline as well/one of the author's papers that uses this pipeline.  

> USEARCH  
> Edgar,RC (2010) Search and clustering orders of magnitude faster than BLAST, Bioinformatics 26(19), 2460-2461. doi: 10.1093/bioinformatics/btq461.  

> Expected error filtering and paired read merging  
> Edgar, R.C. and Flyvbjerg, H (2014) Error filtering, pair assembly and error correction for next-generation sequencing reads. doi: 10.1093/bioinformatics/btv401.  

> UNOISE algorithm  
> Edgar, R.C. (2016), UNOISE2: Improved error-correction for Illumina 16S and ITS amplicon reads. doi: 10.1101/081257.

> SINTAX algorithm  
> Edgar, R.C. (2016), SINTAX, a simple non-Bayesian taxonomy classifier for 16S and ITS sequences. doi: 10.1101/074161.

> UNCROSS paper (This algorithm isn't used here, but this paper discusses the concept of cross-talk)  
> Edgar RC. UNCROSS: Filtering of high-frequency cross-talk in 16S amplicon reads. bioRxiv. 2016;:doi: 10.1101/088666.

> RDP ITS database reference (usearch version downloaded from drive5.com)  
> Cole JR, Wang Q, Fish JA, Chai B, McGarrell DM, Sun Y, et al. Ribosomal Database Project: Data and tools for high throughput rRNA analysis. Nucleic Acids Res. 2014;42:D633–42.

> UNITE ITS database reference (usearch version downloaded from drive5.com)  
> UNITE Community. UNITE USEARCH/UTAX release. 2017.

> This bioinformatics pipeline (initial reference using this pipeline)  
> Hoggard M, Vesty A, Wong G, Montgomery JM, Fourie C, Douglas RG, Biswas K, Taylor MW. Characterising the human mycobiota: a comparison of small subunit rRNA, ITS1, ITS2, and large subunit rRNA genomic targets (*Under review*).

***
