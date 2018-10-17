---
title: "Uncertainity in RNA"
author: "Sonali Arora, Hamid Bolouri"
date: "October 16, 2018"
output: 
  html_document:
    toc: true
    theme: united
---

## Introduction

This github repository contains code to reproduce the analysis in our paper 
"Errors in RNA-seq transcript abundance estimates". A copy of the paper can be 
found [here]()

### Additional Figures

This github includes a large number of additional supplementary figures, not 
present in the online version of this paper.  

1) [Additional Fig 1. TCGA batch effects by PlateID](https://github.com/sonali-bioc/UncertainityRNA/blob/master/data/pdf/Supp_PCA_PlateID_batch_Binder.pdf)  
2) [Additional Fig 2. TCGA batch effects by TSS ID](https://github.com/sonali-bioc/UncertainityRNA/blob/master/data/pdf/Supp_TCGA_PCA_TSS_batch_Binder.pdf)
3) [Additional Fig 3. TCGA batch effects by Sequencing Center](https://github.com/sonali-bioc/UncertainityRNA/blob/master/data/pdf/Supp_TCGA_PCA_Sequening%20center_Batch_Binder.pdf)  
4) [Additional Fig 4. GTEX batch effects (genotype batches) Part 1](https://github.com/sonali-bioc/UncertainityRNA/blob/master/data/pdf/Supp_GTEx_genotype_batches_part1.pdf)  
5) [Additional Fig 5. GTEX batch effects (genotype batches) Part 2](https://github.com/sonali-bioc/UncertainityRNA/blob/master/data/pdf/Supp_GTEx_genotype_batches_part2.pdf)  
6) [Additional Fig 6. GTEX batch effects (nucelic acid batches) Part 1](https://github.com/sonali-bioc/UncertainityRNA/blob/master/data/pdf/Supp_GTEx_nucleic_acid_batches_part1.pdf)   
7) [Additional Fig 6. GTEX batch effects (nucelic acid batches) Part 2](https://github.com/sonali-bioc/UncertainityRNA/blob/master/data/pdf/Supp_GTEx_nucleic_acid_batches_part2.pdf)   
8) [Additional Fig 6. GTEX batch effects (nucelic acid batches) Part 3](https://github.com/sonali-bioc/UncertainityRNA/blob/master/data/pdf/Supp_GTEx_nucleic_acid_batches_part3.pdf)   
9) [Additional Fig 6. GTEX batch effects (nucelic acid batches) Part 4](https://github.com/sonali-bioc/UncertainityRNA/blob/master/data/pdf/Supp_GTEx_nucleic_acid_batches_part4.pdf)   
10) [Additional Fig 6. GTEX batch effects (nucelic acid batches) Part 5](https://github.com/sonali-bioc/UncertainityRNA/blob/master/data/pdf/Supp_GTEx_nucleic_acid_batches_part5.pdf)   
11) [Additional Fig 6. GTEX batch effects (nucelic acid batches) Part 6](https://github.com/sonali-bioc/UncertainityRNA/blob/master/data/pdf/Supp_GTEx_nucleic_acid_batches_part6.pdf)   

## Downloading Data 

### Data folder Organization

To run our code, you need to download data from two different sources  

a) Download all source data and processed Summarized Experiment objects from 
Amazon S3 bucket.

b) These vignettes from the github directory.   

Both the folder from Amazon s3 bucket (ie OriginalTCGAGTExData) and the folder
containing vignettes (git repository) should be saved in the same folder. 
As an example, one could save both of the above folders under "Downloads" 
as shown below


```{}

# folder where S3BUCKET data and github directory are stored. eg: ~/Downloads

# github directory eg: ~/Downloads/UncertainityRNA

# S3 bucket directory eg: ~/Downloads/OriginalTCGAGTExData

# when you run our RMD files, a new subfolder called "data will be created"
# This will essentially remake the "data" subfolder from github repository.
# eg:~/Downloads/data

```

### Amazon S3 Bucket Data

####  Download Processed Data 

If you want to download only the final SE Objects to recreate
figures in our paper, the below mentioned  code will create a 
folder called "OriginalTCGAGTExData" and only 
one sub-folder "SE_objects" and its contents will be downloaded to it.


```{}
wget --recursive -nH --cut-dirs=1 https://s3-us-west-2.amazonaws.com/fh-pi-holland-e/OriginalTCGAGTExData/SE_objects/index.html
```


#### Download complete data in chunks

If you would like to download all the data associated with this Paper, it is 
recommended to download the data in chunks using the following commands 

