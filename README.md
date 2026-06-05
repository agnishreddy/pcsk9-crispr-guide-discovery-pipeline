# PCSK9 CRISPR Guide RNA Discovery Pipeline


## Overview

This project presents a computational bioinformatics workflow for the identification and prioritization of candidate CRISPR-Cas9 guide RNAs (gRNAs) targeting the human PCSK9 gene. The primary objective is to demonstrate a reproducible approach for discovering potential genome editing targets within the PCSK9 locus, a clinically relevant gene involved in cholesterol metabolism and cardiovascular disease risk.

Mutations that reduce PCSK9 activity are known to lower circulating low-density lipoprotein cholesterol (LDL-C), making PCSK9 one of the most extensively studied targets for therapeutic genome editing. This project explores the initial computational stages of guide RNA discovery by identifying potential SpCas9 target sites within the genomic structure of PCSK9 and ranking candidates using sequence-based design criteria.

---

## Scientific Background

Proprotein Convertase Subtilisin/Kexin Type 9 (PCSK9) regulates the degradation of LDL receptors in the liver. Increased PCSK9 activity reduces LDL receptor abundance and elevates blood cholesterol levels, whereas reduced PCSK9 activity leads to enhanced LDL clearance and lower LDL cholesterol concentrations.

Because naturally occurring loss-of-function mutations in PCSK9 are associated with protection against cardiovascular disease, genome editing approaches targeting PCSK9 have emerged as a promising area of therapeutic research.

The goal of this project is not to develop a clinically validated therapeutic guide RNA, but rather to establish a transparent computational framework for identifying candidate CRISPR targets within the PCSK9 genomic locus.

---

## Project Objectives

The pipeline was designed to:

1. Retrieve the annotated human PCSK9 genomic locus directly from NCBI.
2. Parse genomic exon annotations from GenBank records.
3. Extract coding exon sequences for functional gene disruption analysis.
4. Identify SpCas9-compatible target sites containing NGG PAM motifs.
5. Filter candidate guides using established sequence-quality criteria.
6. Rank candidate guides using transparent heuristic scoring methods.
7. Export prioritized guide candidates for downstream validation.

---

## Methodology

### 1. Genomic Data Acquisition

The pipeline retrieves the human PCSK9 genomic RefSeq locus:

**Accession:** NG_009061.1

Data are downloaded directly from the NCBI Nucleotide database using Biopython's Entrez interface.

---

### 2. Exon Annotation Parsing

Rather than relying on manually defined genomic coordinates, exon features are extracted directly from GenBank annotations.

For this study:

* Exon 1 was identified from the genomic annotation record.
* The exon sequence was extracted programmatically.
* Candidate guides were restricted to biologically relevant coding regions.

This approach improves reproducibility and reduces manual annotation errors.

---

### 3. CRISPR Target Discovery

The extracted exon sequence was scanned for canonical SpCas9 PAM motifs:

PAM = NGG

For every PAM site detected:

* A 20-nucleotide protospacer sequence was extracted.
* Genomic coordinates were recorded.
* Strand orientation was retained.

Both forward and reverse-complement strands were evaluated.

---

### 4. Candidate Filtering

Guide sequences were filtered using common sequence-quality criteria:

#### GC Content

Acceptable range:

40–65%

This range is frequently used to avoid extremely low or extremely high GC content that may negatively affect guide performance.

#### Poly-T Exclusion

Sequences containing:

TTTT

were removed because poly-T motifs can terminate transcription when U6 promoters are used for guide RNA expression.

#### Homopolymer Filtering

Sequences containing long nucleotide runs were penalized to reduce the likelihood of synthesis and expression issues.

---

### 5. Candidate Ranking

Remaining candidates were ranked using a transparent heuristic scoring framework based on:

* GC balance
* Seed region composition
* Homopolymer content
* Sequence complexity

The ranking system was intended only for preliminary prioritization and should not be interpreted as a validated prediction of editing efficiency.

---

## Results

### Exon Identification

The pipeline successfully parsed the first annotated exon of the human PCSK9 locus:

* RefSeq Locus: NG_009061.1
* Exon Coordinates: 4929–5498
* Strand: Positive (+)
* Exon Length: 569 bp

### Guide Discovery

A total of 45 candidate SpCas9 guide RNAs passed all filtering criteria.

Each candidate satisfied:

* Acceptable GC content
* No poly-T termination motifs
* Acceptable sequence complexity
* Presence of a valid SpCas9 PAM site

### Top Candidate Characteristics

The highest-ranked guides demonstrated:

* GC content approximately 55%
* Balanced seed-region composition
* Absence of transcriptional termination motifs
* Low homopolymer complexity

These properties are generally considered favorable for further computational evaluation.

---

## Interpretation of Findings

The results demonstrate that multiple candidate CRISPR-Cas9 target sites exist within the first coding exon of the human PCSK9 gene.

The pipeline successfully identified and prioritized guide RNA candidates suitable for downstream analysis. However, the current study should be viewed as an initial guide-discovery and prioritization exercise rather than a therapeutic design platform.

No claims are made regarding:

* Clinical efficacy
* Therapeutic suitability
* Genome-wide specificity
* Experimental editing performance

Additional validation would be required before any candidate could be considered for laboratory testing.

---

## Current Limitations

This project intentionally focuses on the early stages of CRISPR guide discovery and does not yet include:

* Rule Set 3 on-target scoring
* CFD specificity scoring
* Cas-OFFinder genome-wide searches
* CRISPOR validation
* Chromatin accessibility analysis
* Conservation analysis
* Functional knockout prediction
* Experimental validation

Therefore, the identified guides should be regarded as computationally prioritized candidates only.

---

## Future Development

Planned future improvements include:

* Integration of validated Rule Set 3 efficiency models
* Genome-wide off-target analysis using CRISPR-specific tools
* CFD specificity calculations
* Functional exon-disruption assessment
* Comparative analysis against published PCSK9 guide RNAs
* Automated report generation
* Multi-gene therapeutic target support

---

## Conclusion

This project establishes a reproducible computational workflow for discovering candidate CRISPR-Cas9 guide RNAs within the human PCSK9 genomic locus. By combining direct NCBI genomic retrieval, annotation-aware exon parsing, PAM-site discovery, and sequence-quality filtering, the pipeline generates a prioritized set of guide candidates suitable for downstream validation.

The study demonstrates the feasibility of automated CRISPR target discovery using publicly available genomic resources while highlighting the additional analyses required before therapeutic applications can be considered.


**Disclaimer

This project is intended for educational and research purposes only.
The generated guide RNA candidates are computational predictions and
have not been experimentally validated. Results should not be used
for clinical, therapeutic, or laboratory decision-making without
appropriate validation and regulatory review.**
