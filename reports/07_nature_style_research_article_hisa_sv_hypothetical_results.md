# A hierarchical annotation-guided ACAT framework for structural-variant set-based association testing in cardiometabolic traits

## Abstract
Structural-variant (SV) association testing remains statistically challenging because many SVs are rare, multi-mapped to functional units, and difficult to model with correlation-aware methods at scale. We developed **HiSA-SV** (Hierarchical Set-based Annotation test for SVs), a summary-statistic framework that performs SV set-based testing using hierarchical functional annotation and Aggregated Cauchy Association Testing (ACAT), without explicit LD modeling. HiSA-SV uses three functional layers (exon, intron, intergenic) and supports one-to-many SV-to-gene mapping under a 1-bp overlap rule. We drafted and stress-tested this framework in a UK Biobank whole-genome sequencing (WGS) setting (hg38) for a quantitative cardiometabolic trait (Non-HDL-C), with DEL/DUP/INS events parsed from standardized SV tokens. 

In a **hypothetical analysis scenario for manuscript drafting** (no real execution claimed in this document), HiSA-SV controlled type I error in null simulations, showed power gains over burden and min-p baselines under sparse causal architectures, and yielded interpretable gene-level association decomposition through annotation layers. Under assumed UKB-like sample size and allele-frequency structure, ACAT-based hierarchical aggregation prioritized biologically plausible loci while remaining robust to mixed SV labels (AGGREGATED/BREAKPOINT/COVERAGE) after pre-specified deduplication rules. These results support hierarchical ACAT as an extensible strategy for SV summary-based gene discovery and downstream multi-omic integration.

---

## Main

### Introduction
Despite rapid growth of whole-genome sequencing in population cohorts, SV association remains less mature than SNP-based analysis. The gap is methodological as much as technological. First, single-SV tests are often underpowered for rare variants. Second, SV consequences are structurally heterogeneous: one deletion or duplication can overlap exons, introns, and distal regulatory space simultaneously. Third, many set tests either collapse signal too aggressively or require dependence modeling that is brittle for sparse SV matrices and mixed representations.

For practical SV summary workflows, a p-value combination strategy is attractive because it can be modular, scalable, and independent of explicit LD matrix estimation. ACAT is particularly suitable for sparse-signal settings and heavy-tailed p-value distributions. However, flat ACAT aggregation ignores biological hierarchy and can dilute coherent substructure.

We therefore designed **HiSA-SV**, a hierarchical set-based framework that combines SV p-values across nested annotation levels and can be extended to consequence severity, cell-state priors, and pathway modules. Here we present a Nature-portfolio-style research article draft using a UKB-oriented analysis design and hypothetical results for protocol-finalization and manuscript architecture.

---

### Results

> **Important note:** All numerical findings in this Results section are **hypothetical draft values** created to structure the manuscript before real analysis. They must be replaced by actual outputs in the final submission.

### Cohort-scale SV summary landscape and preprocessing assumptions
Using an assumed UKB WGS summary structure (hg38), SV records were parsed from effect-allele tokens to obtain SV type (DEL/INS/DUP), event size, censoring flag (SVSIZE+), and evidence label (AGGREGATED/BREAKPOINT/BREAKPOINT1/BREAKPOINT2/COVERAGE). Under a representative draft scenario (N ≈ 330,000 for Non-HDL-C quantitative trait), we assumed ~1.8 million autosomal SV summary rows before set construction.

Hypothetical composition after QC-oriented filtering:
- DEL: 54.1%
- INS: 30.7%
- DUP: 15.2%
- AGGREGATED labels: 62.4%
- BREAKPOINT-family labels: 28.6%
- COVERAGE labels: 9.0%

As expected, the p-value distribution exhibited an extreme right tail in -log10 scale with underflow-prone near-zero p-values in a small fraction of records.

### Hierarchical annotation map construction
We applied a three-layer annotation system based on `hg38.refGene.gtf.gz`:
1. exon
2. intron (gene body minus exon)
3. intergenic

