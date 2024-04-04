## _Theobroma cacao_ (clone 26) genome - preparing the data
These are the steps to assemble and annotate the diploid _Theobroma cacao_ genome.

The cacao plant is growing at the MARS research station at Pangkep, South Sulawesi. Leaf samples were taken from a  vascular streak dieback (VSD) symptomatic individual infected with _Ceratobasidium theobromae_, in January 2023. This plant (clone 26) is an F1 hybrid cross from S1 (maternal) x RUQ1347 (paternal). Peri Tobias and Jacob Downs collected the material in person and extracted the HMW DNA at the UNHAS plant pathology laboratory in Makassar, with Eirene Brugman. Cross-linking was done on infected leaf material and samples sent to Phase Genomics for HiC libraries and sequencing. HMW DNA was couriered to AGRF in Brisbane, Australia (arrived 27 January 2023) for HiFi sequencing. While the original intent of this research was to assemble the complete genomes of both the biotrophic pathogen and the host, we did not obtain enough sequence data to build the pathogen genome. We proceeded with the cacao tree genome of known parental cross, permitting the assigning of chromosomes as maternal and paternal.

1. PacBio Sequel II ccs.bam file (23G) was downloaded on the 6 March 2023 and filtered of adaptors using HiFiAdapterFilt [https://github.com/sheinasim/HiFiAdapterFilt](url)
2. We ran NanoPlot [https://github.com/wdecoster/NanoPlot](url) on filtered data to check statistics.
- Mean read length:                14,413.4
- Mean read quality:                   35.6
- Median read length:              14,243.0
- Median read quality:                 34.6
- Number of reads:              2,099,377.0
- Read length N50:                 15,791.0
- Total bases:             30,259,224,851.0

3. Phase Genomics HiC paired-end data (25G) was downloaded on the 15 March 2023.
4. We mapped the data to the _Ceratobasidium theobromae_ genome available on NCBI ([https://www.ncbi.nlm.nih.gov/search/all/?term=GCA_009078325.1_ASM907832v1_genomic.fna](url)) with minimap2/2.21-r1071 to separate plant from pathogen reads.
   
   `
   minimap2 -d ${prefix_name}.mmi ${prefix_name}.fasta
   `
   
   `
   minimap2 -K 2g -t 8 -ax map-hifi -o $OUTDIR/${prefix_name}.sam -a ${prefix_name}.mmi ccs.filt.fastq.gz
   `