```{}
wget --recursive -nH --cut-dirs=1 https://s3-us-west-2.amazonaws.com/fh-pi-holland-e/OriginalTCGAGTExData/annotations/index.html
wget --recursive -nH --cut-dirs=1 https://s3-us-west-2.amazonaws.com/fh-pi-holland-e/OriginalTCGAGTExData/datasource_XENA/index.html
wget --recursive -nH --cut-dirs=1 https://s3-us-west-2.amazonaws.com/fh-pi-holland-e/OriginalTCGAGTExData/datasource_GDC/index.html
wget --recursive -nH --cut-dirs=1 https://s3-us-west-2.amazonaws.com/fh-pi-holland-e/OriginalTCGAGTExData/datasource_GTEX_v6/index.html
wget --recursive -nH --cut-dirs=1 https://s3-us-west-2.amazonaws.com/fh-pi-holland-e/OriginalTCGAGTExData/datasource_MSKCC/index.html
wget --recursive -nH --cut-dirs=1 https://s3-us-west-2.amazonaws.com/fh-pi-holland-e/OriginalTCGAGTExData/datasource_PICCOLO/index.html
wget --recursive -nH --cut-dirs=1 https://s3-us-west-2.amazonaws.com/fh-pi-holland-e/OriginalTCGAGTExData/datasource_RECOUNT2_GTEX/index.html
wget --recursive -nH --cut-dirs=1 https://s3-us-west-2.amazonaws.com/fh-pi-holland-e/OriginalTCGAGTExData/datasource_RECOUNT2_TCGA/index.html

wget --recursive -nH --cut-dirs=1 https://s3-us-west-2.amazonaws.com/fh-pi-holland-e/OriginalTCGAGTExData/combined_SEobjects/index.html
wget --recursive -nH --cut-dirs=1 https://s3-us-west-2.amazonaws.com/fh-pi-holland-e/OriginalTCGAGTExData/SE_objects/index.html
```

#### Complete Data Download

**WARNING:** Please note that downloading all the data will take take a long time.

```{}
wget --recursive -nH --cut-dirs=1 https://s3-us-west-2.amazonaws.com/fh-pi-holland-e/OriginalTCGAGTExData/index.html
```

The above line will create a folder called "OriginalTCGAGTExData" and 
the following sub-folders 
1) annotations    
2) data source_GDC   
3) data source_GTEX_v6  
4) data source_MSKCC  
5) data source_PICCOLO  
6) data source_RECOUNT2_GTEX  
7) data source_RECOUNT2_TCGA  
8) data source_XENA  
9) combined_SEobjects  
10) SE_objects

### Clone this github repository 

One can clone this github repository with : 

```{}
git clone https://github.com/sonali-bioc/UncertainityRNA.git
```

### MD5SUM for downloaded files