A 1-bp overlap rule was used, and one-to-many SV-to-gene mapping was allowed. In the hypothetical draft run, the mapping process produced:
- 28,278 genes represented
- median 19 SVs per gene-set (IQR 7–53)
- 12.8% of SVs mapped to >1 gene
- exon-priority assignment for exon+intron overlaps

### Calibration of hierarchical ACAT under null models
We evaluated HiSA-SV using synthetic null simulations matched to observed AF and SV-size distributions. At α = 0.05, 1e-3, and 2.5e-6, type I error remained close to nominal (all deviations <8% relative), with no substantial inflation under annotation overlap or mixed SV-label strata.

Hypothetical calibration summary:
- Genomic-control analogue at set-level: λ_set = 1.01
- QQ slope (middle quantiles): 1.00
- Tail stability improved after p-flooring (`p = max(p, 1e-300)`)

### Power benchmarking against baseline set tests
We compared HiSA-SV to weighted burden, min-p Bonferroni, and flat ACAT in synthetic architectures.

In sparse architecture (1–3 causal SVs per gene-set):
- HiSA-SV power: 0.71
- flat ACAT: 0.62
- min-p: 0.49
- burden: 0.44

In moderately polygenic architecture (8–15 weak causal SVs):
- HiSA-SV: 0.58
- flat ACAT: 0.56
- burden: 0.53
- min-p: 0.40

Performance gains were strongest when causal SVs were concentrated in exon or exon-proximal intron subsets, consistent with hierarchy-aware weighting.

### Hypothetical gene-level discoveries for Non-HDL-C
With an assumed genome-wide corrected threshold, HiSA-SV yielded 14 significant gene-sets and 29 suggestive sets. The top hypothetical signals included loci with known relevance to lipid metabolism and hepatic trafficking pathways. Notably, several sets were driven by mixed DEL+INS evidence where no single SV crossed stringent significance alone, illustrating the utility of hierarchical aggregation.

Illustrative (hypothetical) decomposition example:
- Program: lipid transport module
- Gene: **GENE-X**
- Dominant branch: intron + enhancer-overlapping DEL cluster
- Top contributing SVs: AF 1e-4–1e-3 range, moderate |Beta|, concordant direction

### Robustness to SV representation redundancy
Because AGGREGATED and BREAKPOINT labels can encode partially redundant events, we evaluated three pre-registered deduplication policies (cluster representative, label-priority pruning, and distance-window collapsing). HiSA-SV maintained stable ranking (Spearman ρ = 0.92–0.96 across policy pairs), indicating practical robustness when dependence is handled by conservative preprocessing.

### Biological interpretability from hierarchy paths
HiSA-SV reports not only omnibus p-values but also branch-level contributions:
**set → layer (exon/intron/intergenic) → SV-type (DEL/INS/DUP) → top events**.
This made result interpretation directly compatible with planned downstream multi-omic integration in T2D subtype studies.

---

### Discussion
This draft demonstrates a complete, extensible manuscript structure for hierarchical SV set testing with ACAT. The key conceptual advance is not ACAT alone, but **ACAT embedded in an annotation hierarchy** that mirrors biological organization and improves interpretability.

The framework is specifically suitable for summary-level SV analysis where LD matrices are unavailable or unreliable. By using p-value combination and strict preprocessing rules, HiSA-SV remains computationally tractable and methodologically transparent.

Several practical lessons emerge from the draft design. First, overlap policy and multi-gene mapping decisions materially affect set composition and should be pre-registered. Second, p-value underflow handling is mandatory for numerical stability. Third, mixed SV labels require explicit deduplication to avoid pseudo-replication.

Limitations include dependence on annotation completeness, potential residual dependence among overlapping SV representations, and inability of summary-only workflows to model carrier-level interaction structures. Future versions should integrate consequence severity tiers and optional Bayesian priors while preserving the same hierarchical ACAT backbone.

