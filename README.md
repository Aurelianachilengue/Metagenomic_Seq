# __MetagenomeSeq__
_Statistical analysis for sparse high-throughput sequencing_

Broadly speaking, metagenomics is the genetic analysis of microbial communities contained in natural living environments. The metagenomic studies, is focused on understanding the differences in microbial communities caused by phenotypic differences.


The key point of MetagenomeSeq package, is implementation of methods to account for previously unaddressed biases specific to high-throughput sequencing microbial marker-gene survey data.

![Overview MetagenomeSeq](https://raw.githubusercontent.com/Aurelianachilengue/Metagenomic_Seq/main/MetagenomicSeq.PNG)


The Data analyzed in this portfolio was obtained on `Bioconducter: MetagenomeSeq Package` in this [link](http://www.bioconductor.org/packages/release/bioc/html/metagenomeSeq.html).


```{r}
library(metagenomeSeq)
```

```{r}
library(biomformat)
biom_file <- system.file("extdata", "min_sparse_otu_table.biom", package = "biomformat")
b <- read_biom(biom_file)
biom2MRexperiment(b)
```
