# Cluster Separability Task

This repository contains example scripts for the HCA jamboree problem on cluster separability. Referenced data can be found on the Jamboree server under `/data/tasks/how_many_cells`

## First Deliverable : Calculate actual separability for two clusters in a dataset

**Input:** Gene expression matrix for a full dataset, with pre-determined clustering

**Output:** Separability of any two clusters

**Input arguments to script:**

* Loom file of entire dataset, contains cluster ID for each cell
* Names of the two clusters to determine separability (as separate values)

**Output:**

* A single number: the "separability" of the two clusters, output to console

Example: `Rscript --vanilla actual_separability.R human_pancreas.loom activated_stellate quiescent_stellate`


## Second Deliverable : Predict separability of two clusters, as a function of total cell number in the dataset

**Input:** Gene expression only for example cells that are members of the two clusters, and their cluster frequencies in the full dataset

**Output:** Predicted separability of the clusters as a function of total cell number.

**Input arguments to script:**

* Loom file containing example cells representing the two clusters. Contains the cluster ID for each cell

**Output:** Predicted separability of the clusters as a function of total cell number.
  
* Frequency of the two clusters, in the total dataset (as separate values)
* Path to a TSV file, which will contain two columns.
  1. Number of cells (ranging from 1,000 to 100,000 - with a step of 1,000)
  2. Predicted separability

Example: `Rscript --vanilla predicted_separability.R human_pancreas_activated_quiescent_stellate.loom 0.03 0.02 predictions.tsv`

## Additional notes:

* All data files are stored according to the loom specification, an HDF5-based format. Each contains a UMI matrix, cell_names and cluster ID as column attributes, and gene_names as a row attribute.
* human_pancreas.loom - Human inDrop dataset of 8,569 human pancreatic islet cells.
* For our example "predicted separability" model, we construct a dummy function that considers only the number of DE genes (>2-fold change) as input.

## Example task execution

* See [hcajamboree_howmanycells_vignette.html](https://cdn.rawgit.com/HumanCellAtlas/hca-jamboree-how-many-cells/ajc-upload/hcajamboree_howmanycells_vignette.html) for a worked example of this task. 
