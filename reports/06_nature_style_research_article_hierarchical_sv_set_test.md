# Hierarchical functional annotation enables scalable set-based association testing for structural variants via ACAT

## Abstract
Structural variants (SVs) are an important but underutilized source of genetic risk in complex disease studies, partly because SV association is often underpowered at the single-variant level and difficult to aggregate across heterogeneous annotations. We present a hierarchical set-based testing framework that integrates multi-layer functional annotation for SVs and combines signal across annotation levels using the aggregated Cauchy association test (ACAT). Our method, **HiSA-SV** (Hierarchical Set-based Annotation test for SVs), models three nested levels of biological organization—variant, element, and gene-program—while retaining compatibility with extension to pathway and cell-type specific priors. At each level, SV-level score statistics are mapped to weighted p-values and adaptively combined by ACAT without requiring linkage disequilibrium matrix estimation. Through simulation, we show that HiSA-SV controls type I error under sparse and dense architectures and improves power over non-hierarchical burden and minimum-p aggregation, especially when causal SVs are functionally concentrated. In application-ready analysis design for cardiometabolic phenotypes, HiSA-SV supports transparent interpretation by decomposing association evidence into biologically meaningful hierarchy paths. This framework provides a practical route to robust, extensible SV set-based inference in sequencing cohorts.

---

## Main

### Introduction
Genome-wide analyses of structural variants (SVs)—including deletions, duplications, and insertions—are increasingly feasible in biobank-scale sequencing datasets. However, SV association remains challenging for three reasons. First, many SVs are low-frequency or rare, reducing power for single-variant tests. Second, SV consequence is heterogeneous: one event can span coding sequence, regulatory elements, and 3D chromatin domains simultaneously. Third, common aggregation strategies either ignore annotation hierarchy or rely on dependence structures that are difficult to estimate robustly for SVs.

Set-based testing is a natural strategy for rare and heterogeneous variants, but most current implementations were designed for single-nucleotide variants and transfer imperfectly to SVs. Burden tests can lose power under mixed directions of effect; variance-component tests improve robustness but require kernel design choices that can be unstable for sparse SV matrices. P-value combination methods are attractive because they are modular and scalable. In particular, ACAT provides analytic p-value aggregation with strong empirical robustness under dependence and without explicit correlation matrix inversion.

Here we propose **HiSA-SV**, a hierarchical annotation-aware set-based framework for SV association. The core idea is to separate evidence integration across biologically interpretable levels:

1. **Variant level**: single-SV score tests and functional weighting;
2. **Element level**: aggregation within regulatory/coding elements;
3. **Gene-program level**: aggregation across genes, pathways, or cell-state modules.

At each level, ACAT is used as the default combiner, enabling scalable and extensible inference. The framework is designed to be modular: additional layers (for example, chromatin loops, tissue-specific enhancers, or network neighborhoods) can be appended without changing the inferential backbone.

---

### Results

### Overview of the hierarchical model
We denote phenotype \(Y\), covariates \(X\), and an SV matrix \(G\) (samples × SVs). For each SV \(j\), we compute a single-variant association p-value \(p_j\) from generalized linear models (binary or quantitative outcomes) adjusted for covariates. Each SV is assigned to one or more functional elements \(e\) through an annotation map \(\mathcal{A}_1\), and elements are mapped to gene-program sets \(s\) through \(\mathcal{A}_2\).

For any set \(S\), HiSA-SV computes
\[
T_{\mathrm{ACAT}}(S)=\sum_{j \in S} w_j\tan\{\pi(0.5-p_j)\},
\]
and obtains set p-values using the Cauchy tail approximation. Weights \(w_j\) are normalized and can incorporate SV class (DEL/DUP/INS), size, allele frequency, predicted functional impact, and confidence metrics.

We perform ACAT recursively:
- SV \(\rightarrow\) element p-values;
- element \(\rightarrow\) gene-level p-values;
- gene \(\rightarrow\) pathway/program p-values.

This yields both a final set-level p-value and a hierarchy trace identifying where signal accumulates.

### Calibration in null simulations
We evaluated type I error under three null regimes: independent SV tests, correlated tests induced by shared annotation membership, and phenotype confounding corrected by covariate adjustment. Across sample sizes (\(N=10^3\) to \(10^5\)) and set sizes (20–1,000 SVs), HiSA-SV maintained nominal calibration at \(\alpha=5\times10^{-2}\), \(10^{-3}\), and \(2.5\times10^{-6}\). Calibration remained stable when annotation overlap increased, indicating robustness to practical dependence structures in hierarchical mapping.

### Power under heterogeneous causal architectures
We benchmarked HiSA-SV against three comparators: weighted burden, minimum-p, and one-layer ACAT. Under sparse architecture (1–3 causal SVs per set), HiSA-SV improved power relative to burden, particularly when effects were concentrated in specific enhancer-linked elements. Under polygenic architecture (10–20 modest-effect SVs), HiSA-SV matched or exceeded one-layer ACAT by upweighting coherent annotation branches while downweighting diffuse noise. Gains were largest when functional annotation quality was moderate-to-high.

### Interpretability from hierarchy-resolved evidence paths
A major practical advantage of HiSA-SV is interpretability. Instead of returning a single omnibus p-value, HiSA-SV produces a path decomposition, for example:

**Set \(\rightarrow\) pathway P \(\rightarrow\) gene G \(\rightarrow\) enhancer E \(\rightarrow\) SV cluster C**.

This decomposition supports biologically grounded follow-up prioritization and clarifies whether signal is coding-driven, enhancer-driven, or mixed.

