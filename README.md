# Cell type transfer with scvi-tools

Documentation for cell type transfer/ automatic cell type labeling with the [scvi-tools](https://scvi-tools.org/) package.
The notebook `scvi_cell_transfer.ipynb` shows how to train `scVI` and `scANVI` models and how to transfer celltypes from
labeled to unlabeled datasetse with them.

Five liver datasets were used for this example. The following explains:

* how to download / where to find the datasets
* how to label the datasets
* hoiw to train a scVI/scANVI model

## Datasets

### Dataset 1

* healthy-cirrhotic-human-liver-10XV2.loom
* Ramachandran P, et al. (2019) Resolving the fibrotic niche of human liver cirrhosis at single-cell level. Nature 575(7783):512-518.
* Tech: 10X Genomics
* Source: [Human Cell Atlas](https://data.humancellatlas.org/)

### Dataset 2

* sc-landscape-human-liver-10XV2.loom
* [Single cell RNA sequencing of human liver reveals distinct intrahepatic macrophage populations](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6197289/)
* Tech: 10X Genomics
* Source: [Human Cell Atlas](https://data.humancellatlas.org/)

### Dataset 3

* liver-immune-cells-human-liver-10XV2.loom
* [Single-cell RNA sequencing reveals the heterogeneity of liver-resident immune cells in human.](https://www.nature.com/articles/s41421-020-0157-z)
* Tech: 10X Genomics
* Source: [Human Cell Atlas](https://data.humancellatlas.org/)

### Dataset 4

* GSE124395
* [A human liver cell atlas reveals heterogeneity and epithelial progenitors](https://www.nature.com/articles/s41586-019-1373-2)
* Tech: mCEL-Seq2 protocol
* Source: <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE124395>

### Dataset 5

* GSE158723
* [Single-cell RNA sequencing of human liver reveals hepatic stellate cell heterogeneity](https://www.sciencedirect.com/science/article/pii/S2589555921000549)
* Tech: 10X Genomics
* Source: <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE158723>
* Note: merged the different samples

## Cell type labeling

## Label transfer with scANVI
