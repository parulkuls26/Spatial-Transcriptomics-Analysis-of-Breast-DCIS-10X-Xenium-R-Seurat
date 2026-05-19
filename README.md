Spatial Transcriptomics Analysis of Breast DCIS (10X Xenium, R/Seurat)
Dataset: Janesick et al., Nature Communications (2023) — 10X Xenium in situ spatial transcriptomics
Tool: Seurat (R) | Environment: RStudio

Overview
This analysis explores 10X Xenium spatial transcriptomics data from a human breast ductal carcinoma in situ (DCIS) tissue slide. DCIS is a pre-invasive form of breast carcinoma in which 25–60% of untreated cases progress to invasive ductal carcinoma (IDC). A key clinical challenge is distinguishing progressive from non-progressive DCIS to avoid over- or under-treatment.
The analysis focuses on the role of myoepithelial cells (MECs), which form a protective barrier around ductal structures in normal breast tissue. Disruption of this layer is associated with increased risk of DCIS progression to invasion.

Aims

Perform quality control on the Xenium dataset
Identify cell clusters via unsupervised clustering
Assign cell type identities — including myoepithelial cells — to each cluster
Analyse the spatial distribution of myoepithelial cells relative to other cell types


Methods
QC & Filtering

167,780 cells loaded; filtered to 161,789 (3.5% removed) using thresholds: ≥20 transcripts, ≥15 unique genes, negative probe ratio <5%
Panel: 313 genes; median 164 transcripts/cell, 64 genes/cell, 0 negative probes/cell

Preprocessing

Log-normalisation and variable feature selection (VST method)
Data sketching (LeverageScore, 75,000 cells) for scalable dimensionality reduction

Clustering

PCA (50 PCs), Louvain algorithm (resolution 0.8) → 32 clusters
UMAP visualisation; clusters projected back to full dataset using ProjectData

Cell Type Annotation

Differential expression per cluster (FindAllMarkers; Wilcoxon test; log2FC ≥ log2(1.5), p_adj ≤ 0.05)
Cluster markers intersected with literature-based cell type marker sets → 15 cell types annotated
Top 3 most abundant: Glandular cells, T cells, Fibroblasts

Spatial Proximity Analysis

KNN distance (FNN) calculated between each myoepithelial cell and the nearest cell of every other type
Wilcoxon rank-sum test to assess whether myoepithelial cells are significantly closer to glandular cells than to other populations
Visualised using ImageDimPlot with cell segmentation boundaries


Key Results

161,789 cells retained after QC across a 313-gene targeted panel
32 clusters identified; annotated to 15 cell types
Glandular cells, T cells, and Fibroblasts are the three most abundant populations
Myoepithelial cells are significantly closer to Glandular cells (median 13.39 µm) than to any other cell type; second nearest were Fibroblasts (24.07 µm)
Wilcoxon test confirms the spatial association is statistically significant
Findings are consistent with the known role of myoepithelial cells as a protective monolayer around ductal structures

Repository Contents
Xenium-DCIS-analysis.html — Full analysis including all code, outputs, and spatial figures.

Reference
Janesick A et al. High resolution mapping of the tumor microenvironment using integrated single-cell, spatial and in situ analysis. Nature Communications. 2023;14:8353.

GitHub: github.com/parulkuls26# placeholder
