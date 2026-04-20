# PGRR: Pangenome Gene Reference Resource

The **Pangenome Gene Reference Resource (PGRR)** is a comprehensive pangenome of the _M. tuberculosis complex_ (MTBC), which spans all seven _M. tuberculosis_ lineages and is produced using a virtually error-free sequencing and de novo assembly approach. It encompasses the complete panorama of genetic variation across all genes present in _M. tuberculosis_ to provide an efficient tool for performing isolated gene alignments and for accessing gene-level information from the pangenome reference strains.

## Description of Files

pangenome.fasta.gz:
contains the biological sequences of all genes and their highly similar paralogs collected from 50 strains of _M. tuberculosis_ across all seven lineages

pangenome_BCCM_unique_only.fasta.gz:
subsetted version of pangenome.fasta.gz that contains only sequences that are unique to the BCCM strains

pangenome_H37Rv_only.fasta.gz:
subsetted version of pangenome.fasta.gz that contains only sequences belonging to the H37Rv reference genome

pangenome_no_BCCM.fasta.gz:
subsetted version of pangenome.fasta.gz that includes all sequences EXCEPT for those found in the BCCM strains

## Example Workflow

To use the PGRR, you can use any alignment tool such as Bowtie2 to align your query sequences to the PGRR fasta file:

```
# Unzip and index PGRR
gunzip pangenome.fasta.gz
bowtie2-build -f pangenome.fasta pgrr_reference

#Align paired sample to PGRR
bowtie2 --no-unal --very-sensitive-local -x pgrr_reference -1 sample_R1.fastq.gz -2 sample_R2.fastq.gz -S output.sam

# convert SAM file to BAM format and sort it for downstream analysis
samtools view -bS -u output.sam | samtools sort -n -o output.bam
```


## Citation

Poonam Chitale, Elissa Ocke, Aubrey R. Odom, Howard Fan, Alexander Henoch, Karla Vasco, Emily C. Fogarty, Courtney Grady, Alexander D. Lemenze, Pradeep Kumar, Shannon Manning, A. Murat Eren, W. Evan Johnson, and David Alland. Defining the Mycobacterium tuberculosis Pangenome and Suggestions for a New Composite Reference Sequence.
