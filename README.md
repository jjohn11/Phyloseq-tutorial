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


