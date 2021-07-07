# Cell type transfer with scvi-tools

Documentation for cell type transfer/ automatic cell type labeling with the [scvi-tools](https://scvi-tools.org/) package.
The notebook `scvi_cell_transfer.ipynb` shows how to train `scVI` and `scANVI` models and how to transfer celltypes from
labeled to unlabeled datasetse with them.

Five liver datasets were used for this example. The following explains:

* how to download / where to find the datasets
* how to label the datasets
* hoiw to train a scVI/scANVI model

## Datasets

The following lists all datasets that were used. Three datasets come from the Human Cell Atlas (HCA). You can search for them by selecting liver as tissue, and then download the `.loom` file. The other datasets are available from GEO, and their GSE-accessions are given.

### Dataset 1

* healthy-cirrhotic-human-liver-10XV2.loom
* Ramachandran P, et al. (2019) Resolving the fibrotic niche of human liver cirrhosis at single-cell level. Nature 575(7783):512-518.
* Tech: 10X Genomics
* Source: [Human Cell Atlas](https://data.humancellatlas.org/)
* Labeling: `healthy_cirrhotic_human_liver_labeling.ipynb`

### Dataset 2

* sc-landscape-human-liver-10XV2.loom
* [Single cell RNA sequencing of human liver reveals distinct intrahepatic macrophage populations](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6197289/)
* Tech: 10X Genomics
* Source: [Human Cell Atlas](https://data.humancellatlas.org/)
* Labeling: `sc_landscape_human_liver_labeling.ipynb`

### Dataset 3

* liver-immune-cells-human-liver-10XV2.loom
* [Single-cell RNA sequencing reveals the heterogeneity of liver-resident immune cells in human.](https://www.nature.com/articles/s41421-020-0157-z)
* Tech: 10X Genomics
* Source: [Human Cell Atlas](https://data.humancellatlas.org/)
* Labeling: `liver_immune_cells_human_liver_labeling.ipynb`

### Dataset 4

* GSE124395
* [A human liver cell atlas reveals heterogeneity and epithelial progenitors](https://www.nature.com/articles/s41586-019-1373-2)
* Tech: mCEL-Seq2 protocol
* Source: <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE124395>
* Labeling: `GSE124395_labeling.ipynb`

### Dataset 5

* GSE158723
* [Single-cell RNA sequencing of human liver reveals hepatic stellate cell heterogeneity](https://www.sciencedirect.com/science/article/pii/S2589555921000549)
* Tech: 10X Genomics
* Source: <https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE158723>
* Note: merged the different samples
* Labeling: `gse158723_multi_labeling.ipynb`

## Cell type labeling

Once all datasets are downloaded, you can use the respective labeling `.ipynb` scripts to generate `.h5ad` files with cell type labels that are ready for further analysis. For the files from HCA, you should be able to directly use the loom files with the labeling scripts. The GSE158723 dataset consists of multiple files. The labeling script can take care of this, but you will have to store them all in the corresponding folder and adjust the file paths in the script. For GSE124395, you can download the `GSE124395_Normalhumanlivercellatlasdata.txt` file, but you will have to transpose it in order to work with the script. There is commented code in the first few cells of the respective notebook that needs to be run once and can then be commented out again.

Generally you might have to adjust the file paths in the labeling script.

## Label transfer with scANVI

Once the datasets are downloaded and the labeled `.h5ad` files are generated, you can use the `scvi_cell_transfer.ipynb` script to perform the analysis with `scvi-tools`.

This Notebook is extensively documented so it is easiest to go through the notebook.

### Dataset integration with scARCHES

I also looked into scARCHES for adding new datasets to existing scVI/scANVI models. I ultimately stopped looking into this though, for a few reasons.
First, the issue with training a model and then adding new data later is that the training features must match. So in this case it is genes. This could mean deleting genes
or not having the optimal genes for a new dataset.
Second, training a scVI/scANVI model actually doesn't take that much time. Other methods are much more time intensive. So there is no real benifit of fitting a dataset to
a existing model with scARCHES.
Finally, one important feature of scARCHES is that the latent space for the existing datasets stays the same, and onle the new dataset is added on top. This might be a really nice feature for a big resource, but for analysis at QBiC it is not needed.

For these reasons I think it is easiest to save labeled datasets somewhere and then just train a new scVI/scANVI model whenever necessary. With a GPU this might take less than an hour, without maybe 1-2h (also depends on the size of the dataset).