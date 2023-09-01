# Introduction
Alternative splicing is one of the most complicated cellular processes in which exons from the same gene are joined or skipped in different combinations, leading to different, but related, mRNA transcripts or isoforms. Isoform diversity has been shown to affect phenotypes at the molecular and ultimately organismal level. These mRNA isoforms can be translated to produce various proteins with distinct structures and functions — all from a single gene. Many diseases, like cancer and neurodegenerative disorders, are caused by changes in isoform profiles. For instance, Huang et al, 2021 found novel isoforms and the usage of alternate promoters in cell lines and subtypes of gastric cancer and Lerch et at, 2012 were able to characterize isoform repertoire for injured vs. non-injured neuronal cell types.
Next Generation Sequencing (NGS), especially NGS of the transcriptome (RNA-Seq), including short read and long read sequencing, characterizes the gene expression at the isoform level in different cell types at various conditions and sheds light on biological processes inside the cells and how cells responding to the macro- and micro-environment. However, short-read sequencing is limited and prevents figuring of the high-confidence inference of alternative splicing, novel exons, and junction sites and the characterization of complete isoforms. On the other hand, long-read sequencing promises to overcome the inherent limitations of short-reads. Analysis of long-read sequence data using multiple variants calling algorithms detecting insertion, deletion, inversion, and duplication found nearly 2.5 times more structural variants (SV)s than short-read data, of which ~83% of insertions were missed (Chaisson et al, 2019). The advent of recent long-read sequencing technologies like PacBio high-fidelity (HiFi) sequencing and Oxford Nanopore sequencing have plummeted error rates and enabled high-quality full-length reads that cover entire isoforms, removing any uncertainty in determining exon composition.
There are some existing tools that compare sets of transcript annotations including gffcompare (Partea, 2020) and AGAT (Dainat) agat_sp_compare_two_annotations. To our knowledge, no tool currently exists that takes advantage of the sequence data itself when comparing inferred isoforms from long-read RNA sequencing data. In our case, we utilize HiFi data which provides both full-length isoforms and highly accurate base calls, to identify novel and potentially causal differences in isoform expression between individuals. This IsoComp tool we develop here can be used to make comparisons among more than one sample, e.g. trio, or cancer subtype cell lines, etc. The design purpose of this tool is to compare a query annotation set against a reference, and it is limited, as the name implies, to comparing two annotations or more sets at a time.

---


# Motivation

The purpose of this document is to describe the diversity of isoforms with 
otherwise exact start/end points

## File specification, same isoforms found

### Columns

**1. ref_sample**

Name of the reference sample. This must be known based on how the bedtools 
intersect file was created

**2. ref_isoform**

Name of the reference isoform. This is the fourth column from the bedtools 
intersect output

**3. query_sample**

Name of the query sample. This is the seventh column of the bedtols intersect 
output

**4. query_isoform**

Name of the query isoform. This is column 11

**4. tx_genomic_length**

end-start

**5. edit_distance**

edit distance between query and ref isoform strings

**6. normalized_edit_distance**

`edit_distance / tx_genomic_length`

**7. cigar**

The cigar string of the alignment between the query and the ref
