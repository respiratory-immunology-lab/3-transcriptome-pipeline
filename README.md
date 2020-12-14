Using the 3'-transcriptome pipeline for low input RNAseq analysis
=================================================================

Here we provide a R Notebook template to generate a gene counts table from FASTQ files generated by Paired-End Illumina sequencing using the Qiagen UPX transcriptome library preparation kit (<a href="https://www.qiagen.com/au/products/discovery-and-translational-research/next-generation-sequencing/rna-sequencing/three-rnaseq/qiaseq-upx-3-transcriptome-kits/#orderinginformation" target="_blank">see here</a>). For maximal reproducibility, we also provide a R project file and its associated packrat packages management directory.

Note: Commands described in this documentation assume that you are using a Unix CLI.

## System requirements

The minimal requirements are listed below then further detailed in this section:

* **R 3.6.0:** https://www.r-project.org
* **R package renv:** https://cran.r-project.org/web/packages/renv/index.html
* **RStudio:** https://www.rstudio.com
* **git:** https://git-scm.com/

#### R

The transcriptome-scPipe pipeline comes as a R package. Make sure that R (3.6.0 or higher) is installed before starting.

#### R renv package

R packages are managed using renv. This ensures maximal reproducibility and portability of the analysis by using an encapsulated, version controlled, installation of R packages instead of any system-level R packages installation.

Make sure that the renv R package is installed before starting:

```
# R
> install.packages("renv")
```

#### RStudio

The `transcriptome-scPipe.Rmd` file provided in this repository are a R Notebook. As such, it includes both code lines (chunks) and text and can be exported into html and pdf files.

The prefered way of using these files is with the RStudio Integrated Development Environment (IDE). Make sure you have RStudio installed before starting.

#### git

This repository is managed using the git distributed version control system. You can get a local copy of it using the `git clone` command.
If not done yet, install git.

On debian linux, you can install git using the `apt-get` package manager command:
```
$ apt-get install git
```

## Files

Before starting, make sure you have the five files listed below:

1. **`[laneNN]R1.fastq.gz`**: FASTQ file(s) for the forward read
2. **`[laneNN]R2.fastq.gz`**: FASTQ file(s) for the reverse read
3. **`Samples_barcodes.csv`**: A comma-delimited text file mapping barcodes to samples (1)
4. A reference genome in fasta format: For example, `Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz`
5. A gene annotation file in GFF3 format: For example, `Homo_sapiens.GRCh38.98.gff3.gz`

```
# Download genome
wget http://ftp.ensembl.org/pub/release-98/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna_sm.primary_assembly.fa.gz

# Download gene annotation file
wget http://ftp.ensembl.org/pub/release-98/gff3/homo_sapiens/Homo_sapiens.GRCh38.98.gff3.gz
```

It is assumed that the FASTQ files were archived using gzip.

(1) The `Samples_barcodes.csv` file must contain two comma-delimited columns: the first for samples names and the second for samples barcodes as shown <a href="https://drive.google.com/file/d/1MQtRGfdJSjdvb8NeWTaA8_fcV82NiDZm/view?usp=sharing" target="_blank">here</a>. Avoid special characters.

## Preparation

Get a copy of this repository (give it any name `my_project_dir`) and set it as your working directory:
```
$ git clone https://github.com/respiratory-immunology-lab/trancriptome-scPipe.git
 my_project_dir
$ cd my_project_dir
```
If not done yet, get a copy of the reference databases of your choice. We recommend using Ensembl repository: https://asia.ensembl.org/info/data/ftp/index.html.

Place the `Samples_barcodes.csv` file in the main directory, then place your FASTQ files within the directory named `run_data`.
The final directory structure should look like:
<pre>
my_project_dir
├── aligment
├── data
├── demultiplexed
├── renv
|   └── ...
├── renv.lock
├── run_data
|   ├── <b>[lane1]R1.fastq.gz</b>
|   ├── <b>[lane2]R1.fastq.gz</b>
|   ├── <b>[lane3]R1.fastq.gz</b>
|   ├── <b>[lane4]R1.fastq.gz</b>
|   ├── <b>[lane1]R2.fastq.gz</b>
|   ├── <b>[lane2]R2.fastq.gz</b>
|   ├── <b>[lane3]R2.fastq.gz</b>
|   └── <b>[lane4]R2.fastq.gz</b>
├── packrat
|   └── ...
├── <b>Samples_barcodes.csv</b>
├── LICENSE.txt
├── README.md
├── transcriptome-scpipe.Rmd
└── transcriptome-scpipe.Rproj
</pre>

## Usage

1. Load the `transcriptome-scpipe.Rproj` R project file in RStudio.

2. Open the ` transcriptome-scpipe.Rmd` R Notebook template in RStudio and follow the instructions in the text and comments. At the end of the pipeline, inital files and results are archived into two separate archives. 

3. Store archives in a safe place!

## Run it on the cluster

One possibility is to run it on an interactive smux session. The setting is: `smux n --ntasks=20 --mem=50000 -J Qiagen --nodes=1 --time=3-00:00:00`.

## Citation

If you used this repository in a publication, please mention its url.

In addition, you may cite the tools used by this pipeline:

* **scPipe:** Tian L, Su S, Dong X, Amann-Zalcenstein D, Biben C, Seidi A, Hilton DJ, Naik
SH, Ritchie ME. scPipe: "A flexible R/Bioconductor preprocessing pipeline for
single-cell RNA-sequencing data." PLoS Comput Biol. 2018 Aug 10;14(8):e1006361.
doi: 10.1371/journal.pcbi.1006361.

* **Rsubread:** Liao Y, Smyth GK, Shi W. "The R package Rsubread is easier, faster, cheaper and
better for alignment and quantification of RNA sequencing reads. Nucleic Acids
Res. 2019 May 7;47(8):e47. doi: 10.1093/nar/gkz114."

## Rights

* Copyright (c) 2019 Respiratory Immunology lab, Monash University, Melbourne, Australia.
* License: The R Notebook template (.Rmd) is provided under the MIT license (See LICENSE.txt for details)
* Authors: C. Pattaroni, B.J. Marsland
