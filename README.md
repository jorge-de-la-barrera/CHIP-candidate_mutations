# Source code software used in
Díez-Díez, M., Ramos-Neble, B.L., de la Barrera, J. *et al*. Unidirectional association of clonal hematopoiesis with atherosclerosis development. *Nat Med* (2024). https://doi.org/10.1038/s41591-024-03213-1

## Build a masked version of GRCh38 reference genome
The U2AF1 gene is essential for mRNA splicing and is often mutated in hematopoietic cancers. However, updates in the GRCh38 human reference genome hinder the detection of these mutations by variant calling pipelines as described in [Failure to Detect Mutations in U2AF1 due to Changes in the GRCh38 Reference Sequence](https://doi.org/10.1016/j.jmoldx.2021.10.013).

Based on the instructions detailed in that paper, we built a masked version of GRCh38:

1.- [Get GATK Resource Bundle for GRCh38](https://gatk.broadinstitute.org/hc/en-us/articles/360035890811-Resource-bundle)

2.- [Get regions to be masked from NCBI](https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/001/405/GCA_000001405.15_GRCh38/seqs_for_alignment_pipelines.ucsc_ids/GCA_000001405.15_GRCh38_GRC_exclusions.bed)

3.- Use __bedtools maskfasta__ to mask the fasta file from the GATK Bundle using the .bed file with the regions to be masked

4.- Use __bwa index__ to make the BWA index files for the masked fasta file

## Variant Calling
The variant calling was performed by 2 WDL script:
- __variant_calling.wdl__: make the variant calling for a single-sample level
- __cohort_candidates.wdl__: make the variant calling at a cohort-level

## *Driver* cadidate mutations
A list of *__putative__* cadidate mutations were obtained using:
- __chip_parsing_crossectional.py__ : for a crossectional cohort (one time-point)
- __chip_parsing_longitudinal.py__ : for a longitudinal cohort

Above lists were manually curated using the criteria described in the paper to obtain the list of CH *driver* mutations.