Overall, HiSA-SV offers a scalable route to gene-level SV association discovery and a practical bridge to integrative disease-subtype analyses.

---

## Methods

### Study context and analysis target
This framework was drafted for UKB WGS-based SV association summary analysis in cardiometabolic phenotypes, with current target trait Non-HDL-C (inverse-normal transformed, age/sex/YOB/PC adjusted). Reference genome: hg38.

### Input schema
Required fields:
`Chrom, Pos, Name, effectAllele, effectAlleleFreq, Beta, SE, pval, N, info`.
Derived fields:
`svtype, svsize, svsize_censored, sv_label, start, end`.

SV parsing pattern:
`<(?P<svtype>[A-Z]+):SVSIZE=(?P<svsize>\d+)(?P<svsize_plus>\+)?:(?P<label>[A-Z0-9_]+)>`.

### Set-definition hierarchy
Gene model: `hg38.refGene.gtf.gz`.
Layer policy:
- exon: any 1-bp overlap with exon feature
- intron: gene-body overlap without exon overlap
- intergenic: no overlap with any gene body
Exon takes precedence when overlaps are mixed.

### Multi-mapping policy
One SV may map to multiple genes; this is retained by design. Dependencies introduced by multi-mapping are addressed through deduplication and sensitivity analyses.

### ACAT formulation
For p-values \(p_i\) and normalized weights \(w_i\):
\[
T = \sum_i w_i \tan\{\pi(0.5-p_i)\},
\quad
p_{\mathrm{ACAT}} = 0.5 - \frac{\arctan(T)}{\pi}.
\]
We use equal weights by default and optionally apply AF-based or functional-impact weights.

### Numerical stability and QC rules
- p-value flooring: \(p \leftarrow \max(p, 10^{-300})\)
- p-value range check: \(0 < p \le 1\)
- coordinate convention harmonization prior to overlap
- AF-based inclusion thresholds pre-specified by analysis plan

### Deduplication sensitivity analyses
Given mixed labels (AGGREGATED/BREAKPOINT/COVERAGE), we evaluate:
1. cluster representative policy,
2. label-priority policy,
3. distance-window collapse.
Primary inference uses policy (1); others are sensitivity analyses.

### Comparative methods
- weighted burden
- Bonferroni-corrected min-p
- flat (non-hierarchical) ACAT

### Simulation design (for method validation)
- sample-size grid: 50k, 150k, 300k
- causal sparsity: 0–5% within set
- effect-size distribution scaled by AF bins
- annotation informativeness scenarios: low/medium/high
Outputs: type I error, power, rank stability, and branch-level attribution quality.

---

## Data availability
This manuscript version is a methodological draft with hypothetical results and does not release new participant-level data. Real analyses are intended for controlled-access UKB environments and governed by corresponding approvals.

## Code availability
Implementation scripts (annotation parser, overlap engine, hierarchical ACAT, and sensitivity modules) are planned for repository release in a subsequent version.

## Acknowledgements
We thank members of HAN Lab (Seoul National University College of Medicine) for project framing and cardiometabolic genetics discussion.

## Author contributions
Conceptualization, methodology, and drafting: project team.

## Competing interests
The authors declare no competing interests.

## Reporting summary
Further information on research design will be available in the Nature Portfolio Reporting Summary at submission.

## References
1. Liu Y, et al. ACAT: A fast and powerful p value combination method for rare-variant analysis in sequencing studies. *Am J Hum Genet*. 2019.  
2. Collins RL, et al. A structural variation reference for medical and population genetics. *Nature*. 2020.  
3. Audano PA, et al. Characterizing the major structural variant alleles of the human genome. *Cell*. 2019.  
4. Chiang C, et al. The impact of structural variation on human gene expression. *Nat Genet*. 2017.  
5. Lee S, et al. Rare-variant association analysis: study designs and statistical tests. *Am J Hum Genet*. 2014.
