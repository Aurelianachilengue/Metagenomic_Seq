# __MetagenomeSeq__
_Statistical analysis for sparse high-throughput sequencing_

Broadly speaking, metagenomics is the genetic analysis of microbial communities contained in natural living environments. The metagenomic studies, is focused on understanding the differences in microbial communities caused by phenotypic differences.


The key point of MetagenomeSeq package, is implementation of methods to account for previously unaddressed biases specific to high-throughput sequencing microbial marker-gene survey data.

![Overview MetagenomeSeq](https://raw.githubusercontent.com/Aurelianachilengue/Metagenomic_Seq/main/MetagenomicSeq.PNG)



The Data analyzed in this portfolio was obtained on `Bioconducter: MetagenomicSeq Package` on this [Page](http://www.bioconductor.org/packages/release/bioc/html/metagenomeSeq.html).

The Data analyzed in this portfolio was obtained on `Bioconducter: MetagenomeSeq Package` in this [link](http://www.bioconductor.org/packages/release/bioc/html/metagenomeSeq.html).


```{r}
library(metagenomeSeq)
```

## Data preparation

After the pre-processing of the sequence data of Microbial marker-gene,counts are defined by clustering reads according to read similarity. Given _m_ features and _n_ samples.  the elements in a count matrix C (m, n), cij , are the number of reads annotated
for a particular feature i (whether Oprational Taxonomic Unit, species, genus, etc.) in sample j.

The count data should be stored in a file with sample names along
the first row and feature names along the first column. Then,the data is prepared and formatted as a __MRexperiment__ object.

## BiomFormat

Is a link that we can use to convert the data into __MRexperiment__
```{r}
library(biomformat)
biom_file <- system.file("extdata", "min_sparse_otu_table.biom", package = "biomformat")
b <- read_biom(biom_file)
biom2MRexperiment(b)
```

