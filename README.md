# Enveda's private fork of ABsolute Immune Signal (ABIS) deconvolution

This Shiny app performs absolute deconvolution on RNA-Seq and microarray data. It also contain a Gene Viewer page where the expression of a gene can be visualized across 29 immune cell types.

---
## INSTALLATION

*You can run the apps in several ways:*

### Run it on the web!

This shiny app is hosted online at the https://giannimonaco.shinyapps.io/ABIS/. It does not need R installation and it can be immediately used by just clicking on the link. It only allows the upload of files no bigger than 5 MB.

We suggest using ABIS from the web only for testing. For larger analysis we encourage to install the shiny app locally.

### Run it locally without installation

You need to download the app from GitHub through R and it will run locally. However, as soon as you will close R, the app will not be available anymore and you need it to download it again.
All the packages and dependencies have to be installed first.

install.packages(c("shiny", "MASS", "preprocessCore"), dependencies = TRUE)

shiny::runGitHub("ABIS", user="giannimonaco")

### Run it locally with installation

Save the repository on your local machine. Open either the ui.R or the server.R file with RStudio, then click on "Run App".


---
## ABSOLUTE DECONVOLUTION
 
The gene expression matrix of your PBMC samples must be in a Tab delimited format. The gene names must be gene symbols and there should not be duplicates. Check the file TPMPBMC.txt in the folder data if you are looking for an example. Also, remember that quotes are not necessary.

### RNA-Seq deconvolution
For RNA-Seq deconvolution the gene expression values must be TPM values. 
RNA-Seq deconvolution has been implemented using data from Illumina HiSeq 2000. 

### Microarray deconvolution
For microarray deconvolution, the expression values should derive from the selection of the maximum expression value from the probes encoding for a single gene.
Microarray deconvolution has been implemented using data from Illumina HT-12 v4.

Please, be aware that platform and pre-processing specific effects can occur.  

### Output
The output values should be percentages of immune cell type, hence within the range of 0-100. Hence, if you use PBMC data, when you sum the scores for each sample, you should ideally get a value close to 100. 
Note also that the method used is without constraints, hence it is likely that you will obtain negative values. In this case you can consider one of these two situations:
 - **Negative values close to zero** -- they are likely due to technical or biological variability. Simply set them to zero or scale all the values up so that the minimum value is zero.
 - **Very low negative values** -- there might be strong biological or technical variability for the cell type with such values. Exclude the cell type from the analisys.

 
---
## GENE VIEWER
 
The Gene Viewer panel shows the median gene expression value of a gene accross the 29 immune cell types contained in our dataset. It is straitforward to use, simply enter the name of a gene in one of these formats: gene symbol, Ensembl ID or Entrez ID.

You could also use a standalone-html gene viewer which is available from: https://doi.org/10.5281/zenodo.2649355.

---
This software is  released under the GPL v2 license, "which guarantees end users (individuals, organizations, companies) the freedoms to use, study, share (copy), and modify the software".
