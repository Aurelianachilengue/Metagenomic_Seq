# __Metagenomic_Seq__
_Statistical analysis for sparse high-throughput sequencing_

Broadly speaking, metagenomics, also known as community genomics, is the genetic analysis of microbial communities contained in natural living environments.

Originally focused on exploratory and validation projects, these studies now focus on understanding the differences in microbial communities caused by phenotypic differences.

The key point of Metagenomic_Seq package, is implementation of methods to account for previously unaddressed biases specific to high-throughput sequencing microbial marker-gene survey data

The Data analyzed in this portfolio was obtained on 

```{r}
library(metagenomeSeq)
```

```{r}
library(biomformat)
biom_file <- system.file("extdata", "min_sparse_otu_table.biom", package = "biomformat")
b <- read_biom(biom_file)
biom2MRexperiment(b)
```
