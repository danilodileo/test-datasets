# Modules Test Data

This branch of the `nf-core/test-datasets` repository contains all data used for the individual module tests.
There are two main directories: `genomics` and `delete_me`. The former contains all datasets for genomics tools while the latter contains temporary datasets that will be deleted as better data gets available.

### delete_me
The `delete_me` folder does not adhere to a defined structure as data in this folder should be directly as fast as possible, whenever a more suitable dataset is found that can be added to the `genomics` folder.

### genomics
The genomics folder contains subfolders for all organisms for which test data is available. At the moment, there are twor organisms available:
    * homo_sapiens
    * sarscov2

The two folders are structured in a similar way, with any genome-specific files in `genome` (e.g. fasta, gtf, ...) and technology specific raw-data files
in the `illumina` and `nanopore` subfolders.
It is currently organised in `genomics` and `generic`. The former contains all typical data required for genomics modules, such as fasta, fastq and bam files. Every folder in `genomics` corresponds to a single organisms. Any other data is stored in `generic`. This contains files that currently cannot be associated to a genomics category, but also depreciated files which will be removed in the future and exchanged by files in `genomics`. For every data file, a short description about how this file was generated is available either in this description or in the respective subfolder.

If you cannot find suitable test data on this repository, please contact us on the [nf-core Slack `#modules` channel](https://nfcore.slack.com/channels/modules) (you can join with [this invite](https://nf-co.re/join/slack)). The goal is to create a suitable, small test dataset that should be usable with the available test data and if possible be generated with modules available from `nf-core/modules`. If creating that test data is difficult but you want to add the module first, it is also possible to add a small subset to the `delete_me` folder to get your module tests running, and then add proper test data afterwards. This should be discussed on slack. In order to add test data. For a short description of the workflow for adding new data, have a look at [here](docs/ADD_NEW_DATA)
## Data Description

### genomics

* sarscov2
    * alignment
        * 'all_sites.fas'
        * 'informative_sites.fas'
    * bed
        * 'test.bed': exemplary bed file for the MT192765.1 genome (fasta/test_genomic.fasta)
        * 'test2.bed': slightly modified copy of the above file
        * 'test.bed.gz': gzipped version
        * 'baits.bed'
        * 'test.bed12'
    * db
        * 'kraken2': kraken2 DB
        * 'kraken2.tar.gz': kraken2 DB archive
    * genome
        * 'genome.fasta': MT192765.1 genomem including (GCA_011545545.1_ASM1154554v1)
        * 'genome.dict': GATK dict for 'genome.fasta'
        * 'genome.fasta.fai': fasta index for 'genome.fasta'
        * 'transcriptome.fasta': coding sequencing from MT192765.1 genome (transcripts)
        * 'transcriptome.paf': PAF file for MT192765.1  genome
        * 'genome.gtf': GTF for MT192765.1 genome
        * 'genome.gff3': GFF for MT192765.1 genome
        * 'genome.gff3.gz': bgzipped-version
        * 'genome.sizes': genome size for the MT192765.1 genome

    * illumina
        * bam
            * 'test_{,methylated}_paired_end.bam': sarscov2 sequencing reads aligned against test_genomic.fasta using minimap2
            * 'test_{,methylated}_paired_end.sorted.bam': sorted version of the above bam file
            * 'test_{,methylated}_paired_end.bam.sorted.bam.bai': bam index for the sorted bam file
            * 'test_single_end.bam': alignment (unsorted) of the 'test_1.fastq.gz' reads against test_genomic.fasta using minimap2
            * 'test_unaligned.bam': unmapped BAM file created from 'test_1.fastq.gz' using GATK4 SamToFastq
        * bedgraph
            * 'test.bedgraph'
        * bigwig
            * 'test.bw'
        * deeptools
            * 'test.computeMatrix.mat.gz': matrix generated with deeptools computeMatrix using 'test.bw'
        * fasta
            * 'contigs.fasta': sarscov2 contigs obtained running SPAdes `--rnaviral`on sample1 of the [nf-core/viralrecon tests-dataset](https://github.com/nf-core/test-datasets/tree/viralrecon/illumina/amplicon)
            * 'scaffolds.fasta': sarscov2 scaffolds obtained running SPAdes `--rnaviral`on sample1 of the [nf-core/viralrecon test-dataset](https://github.com/nf-core/test-datasets/tree/viralrecon/illumina/amplicon)
        * fastq
            * 'test_{1,2}.fastq.gz' sarscov2 paired-end sequencing reads
            * 'test_{1,2}.2.fastq.gz‘: copies of the above reads
            * 'test_methylated_{1,2}.fastq.gz' sarscov2 paired-end bisulfite sequencing reads (generated with [Sherman](https://github.com/FelixKrueger/Sherman))
        * gatk
            * 'test.baserecalibrator.table': Recalibration table generated with gatk4 BaseRecalibrator from 'test_paired_end.sorted.bam', using 'test.vcf.gz' as known sites.
        * vcf
            * 'test.vcf', 'test2.vcf': generated from 'test_paired_end.sorted.bam' using bcftools mpileup, call and filter
            * 'test3.vcf': generated from 'test_single_end.sorted.bam' using bcftools mpileup, call and filter
            * '*.gz': generated from VCF files using bgzip
            * '.tbi': generated from '.vcf.gz' files using `tabix -p vcf -f <file>`
        * wig
            * 'test.wig.gz'
    * nanopore
        * bam
            * 'test.sorted.bam'
            * 'test.sorted.bam.bai'
        * fast5
            * '100read_fast5'
        * fastq
            * 'test.fastq.gz'
        * sequencing_summary
            * 'test.sequencing_summary.txt'


* homo_sapiens
    * genome
        * dbsnp: DBSnp file downsampled based on reference position
        * dict: Sequence dictionary corresponding to `fasta`
        * fasta: Reference fasta based on chr22:16570000-16610000
        * gff3: Encode GFF3 file downsampled based on reference position
        * gtf: Encode GTF file downsampled based on reference position
        * sizes:
        * gnomAD: gnomAD file downsampled based on reference position
        * mills_and_1000G: Indels file downsampled based on reference position
        * .bed
    * illumina
        * bam:
            * test.sorted: Mapped, and sorted reads based on `test_{,umi}_{1,2}` (normal)
            * test2.sorted: Mapped, and sorted reads based on `test2_{,umi}_{1,2}` (tumor)
            * test_markduplicates: Mapped, sorted, and duplicate marked reads based on `test_{,umi}_{1,2}` (normal)
            * test2_markduplicates: Mapped, sorted, and duplicate marked reads based on `test2_{,umi}_{1,2}` (tumor)
            * test_recalibrated: Mapped, sorted, duplicate marked, and recalibrated reads based on `test_{,umi}_{1,2}` (normal)
            * test2_recalibrated: Mapped, sorted, duplicate marked, and recalibrated reads based on `test2_{,umi}_{1,2}` (tumor)

            * UMI:
                * test_umi: Files base on  `test_umi_{1,2}` (normal)
                * test2_umi: Files base on  `test2_umi_{1,2}` (tumor)
        * fastq:
            * test_{1,2}: reads corresponding to normal sample
            * test_umi_{1,2}: UMI tagged reads corresponding to normal sample
            * test2_{1,2}: reads corresponding to tumor sample
            * test2_umi_{1,2}: UMI tagged reads corresponding to tumor sample
        * gatk:
            * test: Recalibration table corresponding to `test_{,umi}_{1,2}` (normal) reads
            * test2: Recalibration table corresponding to `test2_{,umi}_{1,2}` (tumor) reads
        * gvcf:
            * test: Genome vcf corresponding to `test_{,umi}_{1,2}` (normal) reads
            * test2: Genome vcf corresponding to `test2_{,umi}_{1,2}` (tumor) reads