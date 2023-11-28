# Phyloseq-tutorial
Walk through of phyloseq for BIOI 494 bioinformatic tool presentation

## Set Up
The first thing is to install the Biocmanager package:
<code>
install.packages("BiocManager")
</code>

Once that is installed, the next thing to do is to load the 'phyloseq' and 'ggplot2' package
<code>
BiocManager::install("phyloseq")
library(phyloseq); packageVersion("phyloseq")
</code>
> [1] ‘1.46.0’

<code>
BiocManager::install("ggplot2")
library(ggplot2); packageVersion("ggplot2")
</code>

> [1] ‘3.4.4’

## Add Example Files to R environmnt
The example data being used is the phyloseq class is provided by the package; 
however, this is how it would look like forming the phyloseq with an OTU matrix, taxonomy table, and sample metadata table.
<code>
GlobalPatterns = phyloseq(OTU, TAX, sample_metadata)
</code>

<code>
> phyloseq-class experiment-level object
> otu_table()   OTU Table:         [ 19216 taxa and 26 samples ] <br>
> sample_data() Sample Data:       [ 26 samples by 7 sample variables ] <br>
> tax_table()   Taxonomy Table:    [ 19216 taxa by 7 taxonomic ranks ] <br>
> phy_tree()    Phylogenetic Tree: [ 19216 tips and 19215 internal nodes ] <br>
</code>

## Using Accessors
Accessors are are functions that allow you to retrieve specific components or information from a phyloseq-class object. They are able to provide helpful information about microbial data.
The following are a few examples of accessors that can be used.
<code>
#Provides the number of taxa in the data set
ntaxa(GlobalPatterns)
</code>

<code>
> [1] 19216
</code>

<code>
#Provides the number of samples in the data
nsamples(GlobalPatterns)
</code>

<code>
> [1] 26
</code>

<code>
#Gives the names of the first 8 samples in the data set
sample_names(GlobalPatterns)[1:8]
</code>

<code>
> [1] "CL3"     "CC1"     "SV1"     "M31Fcsw" "M11Fcsw" "M31Plmr" "M11Plmr" "F21Plmr"
</code>

<code>
#Lists all the variables of the samples in the data set
sample_variables(GlobalPatterns)
</code>

<code>
> [1] "X.SampleID"               "Primer"                   "Final_Barcode"           
> [4] "Barcode_truncated_plus_T" "Barcode_full_length"      "SampleType"              
> [7] "Description" 
</code>

## Using Processors
Processors are functions used to manipulate and alter the phyloseq object. These functions include the ability to do filtering, subsetting, and merging abundance data.
The following are a couple of functions that can be used to filter or subset the microbial data within a phyloseq-class object.

<code>
#This creates a new phyloseq object identical to the original and modifies it to remove any sample with less than 100000 reads
GP.prune = GlobalPatterns
GP.prune = prune_samples(sample_sums(GlobalPatterns)>=100000, GP.prune)
nsamples(GlobalPatterns)
>[1] 26 
nsamples(GP.prune)
>[1] 25
#1 sample was removed from the object
</code>



