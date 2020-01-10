# Analyzing RNA-Seq data using Python 3 Snakemake
### Alex Soupir
[Snakemake](https://snakemake.readthedocs.io/en/stable/) is a Bioinformatics tool for managing a workflow. This tool proves valuable when analyzing a large amount of data with multiple tools. This script was made as a learning tool for workflow manager. There is also [Nextflow](https://www.nextflow.io/) to manage large analysis workflows. Here, Snakemake was used to run everything that is usually run on Linux with [RNA-Seq Analyses](https://github.com/ACSoupir/Bioinformatics_RNASeq/blob/master/Mouse_RNA_Seq_p53_genotoxic.md) (here is my long winded version of an RNA-seq analysis on Mice p53 gene mutation). 

The [Snakemake file](Snakefile) was developed for analyzing sequencing data from a recent publication - **[Dietary walnut altered gene expressions related to tumor growth, survival, and metastasis in breast cancer patients: a pilot clinical trial](https://www.sciencedirect.com/science/article/pii/S0271531718311904)**. The raw sequences were downloaded from the [Sequence Read Archive Run Selector](https://www.ncbi.nlm.nih.gov/Traces/study/?acc=SRP133401&o=acc_s%3Aa) using sra-tools.

* The [genome](ftp://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_32/GRCh38.primary_assembly.genome.fa.gz) and the [gtf](ftp://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_32/gencode.v32.annotation.gtf.gz) files were downloaded and an index was created of the genome.
* The [minikraken ](https://ccb.jhu.edu/software/kraken/dl/minikraken_20171019_8GB.tgz) was downloaded and extracted.
* *Homo sapiens* rRNA sequences were downloaded from NCBI.
* [PhiX](ftp://igenome:G3nom3s4u@ussd-ftp.illumina.com/PhiX/Illumina/RTA/PhiX_Illumina_RTA.tar.gz) sequences were downloaded from Illumina.

### Conda Tools Used:
* FastQC
* Trimmomatic
* STAR
* featureCounts (conda Subread)
* Bowtie2
* bwa
* Samtools
* Bam2Fastx
* MultiQC

### Running
To run [Snakemake](https://snakemake.readthedocs.io/en/stable/), a big memory cluster node was used. To run, in the same folder as the snakefile I used ```snakemake -j 80``` which tells Snakemake to use 80 cores. Snakemake if not given a file name searches current directory for a file named *snakefile*.

The output of running Snakemake is a [QC](MultiQC/) folder with results for all of the steps as well as MultiQC which makes nice HTML pages to summarize the results. 

*MultiQC doesn't have the ability to identify and create summaries for microbial contamination with KrakenUniq.*
