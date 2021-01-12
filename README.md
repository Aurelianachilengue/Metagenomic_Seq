# __1.MetagenomeSeq__
_Statistical analysis for sparse high-throughput sequencing_

Broadly speaking, metagenomics is the genetic analysis of microbial communities contained in natural living environments. The metagenomic studies, is focused on understanding the differences in microbial communities caused by phenotypic differences.


The key point of MetagenomeSeq package, is implementation of methods to account for previously unaddressed biases specific to high-throughput sequencing microbial marker-gene survey data.

![Overview MetagenomeSeq](https://raw.githubusercontent.com/Aurelianachilengue/Metagenomic_Seq/main/MetagenomicSeq.PNG)


The Data analyzed in this portfolio was obtained on `Bioconducter: MetagenomicSeq Package` on this [Page](http://www.bioconductor.org/packages/release/bioc/html/metagenomeSeq.html).


```{r}
library(metagenomeSeq)
```

# 2.Data preparation

After the pre-processing of the microbial marker-gene sequence data, counts are defined by clustering reads according to read similarity. Given _m_ features and _n_ samples. The elements in a count matrix C (_m, n_), _cij_, are the number of reads annotated for a particular feature _i_ (whether Operational Taxonomic Unit, species, genus, etc.) in sample _j_.

The count data should be stored in a file with sample names along
the first row and feature names along the first column. Then,the data is prepared and formatted as a __MRexperiment__ object.


# 2.1 BiomFormat

Is a link that we can use to convert the data into __MRexperiment__

```{r}
#reading in a biom file
library(biomformat)
biom_file <- system.file("extdata", "min_sparse_otu_table.biom", package = "biomformat")
b <- read_biom(biom_file)
biom2MRexperiment(b)
```
Followed is an example of writing an MRexperiment object as a BIOM file, using a mouseData MRexperiment object to a BIOM file.

```{r}
data(mouseData)
# options include to normalize or not
b <- MRexperiment2biom(mouseData)

```

# 2.2 Loading count data

After the pre-processing and annotation of sequencing data, metagenomeSeq requires a count matrix with features along rows and samples along the columns. metagenomeSeq includes functions for loading files of counts as loadMeta and phenodata loadPhenoData.

Next we can see the example, a portion of the lung microbiome, were `Operational Taxonomic Unit` (OTU) matrix is provided in metagenomeSeq’s library ”extdata” folder. The OTU matrix is stored as a tab delimited file. loadMeta loads the taxa and counts into a list.

```{r}
dataDirectory <- system.file("extdata", package = "metagenomeSeq")
lung = loadMeta(file.path(dataDirectory, "CHK_NAME.otus.count.csv"))
dim(lung$counts)

```
# 2.3 Loading taxonomy

Next we can load annotated taxonomy and check to make sure that taxa annotations and OTUs are in the same order as your matrix rows.

```{r}
taxa = read.delim(file.path(dataDirectory, "CHK_otus.taxonomy.csv"),
stringsAsFactors = FALSE)
```
Now can add phenodata.

# 2.4 Loading metadata

This function loads the data as a list

```{r}
clin = loadPhenoData(file.path(dataDirectory, "CHK_clinical.csv"),
tran = TRUE)
ord = match(colnames(lung$counts), rownames(clin))
clin = clin[ord, ]
head(clin[1:2, ])

```

# 2.5 Creating a MRexperiment object

Function `newMRexperiment` takes a count matrix, phenoData (annotated data frame), and featureData (annotated data frame) as input. `Biobase` provides functions to create annotated data frames. Library sizes (depths of coverage) and normalization factors are also optional inputs.

```{r}
phenotypeData = AnnotatedDataFrame(clin)
phenotypeData

```
A feature annotated data frame

```{r}
OTUdata = AnnotatedDataFrame(taxa)
OTUdata
```
```{r}
obj = newMRexperiment(lung$counts,phenoData=phenotypeData,featureData=OTUdata)
# Links to a paper providing further details can be included optionally.
# experimentData(obj) = annotate::pmid2MIAME("21680950")
obj

```
# 2.5 Exemple  Datasets

There are two datasets included as examples in the metagenomeSeq package. Data needs to be in a MRexperiment object format to normalize, run statistical tests, and visualize

* Human lung microbiome
