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
The example data being used is the phyloseq object is provided by the package; 
however, this is how it would look like forming the phyloseq with an OTU matrix, taxonomy table, and sample metadata table.
<code>
GlobalPatterns = phyloseq(OTU, TAX, sample_metadata)
</code>

To add the example data to the R environment use:

<code>
data(GlobalPatterns)
</code>

The phyloseq object should present as:

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


## Ordination Plots
Ordination is often employed to explore and represent the relationships between samples based on their composition or other characteristics. Use ordinate() function to create ordination class. In the function you will specify the Phyloseq class, the statistical analysis you want, and the name of a supported distance method. 

<code>
#Plot ordination
GP.ord <- ordinate(GlobalPatterns, "NMDS", "bray")
#Plots the OTUs by Family
plot_ordination(GlobalPatterns, GP.ord, type="Family", title="Family")
</code>

![image](https://github.com/jjohn11/Phyloseq-tutorial/assets/148915446/2bd97e03-5f6c-48fc-a4e2-af82a0725af2)


## Plot Alpha Diversity 
The plot_richness function is used to create richness plots, which visualize alpha diversity measures across samples.

<code>
#Specifying a measures argument Simpson and Fisher, which will include just the alpha-diversity measures that we want.
#Specifying a sample variable (SampleType and Human) on which to group/organize samples along the horizontal (x) axis
plot_richness(GlobalPatterns, x="human", color="SampleType", measures=c("Simpson", "Fisher"))
</code>  

![image](https://github.com/jjohn11/Phyloseq-tutorial/assets/148915446/d105a87c-4b9a-4deb-aded-24073fa6b976)

## Bar Plots
Bar plots generate insightful visual summaries depicting variations in taxa abundance among samples within an experiment. Depending on the parameters you choose to separate the data, it will result in more in depth look comparing between specific variables

<code>
#Using subset_taxa to focus on specific phylum, this particular phylum is small to be visually informative
GP.Chlam = subset_taxa(GlobalPatterns, Phylum == "Chlamydiae")
#Using color to assign the Genus which the OTU belongs to
plot_bar(GP.Chlam, x="SampleType", fill="Genus")
</code>

![image](https://github.com/jjohn11/Phyloseq-tutorial/assets/148915446/c2b2bf31-62ec-4a6d-9919-387df24aa23f)

## Heat Map
plot_heatmap creates a heat map which can be used to observe the patterns of high-abundance OTUs in the context of a matrix with lower abundance OTUs in all samples

<code>
#Using subset_taxa to create a new phyloseq object to focus on specific phylum, this particular phylum is small to be visually informative
GP.heat <- subset_taxa(GlobalPatterns, Phylum =="Crenarchaeota")
# plotting new phyloseq object, using low and high parameters to assign colors for low abundance and high abundance
plot_heatmap(GP.heat,low="#000033", high="#66CCFF")
</code>

![image](https://github.com/jjohn11/Phyloseq-tutorial/assets/148915446/29898178-f3cc-455c-a704-6ba1ea908a09)




