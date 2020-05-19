---
title: The index to evaluate gene expression in RNA-seq
author: Zijian Zhang
date: '2018-07-21'
slug: the-index-to-evaluate-gene-expression-in-rna-seq
categories:
  - R
tags:
  - Cancer
---
# Backgroud

One commen quesion is wether one certain gene is expresed in one cell line or tissue or organ in human or mouse. for wet lab, qPCR or antibody-based assays can be performed with commercial antibodies. if no antibody is available, How should we do and this data is indispensable.

# RPKM, FKPM and TPM

> RPKM (Reads Per Kilobase Million) or FPKM (Fragments Per Kilobase Million). However, TPM (Transcripts Per Kilobase Million) is now becoming quite popular.

> RPKM:
>1. Count up the total reads in a sample and divide that number by 1,000,000 – this is our “per million” scaling factor.
>2. Divide the read counts by the “per million” scaling factor. This normalizes for sequencing depth, giving you reads per million (RPM)
>3. Divide the RPM values by the length of the gene, in kilobases. This gives you RPKM.

>FPKM is very similar to RPKM. RPKM was made for single-end RNA-seq, where every read corresponded to a single fragment that was sequenced. FPKM was made for paired-end RNA-seq. With paired-end RNA-seq, two reads can correspond to a single fragment, or, if one read in the pair did not map, one read can correspond to a single fragment. The only difference between RPKM and FPKM is that FPKM takes into account that two reads can map to one fragment

>TPM is very similar to RPKM and FPKM. The only difference is the order of operations. Here’s how you calculate TPM:

>1. Divide the read counts by the length of each gene in kilobases. This gives you reads per kilobase (RPK).
>2. Count up all the RPK values in a sample and divide this number by 1,000,000. This is your “per million” scaling factor.
>3. Divide the RPK values by the “per million” scaling factor. This gives you TPM.

# Z-score

>The z-score gives you the numer of standard-deviations that a value is away from the mean of all the values in the same group (= same gene).

>A z-score of -3 for the gene X in sample A means that this value is 3 standard-deviations lower than the mean of the values for gene X in all the samples (A,B,C...).
When a gene is differentially expressen in two groups (like treated and control or disiesed and healthy), then the z-scores of samples will be (mostly) positive in one group and (mostly) negative in the other group.

>The z-score is a signal-to-noise ratio. Large absolute z-scores (=large positive or negative values) is therefore not a direct estimate of the effect (i.e. the strength of the differential expressioin).
The very same (larger absolute) z-score can have different meanings, and this depends on the noise:
>- with large noise: a very large effect
>- with some noise: a rather large effect
>- with only little noise: a rather small effect
>- with almost no noise: a tiny effect

>The problem for a biological interpretation is that "noise" is not only measurement noise. It is also connected to the "tightness" of the control of gene regulation. Genes that are not tightly controlled (so the expression may vary in a wider range) can be considerably induced or repressed and this would not be recognized by the z-scores. In contrast, genes that are tightly controlled may change the expression only very slighlty, without any biological impact, but they will get large absolute z-scores.