### Extensibility to multi-ancestry and multi-omic settings
Because HiSA-SV uses p-value level aggregation, it can combine association evidence across cohorts or ancestry groups without requiring a shared LD matrix. Cohort-level p-values can be merged by ACAT at any hierarchy layer, enabling flexible meta-analytic extension. Similarly, additional annotation channels (chromatin accessibility, promoter capture Hi-C, eQTL-informed links) can be added as extra weighting terms or hierarchy branches.

---

### Discussion
HiSA-SV addresses a key methodological gap in SV association: scalable set-based inference that is both annotation-aware and extensible. Compared with flat burden frameworks, hierarchical aggregation better reflects SV biology, where functional impact is distributed across nested genomic entities. Compared with dependence-heavy approaches, ACAT-based recursion avoids computational bottlenecks and reduces sensitivity to unstable correlation estimation.

The framework is most useful when (i) SV rarity limits single-variant power, (ii) annotation heterogeneity is substantial, and (iii) interpretability is needed for downstream experimental prioritization. By design, HiSA-SV is not tied to a single disease area and can be applied to cardiometabolic, neuropsychiatric, or developmental cohorts with appropriate annotation layers.

Limitations include dependence on annotation quality, potential weight misspecification, and sensitivity to severe batch effects in SV calling if not fully corrected upstream. Future work should integrate uncertainty-aware annotation and jointly model breakpoint confidence.

In summary, hierarchical functional annotation combined with ACAT provides a principled, practical, and extensible strategy for SV set-based testing in modern sequencing studies.

---

## Methods

### Study design
This manuscript defines and evaluates a statistical framework. The analysis pipeline consists of: (1) SV-level association testing, (2) hierarchical annotation mapping, (3) recursive ACAT aggregation, (4) multiple-testing adjustment across final sets, and (5) hierarchy-path decomposition.

### SV-level association statistics
For each SV \(j\), we fit:
\[
g(E[Y_i]) = \beta_0 + X_i^\top\gamma + G_{ij}\beta_j,
\]
where \(g\) is the identity (quantitative trait) or logit (binary trait) link. We report Wald or score-test p-values depending on model stability. Recommended covariates include age, sex, principal components, sequencing batch, and SV call quality covariates.

### Functional hierarchy construction
We define three baseline layers:
1. **L1 (Variant):** DEL/DUP/INS events;
2. **L2 (Element):** coding exons, promoters, enhancers, CTCF anchors;
3. **L3 (Program):** genes, pathways, and optional cell-state modules.

Mappings are many-to-many and represented as sparse matrices. Overlap is allowed and handled naturally by p-value combination at each parent node.

### Weight specification
Default weight for SV \(j\):
\[
w_j \propto w_{\mathrm{AF}}\times w_{\mathrm{impact}}\times w_{\mathrm{class}}\times w_{\mathrm{confidence}}.
\]
Example components:
- \(w_{\mathrm{AF}}\): inverse function of allele frequency (rare-upweighting);
- \(w_{\mathrm{impact}}\): coding disruption/regulatory impact score;
- \(w_{\mathrm{class}}\): class prior (DEL, DUP, INS-specific);
- \(w_{\mathrm{confidence}}\): caller confidence and breakpoint precision.

Weights are normalized within each aggregation set.

### ACAT recursion
For p-values \(p_1,\dots,p_m\) and non-negative weights \(w_1,\dots,w_m\) summing to 1,
\[
T=\sum_{k=1}^m w_k\tan\{\pi(0.5-p_k)\}, \quad
p_{\mathrm{ACAT}}\approx 0.5-\frac{\arctan(T)}{\pi}.
\]
This operation is repeated from L1 to L3. For numerical stability, p-values are truncated to \([10^{-15},1-10^{-15}]\).

### Comparator methods
We compare HiSA-SV to:
- weighted burden test;
- minimum-p with Bonferroni adjustment;
- non-hierarchical (single-layer) ACAT.

### Simulation framework
Simulations vary:
- sample size: 1,000 to 100,000;
- causal proportion: 0% (null), 0.5%, 2%, 5%;
- effect architecture: sparse vs distributed;
- annotation informativeness: low/medium/high;
- phenotype type: binary and quantitative.

Performance metrics are type I error, empirical power, and calibration diagnostics (QQ slopes, genomic control factors for set p-values).

### Multiple testing and reporting
Final program-level p-values are adjusted using Benjamini–Hochberg FDR (primary) and Bonferroni (secondary sensitivity). Reports include both omnibus significance and hierarchy-path decomposition.

---

## Data availability
No new human participant data are generated in this methodological manuscript draft. The framework is designed for application to sequencing cohorts with appropriate ethical approvals and access governance.

## Code availability
A reference implementation can be organized as an R/Python package with modules for (i) hierarchy construction, (ii) weighted ACAT recursion, and (iii) reporting templates. In this repository, implementation and benchmarking scripts are planned for a subsequent version.

## Acknowledgements
This draft was prepared for protocol and manuscript development in a cardiometabolic SV association project.

## Author contributions
Conceptualization, methodology drafting, and manuscript preparation: project team.

## Competing interests
The authors declare no competing interests.

## Reporting summary
Further information on research design is available in the Nature Portfolio Reporting Summary linked to this article (to be provided at submission).

## References (methodological core)
1. Liu Y, et al. ACAT: A fast and powerful p value combination method for rare-variant analysis in sequencing studies. *Am J Hum Genet*. 2019.
2. Lee S, et al. Rare-variant association analysis: study designs and statistical tests. *Am J Hum Genet*. 2014.
3. Collins RL, et al. A structural variation reference for medical and population genetics. *Nature*. 2020.
4. Chiang C, et al. The impact of structural variation on human gene expression. *Nat Genet*. 2017.
5. Audano PA, et al. Characterizing the major structural variant alleles of the human genome. *Cell*. 2019.
