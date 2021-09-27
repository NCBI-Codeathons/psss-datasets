# Dataset

This repo contains information for metagenome datasets to be used in **Petabyte Scale Sequence Search: Metagenomics Benchmarking Codeathon** held on Sept. 27-Oct. 1. Included metagenomes are from three different environments (human gut, marine, and soil). Details of each dataset (e.g. SRR, SRX ids, etc. when available) and their location in GCP and AWS bucket can be found in `data.tsv`.

# Slides
Overview of the datasets for the codeathon are available here: https://tinyurl.com/PSSSslides

# Data processing
Raw files (*.sra) were obtained from sra using [`sratoolkit`](https://github.com/ncbi/sra-tools) with following command:

```
prefetch $SRR
```

Then `fastq-dump` was used for extracting the paired reads with following command:

```
fastq-dump --gzip --clip --read-filter pass --outdir $OUTDIR --skip-technical --split-3 $SRR.sra
```

And, then interleaved files with `1` and `2` attended at the end of the read names were generated using:

```
reformat.sh in1=$SRR_1.fastq.gz in2=$SRR_2.fastq.gz out=$SRR.interleaved.fq.gz addslash int
```
All the metagenome datasets were then processed using NMDC metagenome workflow (https://github.com/microbiomedata/metaG). 

## Output Folder
Folder names correspond to a NMDC specific id (For example `nmdc:mga00p32/`), within each folder there are specific subfolders (`qa`, `MAGs`, `ReadbasedAnalysis`, `annotation`, `assembly`) associated with analyses. Here is an example `tree` listing of all the files and folders for project id `nmdc:mga0ke75`.

```
.
|-- MAGs
|   |-- activity.json
|   |-- data_objects.json
|   |-- nmdc_mga0ke75_bins.lowDepth.fa
|   |-- nmdc_mga0ke75_bins.lowDepth.fa.md5
|   |-- nmdc_mga0ke75_bins.tooShort.fa
|   |-- nmdc_mga0ke75_bins.tooShort.fa.md5
|   |-- nmdc_mga0ke75_bins.unbinned.fa
|   |-- nmdc_mga0ke75_bins.unbinned.fa.md5
|   |-- nmdc_mga0ke75_checkm_qa.out
|   |-- nmdc_mga0ke75_checkm_qa.out.md5
|   |-- nmdc_mga0ke75_hqmq_bin.zip
|   |-- nmdc_mga0ke75_hqmq_bin.zip.md5
|   |-- nmdc_mga0ke75_metabat_bin.zip
|   `-- nmdc_mga0ke75_metabat_bin.zip.md5
|-- ReadbasedAnalysis
|   |-- activity.json
|   |-- data_objects.json
|   |-- nmdc_mga0ke75_centrifuge_classification.tsv
|   |-- nmdc_mga0ke75_centrifuge_classification.tsv.md5
|   |-- nmdc_mga0ke75_centrifuge_krona.html
|   |-- nmdc_mga0ke75_centrifuge_krona.html.md5
|   |-- nmdc_mga0ke75_centrifuge_report.tsv
|   |-- nmdc_mga0ke75_centrifuge_report.tsv.md5
|   |-- nmdc_mga0ke75_gottcha2_krona.html
|   |-- nmdc_mga0ke75_gottcha2_krona.html.md5
|   |-- nmdc_mga0ke75_gottcha2_report.tsv
|   |-- nmdc_mga0ke75_gottcha2_report.tsv.md5
|   |-- nmdc_mga0ke75_gottcha2_report_full.tsv
|   |-- nmdc_mga0ke75_gottcha2_report_full.tsv.md5
|   |-- nmdc_mga0ke75_kraken2_classification.tsv
|   |-- nmdc_mga0ke75_kraken2_classification.tsv.md5
|   |-- nmdc_mga0ke75_kraken2_krona.html
|   |-- nmdc_mga0ke75_kraken2_krona.html.md5
|   |-- nmdc_mga0ke75_kraken2_report.tsv
|   `-- nmdc_mga0ke75_kraken2_report.tsv.md5
|-- activity.json
|-- annotation
|   |-- activity.json
|   |-- annotations.json
|   |-- data_objects.json
|   |-- features.json
|   |-- nmdc_mga0ke75_cath_funfam.gff
|   |-- nmdc_mga0ke75_cath_funfam.gff.md5
|   |-- nmdc_mga0ke75_cog.gff
|   |-- nmdc_mga0ke75_cog.gff.md5
|   |-- nmdc_mga0ke75_ec.tsv
|   |-- nmdc_mga0ke75_ec.tsv.md5
|   |-- nmdc_mga0ke75_functional_annotation.gff
|   |-- nmdc_mga0ke75_functional_annotation.gff.md5
|   |-- nmdc_mga0ke75_ko.tsv
|   |-- nmdc_mga0ke75_ko.tsv.md5
|   |-- nmdc_mga0ke75_ko_ec.gff
|   |-- nmdc_mga0ke75_ko_ec.gff.md5
|   |-- nmdc_mga0ke75_pfam.gff
|   |-- nmdc_mga0ke75_pfam.gff.md5
|   |-- nmdc_mga0ke75_proteins.faa
|   |-- nmdc_mga0ke75_proteins.faa.md5
|   |-- nmdc_mga0ke75_smart.gff
|   |-- nmdc_mga0ke75_smart.gff.md5
|   |-- nmdc_mga0ke75_stats.json
|   |-- nmdc_mga0ke75_stats.tsv
|   |-- nmdc_mga0ke75_structural_annotation.gff
|   |-- nmdc_mga0ke75_structural_annotation.gff.md5
|   |-- nmdc_mga0ke75_supfam.gff
|   |-- nmdc_mga0ke75_supfam.gff.md5
|   |-- nmdc_mga0ke75_tigrfam.gff
|   `-- nmdc_mga0ke75_tigrfam.gff.md5
|-- assembly
|   |-- activity.json
|   |-- data_objects.json
|   |-- nmdc_mga0ke75_assembly.agp
|   |-- nmdc_mga0ke75_assembly.agp.md5
|   |-- nmdc_mga0ke75_contigs.fna
|   |-- nmdc_mga0ke75_contigs.fna.md5
|   |-- nmdc_mga0ke75_covstats.txt
|   |-- nmdc_mga0ke75_covstats.txt.md5
|   |-- nmdc_mga0ke75_pairedMapped.sam.gz
|   |-- nmdc_mga0ke75_pairedMapped_sorted.bam
|   |-- nmdc_mga0ke75_pairedMapped_sorted.bam.md5
|   |-- nmdc_mga0ke75_scaffolds.fna
|   |-- nmdc_mga0ke75_scaffolds.fna.md5
|   `-- nmdc_mga0ke75_stats.json
`-- qa
    |-- activity.json
    |-- data_objects.json
    |-- nmdc_mga0ke75_filterStats.txt
    |-- nmdc_mga0ke75_filterStats.txt.md5
    |-- nmdc_mga0ke75_filterStats2.txt
    |-- nmdc_mga0ke75_filtered.fastq.gz
    `-- nmdc_mga0ke75_filtered.fastq.gz.md5

```






