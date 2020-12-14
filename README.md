# bigleaf_maple_SNPs
R Scripts and data from bigleaf maple range-wide SNP genetic marker survey

Range-wide assessment of a SNP panel for individualization and geolocalization of bigleaf maple 
===============================================================================================
Rich Cronn and Kristen Finch - December 2020


This repository contains the code and data used to analyze Bigleaf Maple (*Acer macrophyllum* 
Pursh,or *ACMA*) genetic data associated with the manuscript:

Cronn R, Finch KN, Hauck LL, Parker-Forney M, Milligan B, Dowling J, & Adventure Scientists (2020).    
Range-wide assessment of a SNP panel for individualization and geolocalization of bigleaf maple 
(*Acer macrophyllum* Pursh). Forensic Sci Int. Submitted.

We used the Agena MassARRAY SNP assay described by Jardine et al. 
(https://link.springer.com/article/10.1007/s12686-015-0486-7) to analyze 133 SNPs from 1195 unique 
ACMA samples in 1344 separate genotyping reactions. The analysis includes replication tests on 
controls, as well as 'population' samples from across the range of *ACMA* (California, USA to 
British Columbia, CAN).

This repository contains five files, including three R/Markdown files and two data files:

    File 1: MapleAnalysis_controls_20201201.Rmd. 
    This script:
	+ Reads mass array genotype sample metadata and defines individuals and populations.
	+ Identifies and removes samples (genotypes) that exceed a 'missing data' threshold 
		(10% in this analysis).
	+ Identifies and removes SNPs (loci) that exceed a 'missing data' threshold (10% in 
		this analysis).
	+ Evaluates the association between Call Rate and input DNA mass, Tissue, and MassARRAY
		run date.
	+ Evaluates the association between Call Rate and latitude of origin, ecoregion of origin,
		and state/province of origin.
	+ Clusters genotypes with 'alleleMatch' so that genotyping error can be identified in the
		resulting outputs (*html or *csv). 
	+ Saves the dataset in a format that can be read by file 3, Random Forest Analysis.

 
    File 2: MapleAnalysis_populations_20201201.Rmd. 
    This script:
	+ Reads mass array genotype sample metadata, defines individuals and populations, and 
		makes maps.
	+ Identifies and removes samples (genotypes) that exceed a 'missing data' threshold 
		(10% in this analysis).
	+ Identifies and removes SNPs (loci) that exceed a 'missing data' threshold (10% in 
		this analysis).
	+ Identifies loci that violate assumptions of Hardy-Weinburg equilibrium.
	+ Calculates and plots minor allele freqencies.
	+ Calculates and plots expected and observed per-locus heterozygosity globally, and 
		examines relationship between heterozygosity and Level 3 Ecoregion source.
	+ Examines overall and pairwise population differentiation, as Fst.
	+ Removes loci known to exhibit poor assay behavior or linkage disequilibrium (LD was 
		estimated separately using `Genepop/R`).
	+ Calculates genotype probabilities for each genotype, globally and by population.
	+ Uses Discriminant Analysis of Principle Components to identify genetic 'clusters'.


    File 3: MapleAnalysis_randomforest_20201201.Rmd. 
    This script:
	+ Reads mass array genotype data output from File 1.
	+ Uses Random Forests to produce 5,000 models to predict the Level 3 Ecoregion source
		for each sample, and a distribution of all samples across all models.
	+ Uses Random Forests to produce 5,000 random Level 3 Ecoregion source predictions.
	+ Calculates summaries of observed and randomized predicted errors. 


    File 4: MapleSNP_20201201_1344i133s_adegenet.csv.
    This is a diploid genotype data file, and it includes all samples and metadata describing
	the source and tests run. This is the input for Files 1 and 2.

    File 5: Maple_LE.tsv.
    This is output file from genepop summarizing linkage disequilibrium for all pairs of SNP 
	markers for all populations. Markers showing a value of '0.05' are in significant 
	disequilibrium (P<=0.05, after Benjamini and Hochberg false-discovery rate correction)
	and should be removed from population analysis. Markers showing a value of 1 are in 
	linkage equilibrium if markers noted as '0.05' are removed from the analysis.


If you have any suggestions on improving this analysis, please send a message to the contact 
emails provided in our ORCID ID’s (Cronn, https://orcid.org/0000-0001-5342-3494; 
Finch, https://orcid.org/0000-0003-2098-7546).