The md5sum for all downloaded files from s3 bucket have been places 
[here](https://github.com/sonali-bioc/UncertainityRNA/blob/master/data/file_md5sums.txt).


## Vignette Overview

The steps below provide a roadmap for the analysis done in the paper:

### 1) Acquiring TCGA data

In this [vignette](https://github.com/sonali-bioc/UncertainityRNA/blob/master/01_Acquiring_TCGA_Data_various_sources.Rmd) we show in detail how data was downloaded from each source 
of TCGA Data. For easier manipulation of this large data set, we convert the large
text files to SummarizedExperiment objects.

### 2) Acquiring GTEX data

In this [vignette](https://github.com/sonali-bioc/UncertainityRNA/blob/master/02_Acquiring_GTEx_Data_various_sources.Rmd) we show in detail how data was downloaded from each source 
of GTEx Data. For easier manipulation of this large data set, we convert the large
text files to SummarizedExperiment objects.

### 3) Creating TPM Normalized SE objects for TCGA data.

In this [vignette](https://github.com/sonali-bioc/UncertainityRNA/blob/master/03_Creating_TPM_TCGA_Data_objects.Rmd) , we first find common genes and common
samples present in each source of TCGA Data. Next, we convert RPKM normalized
data to TPM normalized data.

### 4) Creating TPM Normalized SE objects for GTEx data

In this [vignette](https://github.com/sonali-bioc/UncertainityRNA/blob/master/04_Creating_TPM_GTEx_Data_objects.Rmd) , we first find common genes and common
samples present in each source of GTEx Data. Next, we convert RPKM normalized
data to TPM normalized data.

### 5) PCA using RPKM normalized data

In this [vignette](https://github.com/sonali-bioc/UncertainityRNA/blob/master/05_RPKM_normalized_Data.Rmd), we take RPKM normalized data from all sources of TCGA
and GTEx data and compute Principal Components to see how similar/dissimilar
these data sources are. The results from PCA analysis are stored as text files, 
which can be used later on for plotting in multi-panel figures.

### 6) PCA  using TPM normalized data

In this [vignette](https://github.com/sonali-bioc/UncertainityRNA/blob/master/06_TPM_normalized_Data.Rmd), we use TPM normalized data from all sources of TCGA
and GTEx data and compute Principal Components to see how similar/dissimilar
these data sources are. The results from PCA analysis are stores as text files, 
which can be used later on for plotting in multi-panel figures.

### 7) Discordant Genes

In this [vignette](https://github.com/sonali-bioc/UncertainityRNA/blob/master/07_Discordant_genes_samples.Rmd), we calculate  
- discordant genes across various TCGA sources  
- discordant genes across various GTEx sources  
- discordant samples across various TCGA sources  
- discordant samples across various GTEx sources  
- compare the discordant genes to disease related genes   
- compare the discordant genes to multi-mapped reads as reported by Robert et al.  

### 8) Supplemental Tables

In this [vignette](https://github.com/sonali-bioc/UncertainityRNA/blob/master/08_Supp_Tables.Rmd), we calculate various Supplemental Tables for our paper.
These tables are also subsequently used in our analysis. They include  
- mRNA correlations across various TCGA sources  
- mRNA correlations across various GTEx sources  
- Protein-mRNA correlations across various TCGA sources   

### 9) Supplemental Figures

In this [vignette](https://github.com/sonali-bioc/UncertainityRNA/blob/master/09_Supp_Figures.Rmd), we make various supplemental figure for our paper.

### 10) Batches in TCGA Data

In this [vignette](https://github.com/sonali-bioc/UncertainityRNA/blob/master/10_github_tcga_batches.Rmd), we make various PCA plots for each type of cancer using 
the following Batch variables: TSS, PlateID and Sequencing center for various 
source of TCGA data.

### 11) Batches in GTEx Data

In this [vignette](https://github.com/sonali-bioc/UncertainityRNA/blob/master/11_github_gtex_batches.Rmd), we make various PCA plots using "Nucleic Acid" and 
"Genotype" Batches for all sources of GTEx data.

### 12) Combining GTEx and TCGA Data

In this [vignette](https://github.com/sonali-bioc/UncertainityRNA/blob/master/12_github_combine_tcga_gtex_data.Rmd), we follow the approach showed in Wang et al, to taking three example
regions = "Thyroid, Stomach and Liver" from GTEx, and their corresponding 
cancer Types( "THCA", "LIHC", "STAD") and making PCA plots  for each data source 
to see how similar/dissimilar TCGA and GTEx data are, for various data sources.

### 13) Figure 1 of submitted paper

In this [vignette](https://github.com/sonali-bioc/UncertainityRNA/blob/master/13_Fig1_PCA_plots.Rmd), we reproduce Figure 1 of our paper.

### 14) Figure 2 of submitted paper

In this [vignette](https://github.com/sonali-bioc/UncertainityRNA/blob/master/14_Fig2_Pipeline_Differences.Rmd), we reproduce Figure 2 of our paper.

## References 

1) Grossman, Robert L., Heath, Allison Pet al. (2016) Toward a Shared Vision for Cancer Genomic Data. New England Journal of Medicine
2) Vivian J, Rao AA, Nothaft FA, et al. (2017) Toil enables reproducible, open source, big biomedical data analyses. Nature biotechnology. 
3) Collado-Torres L, Nellore A, et al (2017) Reproducible RNA-seq analysis using recount2. Nature biotechnology.
4) Q. Wang, J Armenia, C. Zhang, A.V. Penson, E. Reznik, L. Zhang, T. Minet, A. Ochoa, B.E. Gross, C. A. Iacobuzio-Donahue, D. Betel, B.S. Taylor, J. Gao, N. Schultz. Unifying cancer and normal RNA sequencing data from different sources. Scientific Data 5:180061, 2018.
5) Rahman M, et al. (2015) Alternative preprocessing of RNA-Sequencing data in TCGA leads to improved analysis results. Bioinformatics.
6) The GTEx Consortium. The Genotype-Tissue Expression (GTEx) project. (2013) Nature genetics.
7) Robert, C. & Watson, M. Errors in RNA-Seq quantification affect genes of relevance to human disease. Genome Biol 16, 177 (2015)
8) R Core Team (2018). R: A language and environment for statistical computing. R Foundation for Statistical Computing, Vienna, Austria. URL https://www.R-project.org/.


## Tools used for analysis 

All our analysis is done in R. We found the following  R/Biocondcutor packages 
extremely useful in our analysis.

1) [SummarizedExperiment](https://bioconductor.org/packages/release/bioc/html/SummarizedExperiment.html) for creating and storing TCGA and GTEX data as 
SE objects.
2) [GenomicRanges](https://bioconductor.org/packages/release/bioc/html/GenomicRanges.html) for manipulating genomic ranges.
3) [rtracklayer](https://bioconductor.org/packages/release/bioc/html/rtracklayer.html) for reading in GTF files quickly as GenomicRanges objects 
4) [ggplot2](https://ggplot2.tidyverse.org/) for making most of the plots in our paper. 
5) [pheatmap](https://cran.r-project.org/web/packages/pheatmap/index.html) for making heatmaps
6)  We also used [RColorBrewer](https://cran.r-project.org/web/packages/RColorBrewer/index.html), [UpSetR](https://cran.r-project.org/web/packages/UpSetR/README.html) and [eulerr](https://cran.r-project.org/web/packages/eulerr/index.html)

