# Clinical Pharmacogenetics of 2,000 Human Genomes — R Scripts

## Description

This repository contains R scripts I personally created and worked on during my internship in the [Laboratory of Computational Genomics](https://bosco-aosp.github.io/computational-genomics-platform/) at the [IRCCS Policlinico di Sant'Orsola - Azienda Ospedaliero Universitaria di Bologna](https://www.aosp.bo.it/), as part of my [MSc in Pharmaceutical Biotechnology at the University of Bologna](https://corsi.unibo.it/2cycle/PharmaceuticalBiotechnology).

The internship project focused on establishing pharmacogenomic variants across approximately 2,000 human genomes. The scripts cover several analytical steps, including genotype frequency computation, sequencing coverage assessment, and population stratification via machine learning methods (K-Nearest Neighbors and K-means clustering).

> **Note:** These are not the only scripts used during the internship. This repository only includes scripts that I personally wrote and developed; scripts produced by other team members are not shared here.

## Background

This project was inspired by the study published by [Shugg et al. (2024)](https://ascpt.onlinelibrary.wiley.com/doi/full/10.1002/cpt.3402) in [Clinical Pharmacology & Therapeutics](https://ascpt.onlinelibrary.wiley.com/journal/15326535):

> Shugg T, Tillman EM, Breman AM, et al. "Development of a Multifaceted Program for Pharmacogenetics Adoption at an Academic Medical Center: Practical Considerations and Lessons Learned." *Clin Pharmacol Ther.* 2024;116(4):914–931. doi: [10.1002/cpt.3402](https://doi.org/10.1002/cpt.3402)

The study details Indiana University's 2019 Precision Health Initiative for pharmacogenetics (PGx) implementation at university-affiliated practice sites, with the overarching goal of facilitating the sustainable adoption of genotype-guided prescribing into routine clinical care. Among other things, the study describes the extraction of PGx-relevant genotypes from genetic sequencing data available within the health system.

## Data Note

Clinical data and results are **not** included in this repository. Only scripts are shared, as the underlying data are subject to privacy and confidentiality constraints.

## Repository Contents

| Script | README | Description |
|--------------------|--------------------|--------------------------------|
| [`gt_freq.R`](gt_freq.R) | [`README_gt_freq.md`](README_gt_freq.md) | Computes per-variant genotype counts and frequencies across all individuals from the body of a gVCF file, with three output modes for handling non-standard genotype values |
| [`coverage_analysis_preprocessing.R`](coverage_analysis_preprocessing.R) | [`README_coverage_analysis_preprocessing.md`](README_coverage_analysis_preprocessing.md) | Prepares input files for a coverage assessment on exonic and genomic regions harboring pharmacogenetic variants within WES and WGS cohorts |
| [`coverage_analysis.R`](coverage_analysis.R) | [`README_coverage_analysis.md`](README_coverage_analysis.md) | Visualizes mean coverage distribution via heatmaps and determines how many samples fail to meet quality thresholds (\>30X for WES, \>20X for WGS) |
| [`knn.R`](knn.R) | [`README_knn.md`](README_knn.md) | Predicts superpopulation assignment using KNN with cross-validation via the `caret` package, including model retraining on the full dataset |
| [`knn_easy.R`](knn_easy.R) | [`README_knn_easy.md`](README_knn_easy.md) | Simplified version of `knn.R` using the `class` package for KNN classification, with manual hyperparameter tuning |
| [`kmeans.R`](kmeans.R) | [`README_kmeans.md`](README_kmeans.md) | Attempted superpopulation assignment via K-means clustering (\~80.7% accuracy vs \>99% with KNN — ultimately not the most appropriate method) |

## Dependencies

All packages used across the scripts are listed below.

| Package | Source | Used in |
|-------------------------|----------------------|-------------------------|
| [caret](https://topepo.github.io/caret/index.html) | CRAN | `knn.R` |
| [class](https://cran.r-project.org/package=class) | CRAN | `knn_easy.R` |
| [ggplot2](https://ggplot2.tidyverse.org/) | CRAN | `knn.R`, `knn_easy.R`, `kmeans.R` |
| [ComplexHeatmap](https://bioconductor.org/packages/ComplexHeatmap/) | Bioconductor | `coverage_analysis.R` |
| [circlize](https://cran.r-project.org/package=circlize) | CRAN | `coverage_analysis.R` |

> **Note:** `gt_freq.R` and `coverage_analysis_preprocessing.R` rely entirely on base R functions, requiring no additional packages. Similarly, `kmeans.R` uses the base R `kmeans()` function from the `stats` package.

### Installation

``` r
# CRAN packages
install.packages("caret")
install.packages("class")
install.packages("ggplot2")
install.packages("circlize")

# Bioconductor package
install.packages("BiocManager")
BiocManager::install("ComplexHeatmap")
```

## How to Run

Each script is designed to be self-contained. To run any script:

1.  Open the script in R/RStudio;
2.  Set the input and output file paths at the top of the script (each path is marked with a comment indicating it should be replaced);
3.  Run the script.

Refer to the individual README for each script for detailed information on input file formats, processing steps, and output files.

## Author

**Riccardo Guatteri**\
MSc in Pharmaceutical Biotechnology — [University of Bologna](https://www.unibo.it/)\
Internship at the [IRCCS Policlinico di Sant'Orsola](https://www.aosp.bo.it/) (Azienda Ospedaliero-Universitaria di Bologna)

## Contributing

Contributions, suggestions, and improvements are welcome. Feel free to open an issue or submit a pull request.

If you'd like to reach out, you can find me on [LinkedIn](https://www.linkedin.com/in/riccardo-guatteri/).

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
