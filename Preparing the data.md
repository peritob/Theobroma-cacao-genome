1. PacBio Sequel II ccs.bam file (23G) was downloaded on the 6 March 2023 and filtered of adaptors using HiFiAdapterFilt [https://github.com/sheinasim/HiFiAdapterFilt](url). Data available at NCBI accession: SRR28294702
2. We ran NanoPlot [https://github.com/wdecoster/NanoPlot](url) on filtered data to check statistics.
- Mean read length:                14,413.4
- Mean read quality:                   35.6
- Median read length:              14,243.0
- Median read quality:                 34.6
- Number of reads:              2,099,377.0
- Read length N50:                 15,791.0
- Total bases:             30,259,224,851.0

3. Phase Genomics HiC paired-end data (25G) was downloaded on the 15 March 2023. Raw data available at NCBI accession: SRR28294701.
4. We mapped the data to the _Ceratobasidium theobromae_ genome available on NCBI ([https://www.ncbi.nlm.nih.gov/search/all/?term=GCA_009078325.1_ASM907832v1_genomic.fna](url)) with minimap2/2.21-r1071 to separate plant from pathogen reads.

   
   `
   minimap2 -d ${prefix_name}.mmi ${prefix_name}.fasta
   `
   
   `
   minimap2 -K 2g -t 8 -ax map-hifi -o $OUTDIR/${prefix_name}.sam -a ${prefix_name}.mmi ccs.filt.fastq.gz
   `
5. Parental Illumina data was available from previous work within our lab in 2021,  and is available at NCBI accessions: SRR28294700 (maternal S1 raw data) and SRR28294699 (paternal RUQ1347 raw data).
