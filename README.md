# Scripts and data from Griffiths, J.S. et al. (2019) Differential responses to ocean acidification between populations of *Balanophyllia elegans* corals from high and low upwelling environments. Mol. Ecol. DOI: 10.1111/mec.15050

## Physiological Analysis

*Script*: Respiration_analysis.R

*Input files*: Resp_all_data.csv, Resp_day9_data.csv, Resp_day29_data.csv

*Description*: Script contains code for normalizing respiration data and performing an ANOVA and a Tukey’s post-hoc test


*Script*: lipid_protein_ananlysis.R

*Input files*: lipid_protein_data.csv

*Description*: Script contains code for normalizing lipid and protein data and performing an ANOVA



## Post OrthoFinder Cleaning

*Script*: find_genes_both_pop_from_ortho.py, find_orphans_from_orthogroups.py, Count_orthos.py, get_1stgene_from_orthos.py, 

*Input files*: OrthoGroup.txt, RSEM_merged_matrix for each population (files were too large for GitHub so they are located on Dryad: https://doi.org/10.5061/dryad.8pg7963)

*Output files*: Orthoblast_RSEM_merged_matrix

*Description*: After using OrthoFinder to merge orthologous contigs between two assembled population-specific transcriptomes, we want to remove all OrthoGroups with a single contig from one population, but not the other population, which also did not get further sorted into other OrthoGroups via an independent blast search (identified via script find_orphans_from_orthogroups.py), were removed from the final consensus transcriptome (via script find_genes_both_pop_from_ortho.py). Now the script Count_orthos.py will use the RSEM count matrix to create an OrthoFinder RSEM matrix by summing counts for all contigs in an OrthoGroup. RSEM count matrix will now contain counts on an OrthoGroup level rather than the contig level. OrthoGroups now contain shared contigs between the two populations, which makes differentially expressed gene analysis for treatment conditions possible. The script get_1stgene_from_orthos.py will retreive the first gene found in each OrthoGroup (in OrthoGroup.txt file) so that Interproscan results for each gene can be matched up with its corresponding OrthoGroup.



## Differentially Expressed Gene Analysis

*Script*: DeSeq2.R

*Input files*: Orthoblast_RSEM_merged_matrix, column_2transcriptomes.txt

*Output files*: output_DEG_GOLtp1.txt, output_DEG_GOLtp2.txt, output_DEG_PACtp1.txt, output_DEG_PACtp2.txt

*Description*: Script contains analysis using DeSeq2. The merged matrix file contains the total counts of contains for each “Orthogroup”. The column file gives an explanation for the headers in the matrix file (the treatment conditions and population names for each read file. Output files contain the pvalues for log fold changes in Orthogroups in response to pH for each population timepoint (day 9 and 29).



## Functional Enrichment Analysis

*Script*: Please see scripts and explanations located at: https://github.com/z0on/GO_MWU\

*Input files*: Orthoblast_interproresults_nonredun.csv, pvalue_GOL_tp1, pvalue_GOL_tp2, pvalue_PAC_tp1, pvalue_PAC_tp2

*Output files*: BP_pvalue_GOL_tp1, BP_pvalue_GOL_tp2, BP_pvalue_PAC_tp1, BP_pvalue_PAC_tp2, MF_pvalue_GOL_tp1, MF_pvalue_GOL_tp2, MF_pvalue_PAC_tp1, MF_pvalue_PAC_tp2

*Description*: Script contains analysis for functional enrichment of logfold contig changes. The Orthoblast_interproresults_nonredun.csv input file contains the GO terms associated with each Orthogroup. The pvalue input files contain the signed logfold pvalues for expression changes derived from the DEG analysis using DeSeq2. Output files correspind to each input file name and whether the Biological Processes (BP) or Molecular Functions (MF) were analyzed.



## WGCNA Analysis

*Script*: WGCNA.R

*Input files*: Orthoblast_RSEM_merged_matrix (in the DESeq2 folder), PhenData_WGCNA

*Description*: Script contains analysis for WGCNA for day 29. The input file is the same for DESeq2 analysis (the merged matrix file contains the total counts of contains for each “Orthogroup” and the PhenData_WGCNA file gives an explanation for the headers in the matrix file (the treatment conditions, population names, and physiological data associated with each sample).



## PCoA Analysis

*Script*: PCoA.R

*Input files*: Orthoblast_RSEM_merged_matrix (in the DESeq2 folder), column_for_PCA_tp2.txt, column_for_PCA_tp1.txt, column_for_PCA_all_v3.txt

*Description*: Script contains analysis for PCoA analysis transcriptomic data. The input file is the same for DESeq2 analysis (the merged matrix file contains the total counts of contains for each “Orthogroup” and the column files gives an explanation for the headers in the matrix file (the treatment conditions and population names associated with each sample).



## DAPC Analysis

*Script*: DAPC.R

*Input files*: Orthoblast_RSEM_merged_matrix (in the DESeq2 folder), PhenData_WGCNA (in the WGCNA folder)

*Description*: Script contains analysis for DAPC analysis for day 29 and plotting results onto physiological PCA. The input file is the same for DESeq2 analysis (the merged matrix file contains the total counts of contains for each “Orthogroup” and the PhenData_WGCNA file gives an explanation for the headers in the matrix file (the treatment conditions, population names, and physiological data associated with each sample).
