# Phyloseq-tutorial
Walk through of phyloseq for BIOI 494 bioinformatic tool presentation

## Set Up
The first thing is to install the Biocmanager package:
<code>
install.packages("BiocManager")
</code>

Once that is installed, the next thing to do is to load the 'phyloseq' package
<code>
BiocManager::install("phyloseq")
library(phyloseq); packageVersion("phyloseq")
</code>

{
[1] ‘1.46.0’
}
