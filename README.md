# Single-Cell RNA-Seq Analysis
## ❓What is scRNA-Seq
**Single-cell RNA sequencing (scRNA-seq) analysis** is a powerful technique that allows researchers to measure the gene expression of individual cells within a heterogeneous sample. Unlike bulk RNA sequencing, where gene expression is averaged across all cells, scRNA-seq captures the unique transcriptomic profiles of each cell. This provides insights into cellular diversity, rare cell types, developmental pathways, and responses to treatments at a single-cell resolution.

One of the most widely used tools for scRNA-seq analysis is the **[Seurat](https://satijalab.org/seurat/)** package in R. Seurat is designed to process, analyze, and visualize single-cell RNA-seq data. It offers an integrated pipeline for performing key steps in scRNA-seq analysis, such as normalization, dimensionality reduction, clustering, and differential expression. Seurat has become an essential tool for biologists working with scRNA-seq, offering flexibility and robustness for both novice and advanced users in single-cell analysis.

A typical workflow looks something like this:

![wf](https://github.com/ndomah001/scRNA-Seq-Analysis/blob/main/workflow.jpg)

## 📝 Data
I analyzed a single-cell RNA sequencing dataset of Non-Small Cell Lung Cancer (NSCLC) cells using the Seurat package in R. The dataset, obtained from [10x Genomics](https://www.10xgenomics.com/datasets/20-k-mixture-of-nsclc-dt-cs-from-7-donors-3-v-3-1-3-1-standard-6-1-0), contains approximately 20,000 cells from a mixture of NSCLC donors.

## 📊 Visualizations
### Quality Control Violin Plots
Three violin plots for key quality control metrics:
- `nFeature_RNA`: Number of unique genes detected in each cell.
- `nCount_RNA`: Total number of RNA molecules detected in each cell.
- `percent.mt`: Percentage of mitochondrial genes in each cell.

Interpretation:
- Most cells have between 2,500 and 7,500 unique genes detected.
- The total RNA count per cell mostly ranges from about 5,000 to 50,000.
- The majority of cells have less than 25% mitochondrial RNA, but there's a long tail of cells with higher percentages.

These plots help in determining appropriate thresholds for cell filtering.

![vp](https://github.com/ndomah001/scRNA-Seq-Analysis/blob/main/1.%20violin%20plot.png)

### Feature-Count Correlation Plot
This scatter plot shows the relationship between the number of unique genes (`nFeature_RNA`) and the total RNA count (`nCount_RNA`) per cell.

Interpretation:
- There's a strong positive correlation (0.93) between gene count and RNA count.
- The relationship is roughly linear up to about 10,000 genes, then it plateaus.
- Some outlier cells have very high RNA counts but not proportionally high gene counts, which could indicate doublets or unusually large cells.

![fccp](https://github.com/ndomah001/scRNA-Seq-Analysis/blob/main/2.%20molecules%20x%20genes.png)

### Variable Features Plot
This plot shows the average expression and variability of genes across cells. 

Interpretation:
- Red points represent the 2,000 most variable genes.
- Several highly variable genes are labeled, including `IGHG1`, `IGKC`, and `IGHA1`, which are immunoglobulin genes.
- The most variable genes tend to have moderate to high average expression.
- This plot helps identify genes that are most informative for distinguishing cell types or states.

![cfp](https://github.com/ndomah001/scRNA-Seq-Analysis/blob/main/3%20avg%20expression%20x%20standardized%20variance.png)

### PCA Heatmap
This heatmap shows the top genes contributing to the first principal component (`PC_1`).

Interpretation:
- Genes like `FTL`, `SPP1`, and `APOE` are strongly associated with `PC_1`.
- There's a clear pattern of genes that are either highly expressed (yellow) or lowly expressed (purple) in groups of cells.
- This suggests that `PC_1` is capturing a major axis of variation in the dataset, possibly representing different cell types or states.

![pcah](https://github.com/ndomah001/scRNA-Seq-Analysis/blob/main/4.%20PCA%20heatmap.png)

### Elbow Plot
This plot shows the standard deviation explained by each principal component.

Interpretation:
- There's a sharp drop in explained variance after the first few PCs.
- The "elbow" of the plot is around PC 5-10, suggesting that most of the meaningful variation in the data is captured in the first 10-15 PCs.
- This plot helps in deciding how many PCs to use for downstream analysis. Based on this, using 15 PCs (as done in your analysis) is a reasonable choice.

![ep](https://github.com/ndomah001/scRNA-Seq-Analysis/blob/main/5.%20PC%20x%20std.png)

### PCA Plot
This plot shows the first two principal components (`PC_1` and `PC_2`) of the single-cell data, colored by the cluster assignments at a resolution of 0.5. The different colors represent the 13 distinct cell clusters identified in the data.

Interpretation:
- There is a clear separation between the cell clusters, suggesting that the principal component analysis has effectively captured the major sources of heterogeneity in the NSCLC dataset.
- The distinct grouping of cells indicates that the clustering algorithm has been able to identify biologically meaningful subpopulations within the sample.

![pcap](https://github.com/ndomah001/scRNA-Seq-Analysis/blob/main/6.%20res0.1%20clusters.png)

### UMAP
This is a UMAP (Uniform Manifold Approximation and Projection) visualization of the single-cell data, again colored by the cluster assignments at a resolution of 0.5. UMAP is a non-linear dimensionality reduction technique that preserves the local structure of the data while also capturing global patterns.

Interpretation:
- The UMAP plot shows a similar clustering pattern as the PCA plot, with distinct groups of cells corresponding to the 13 identified clusters.
- The spatial arrangement of the clusters suggests that there are gradual transitions between some of the cell states, rather than a strict separation.
- This could indicate the presence of intermediate or transitional cell types within the NSCLC sample.

![umap](https://github.com/ndomah001/scRNA-Seq-Analysis/blob/main/7.%20res0.5%20clusters.png)

**These findings lay the groundwork for further analyses, such as differential gene expression analysis and cell type annotation, to gain deeper insights into the cellular composition and functional states within the NSCLC tumor microenvironment.**
