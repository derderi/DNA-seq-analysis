# DNA-seq

### Databases for variants
* [Disease Variant Store](https://rvs.u.hpc.mssm.edu/divas/)
* [The ExAC Browser: Displaying reference data information from over 60,000 exomes](https://github.com/konradjk/exac_browser)

**Important paper** [DNA damage is a major cause of sequencing errors, directly confounding variant identification](http://biorxiv.org/content/early/2016/08/19/070334)

>However, in this study we show that false positive variants can account for more than 70% of identified somatic variations, rendering conventional detection methods inadequate for accurate determination of low allelic variants. Interestingly, these false positive variants primarily originate from mutagenic DNA damage which directly confounds determination of genuine somatic mutations. Furthermore, we developed and validated a simple metric to measure mutagenic DNA damage and demonstrated that mutagenic DNA damage is the leading cause of sequencing errors in widely-used resources including the **1000 Genomes Project** and **The Cancer Genome Atlas**.

### How to represent sequence variants
[Sequence Variant Nomenclature from Human Genome Variation Society](http://varnomen.hgvs.org/)

dbSNP IDs are not unique?

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Oh God, why are people still using dbSNP IDs as though they&#39;re unique identifiers?</p>&mdash; Daniel MacArthur (@dgmacarthur) <a href="https://twitter.com/dgmacarthur/status/758331620080422912">July 27, 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

#### The Evolving Utility of dbSNP 

see a [post:dbSNP (build 147) exceeds a ridiculous 150 million variants](http://massgenomics.org/2016/09/dbsnp-ridiculous-variants.html)

>In the early days of next-generation sequencing, dbSNP provided a vital discriminatory tool. In exome sequencing studies of Mendelian disorders, any variant already present in dbSNP was usually common, and therefore unlikely to cause rare genetic diseases. Some of the first high-profile disease gene studies therefore used dbSNP as a filter. Similarly, in cancer genomics, a candidate somatic mutation observed at the position of a known polymorphism typically indicated a germline variant that was under-called in the normal sample. Again, dbSNP provided an important filter.

>Now, **the presence or absence of a variant in dbSNP carries very little meaning.** The database includes over 100,000 variants from disease mutation databases such as OMIM or HGMD. It also contains some appreciable number of somatic mutations that were submitted there before databases like COSMIC became available. And, like any biological database, dbSNP undoubtedly includes false positives.

>Thus, while the mere presence of a variant in dbSNP is a blunt tool for variant filtering, dbSNP’s deep allele frequency data make it incredibly powerful for genetics studies: it can rule out variants that are too prevalent to be disease-causing, and prioritize ones that are rarely observed in human populations. This discriminatory power will only increase as ambitious large-scale sequencing projects like CCDG make their data publicly available.


### Tips and lessons learned during my DNA-seq data analysis journey.  

1. [Allel frequency](https://en.wikipedia.org/wiki/Allele_frequency)  
  Allele frequency, or gene frequency, is the proportion of a particular allele (variant of a gene) among all allele copies       being considered. It can be formally defined as the percentage of all alleles at a given locus on a chromosome in a population   gene pool represented by a particular allele.

2. "for SNVs, we are interested in genotype 0/1, 1/1 for tumor and 0/0 for normal. 1/1 genotype is very rare.  
   It requires the same mutation occurs at the same place in two sister chromsomes which is very rare. one possible way to get 
   1/1 is deletion of one chromosome and duplication of the mutated chromosome". Quote from Siyuan Zheng.

3. "Mutect analysis on the TCGA samples finds around 5000 ~ 8000 SNVs per sample." Quote from Siyuan Zheng. 
4. Cell lines might be contamintated or mislabled. [The Great Big Clean-Up](http://mobile.the-scientist.com/article/43821/the-great-big-clean-up)  
5. Tumor samples are not pure, you will always have stromal cells and infiltrating immnue cells in the tumor bulk. When you analyze the data, keep this in mind.
6. the devil 0 based and 1 based coordinate systems! Make sure you know which system your file is using:
![](https://camo.githubusercontent.com/3937606a47ad455b9bf2ba9bfca9e91f5afbb3a8/68747470733a2f2f692e696d6775722e636f6d2f337449445574442e706e67)

credit from Vince Buffalo.
Also, read this [post](https://standage.github.io/on-genomic-interval-notation.html) and this [post](https://www.biostars.org/p/84686/)  


### Mutation caller, structural variant caller

* paper [Making the difference: integrating structural variation detection tools](http://bib.oxfordjournals.org/content/16/5/852.short?rss=1&utm_source=twitterfeed&utm_medium=twitter)
* [GATK HaplotypeCaller Analysis of BWA (mem) mapped Illumina reads](http://wiki.bits.vib.be/index.php/GATK_HaplotypeCaller_Analysis_of_BWA_(mem)_mapped_Illumina_reads)
* [NGS-DNASeq_GATK-session.pdf](https://github.com/crazyhottommy/DNA-seq-analysis/files/94758/NGS-DNASeq_GATK-session.pdf)  
* [GATK pipeline](https://github.com/crazyhottommy/GATK-pipeline)  
* [An ensemble approach to accurately detect somatic mutations using SomaticSeq](http://www.genomebiology.com/2015/16/1/197#B14) [tool github page](https://github.com/bioinform/somaticseq/)
* [lumpy](https://github.com/arq5x/lumpy-sv)
* [wham](https://github.com/zeeev/wham)
* [SV-Bay](https://github.com/InstitutCurie/SV-Bay )  
* [Delly](https://github.com/tobiasrausch/delly)
* [COSMOS](http://seselab.org/cosmos/): Somatic Large Structural Variation Detector
* Fusion And Chromosomal Translocation Enumeration and Recovery Algorithm [(FACTERA)](https://factera.stanford.edu/)  
* [VarDict](https://github.com/AstraZeneca-NGS/VarDict): a novel and versatile variant caller for next-generation sequencing in cancer research. we demonstrated that VarDict has improved sensitivity over `Manta` and equivalent sensitivity to `Lumpy`. SNP call rates are on par with `MuTect`, and VarDict is more sensitive and precise than `Scalpel` and other callers for insertions and deletions. see a [post](http://bcb.io/2016/04/04/vardict-filtering/) by Brad Chapman. Looks very promising.
* [Weaver: Allele-Specific Quantification of Structural Variations in Cancer Genomes](https://github.com/leofountain/Weaver). [Paper](http://biorxiv.org/content/early/2016/04/12/048207)
* [SVScore: An Impact Prediction Tool For Structural Variation](http://biorxiv.org/content/early/2016/09/06/073833)
* [Prioritisation of Structural Variant Calls in Cancer Genomes](http://biorxiv.org/content/early/2016/11/04/084640) [simple_sv_annotation.py](https://github.com/AstraZeneca-NGS/simple_sv_annotation) to annotate Lumpy and Mannta SV calls.
* [Genome-wide profiling of heritable and de novo STR variations](http://biorxiv.org/content/early/2016/09/27/077727) short tandem repeats.

### SNV filtering

* [paper: Using high-resolution variant frequencies to empower clinical genome interpretation](http://biorxiv.org/content/early/2016/09/02/073114) [shiny App](https://jamesware.shinyapps.io/alleleFrequencyApp/)  
>Whole exome and genome sequencing have transformed the discovery of genetic variants that cause human Mendelian disease, but discriminating pathogenic from benign variants remains a daunting challenge. Rarity is recognised as a necessary, although not sufficient, criterion for pathogenicity, but frequency cutoffs used in Mendelian analysis are often arbitrary and overly lenient. Recent very large reference datasets, such as the Exome Aggregation Consortium (ExAC), provide an unprecedented opportunity to obtain robust frequency estimates even for very rare variants. Here we present a statistical framework for the frequency-based filtering of candidate disease-causing variants, accounting for disease prevalence, genetic and allelic heterogeneity, inheritance mode, penetrance, and sampling variance in reference datasets.

* a new database called [dbDSM](http://bioinfo.ahu.edu.cn:8080/dbDSM/index.jsp)
A database of Deleterious Synonymous Mutation, a continually updated database that collects, curates and manages available human disease-related SM data obtained from published literature.

* [LncVar](http://bioinfo.ibp.ac.cn/LncVar/): a database of genetic variation associated with long non-coding genes

### Third generation sequencing for Structural variants (works on short reads as well!)
* [beautiful “Ribbon” viewer to visualize complicated SVs revealed by PacBio reads](http://genomeribbon.com/) [github page](https://github.com/MariaNattestad/ribbon)
* [Sniffles: Structural variation caller using third generation sequencing](https://github.com/fritzsedlazeck/Sniffles) is a structural variation caller using third generation sequencing (PacBio or Oxford Nanopore). It detects all types of SVs using evidence from split-read alignments, high-mismatch regions, and coverage analysis.
* [splitThreader](http://splitthreader.com/) for visualizing structural variants. Finally a good visualizer!

**A series of posts from Brad Chapman**  

1. [Validating multiple cancer variant callers and prioritization in tumor-only samples](http://bcb.io/2015/03/05/cancerval/)  
2. [Benchmarking variation and RNA-seq analyses on Amazon Web Services with Docker](http://bcb.io/2014/12/19/awsbench/)  
3. [Validating generalized incremental joint variant calling with GATK HaplotypeCaller, FreeBayes, Platypus and samtools](http://bcb.io/2014/10/07/joint-calling/)  
4. [Validated whole genome structural variation detection using multiple callers](http://bcb.io/2014/08/12/validated-whole-genome-structural-variation-detection-using-multiple-callers/)  
5. [Validated variant calling with human genome build 38](http://bcb.io/2015/09/17/hg38-validation/)


### Copy number variants 
* [Interactive analysis and assessment of single-cell copy-number variations](http://www.nature.com/nmeth/journal/vaop/ncurrent/full/nmeth.3578.html): [Ginkgo](http://qb.cshl.edu/ginkgo)   
* [Copynumber Viewer](https://github.com/RCollins13/CNView)
* [paper: Computational tools for copy number variation (CNV) detection using next-generation sequencing data: features and perspectives](http://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-14-S11-S1)
* [bioconductor copy number work flow](https://www.bioconductor.org/help/course-materials/2014/SeattleOct2014/B02.2.3_CopyNumber.html)
* [paper: Assessing the reproducibility of exome copy number variations predictions](http://www.ncbi.nlm.nih.gov/pubmed/27503473?dopt=Abstract&utm_source=dlvr.it&utm_medium=twitter)
* [CNVkit](https://github.com/etal/cnvkit) A command-line toolkit and Python library for detecting copy number variants and alterations genome-wide from targeted DNA sequencing.

### Tools for visulization 
1. [New app gene.iobio](http://iobio.io/)  
[App here](http://gene.iobio.io/?rel0=proband&rel1=mother&rel2=father) I will definetely have it a try.

2. [ASCIIGenome](https://github.com/dariober/ASCIIGenome) is a command-line genome browser running from terminal window and solely based on ASCII characters. Since ASCIIGenome does not require a graphical interface it is particularly useful for quickly visualizing genomic data on remote servers. The idea is to make ASCIIGenome the Vim of genome viewers.

### Tools for vcf files
1. [tools for pedigree files](https://github.com/brentp/peddy). It can determine sex from PED and VCF files. Developed by Brent Pedersen. I really like tools from Aaron Quinlan's lab.
2. [cyvcf2](https://github.com/brentp/cyvcf2) is a cython wrapper around htslib built for fast parsing of Variant Call Format (VCF) files
3. [PyVCF](http://pyvcf.readthedocs.org/en/latest/) - A Variant Call Format Parser for Python
4. [VcfR: an R package to manipulate and visualize VCF format data](https://cran.r-project.org/web/packages/vcfR/index.html)
5. [Varapp](https://varapp-demo.vital-it.ch/docs/src/about.html) is an application to filter genetic variants, with a reactive graphical user interface. Powered by [GEMINI](https://varapp-demo.vital-it.ch/docs/src/about.html).
6. [varmatch: robust matching of small variant datasets using flexible scoring schemes](https://github.com/medvedevgroup/varmatch)
7. [vcf-validator](https://github.com/EBIvariation/vcf-validator) validate your VCF files!
8. [BrowseVCF](https://github.com/BSGOxford/BrowseVCF): a web-based application and workflow to quickly prioritize disease-causative variants in VCF files

### mutation signature

* [signeR](http://bioconductor.org/packages/release/bioc/html/signeR.html)
* [deconstructSigs](https://github.com/raerose01/deconstructSigs)
* [MutationalPatterns](https://github.com/CuppenResearch/MutationalPatterns)

### Tools for MAF files
TCGA has all the variants calls in MAF format. Please read a [post](https://www.biostars.org/p/69222/) by Cyriac Kandoth. 

1. [convert vcf to MAF](https://github.com/mskcc/vcf2maf): perl script by Cyriac Kandoth.
2. once converted to MAF, one can use this [MAFtools](https://github.com/PoisonAlien/maftools) to do visualization: oncoprint wraps complexHeatmap, Lollipop and Mutational Signatures etc. Very cool, I just found it...
3. [MutationalPatterns](https://github.com/CuppenResearch/MutationalPatterns): an integrative R package for studying patterns in base substitution catalogues

### Tools for bam files

1. [VariantBam](https://github.com/jwalabroad/VariantBam): Filtering and profiling of next-generational sequencing data using region-specific rules


### Annotate and explore variants 
1. Variant Effect Predictor: [VEP](http://useast.ensembl.org/info/docs/tools/vep/index.html)
2. [SNPEFF](http://snpeff.sourceforge.net/)
3. [vcfanno](https://github.com/brentp/vcfanno)
4. [myvariant.info](http://myvariant.info/) [tutorial](https://github.com/SuLab/myvariant.info/blob/master/docs/ipynb/myvariant_R_miller.ipynb) 
5. [FunSeq2](http://funseq2.gersteinlab.org/)- A flexible framework to prioritize regulatory mutations from cancer genome sequencing
6. [ClinVar](https://github.com/macarthur-lab/clinvar)  
7. [ExAC](http://exac.broadinstitute.org/)
8. [vcf2db](https://github.com/quinlan-lab/vcf2db) and [GEMINI](https://gemini.readthedocs.org/en/latest/index.html): a flexible framework for exploring genome variation from Qunlan lab.

### Plotting
1.[oncoprint](https://bioconductor.org/packages/release/bioc/vignettes/ComplexHeatmap/inst/doc/s8.oncoprint.html)
2. [deconstructSigs](https://github.com/raerose01/deconstructSigs) aims to determine the contribution of known mutational processes to a tumor sample. By using deconstructSigs, one can: Determine the weights of each mutational signature contributing to an individual tumor sample; Plot the reconstructed mutational profile (using the calculated weights) and compare to the original input sample
3. [Fast Principal Component Analysis of Large-Scale Genome-Wide Data](https://github.com/gabraham/flashpca)

### Identify driver genes

* [MUFFINN: cancer gene discovery via network analysis of somatic mutation data](http://genomebiology.biomedcentral.com/articles/10.1186/s13059-016-0989-x?platform=hootsuite)

### Tumor purity 
* ESTIMATE
* ABSOLUTE
* [THetA: Tumor Heterogeneity Analysis](http://compbio.cs.brown.edu/projects/theta/) is an algorithm that estimates the tumor purity and clonal/sublconal copy number aberrations directly from high-throughput DNA sequencing data. The latest release is called THetA2 and includes a number of improvements over previous versions.
* [CIBERSORT](https://cibersort.stanford.edu/index.php) is an analytical tool developed by Newman et al. to provide an estimation of the abundances of member cell types in a mixed cell population, using gene expression data
* [paper: Digitally deconvolving the tumor microenvironment](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-016-1036-7?utm_content=buffer45a4c&utm_medium=social&utm_source=twitter.com&utm_campaign=buffer)
* [Comprehensive analyses of tumor immunity: implications for cancer immunotherapy](http://genomebiology.biomedcentral.com/articles/10.1186/s13059-016-1028-7?platform=hootsuite) by Shierly Liu's lab. [TIMER](http://cistrome.org/TIMER/): Tumor IMmune Estimation Resource
A comprehensive resource for the clinical relevance of tumor-immune infiltrations
* [Reference-free deconvolution of DNA methylation data and mediation by cell composition effects](http://biorxiv.org/content/early/2016/01/22/037671). The R package's documentation is minimal... see tutorial [here](http://people.oregonstate.edu/~housemae/software/TutorialLondon2014/) from the author. Brent Perdson has a tool implementing the same method used by Houseman: [celltypes450](https://github.com/brentp/celltypes450).
* [paper: Toward understanding and exploiting tumor heterogeneity](http://www.ncbi.nlm.nih.gov/pubmed/26248267)  
* [paper: The prognostic landscape of genes and infiltrating immune cells across human cancers](http://www.ncbi.nlm.nih.gov/pubmed/26193342)  from Alizadeh lab.
* [Robust enumeration of cell subsets from tissue expression profiles](http://www.nature.com/nmeth/journal/v12/n5/abs/nmeth.3337.html)  from Alizadeh lab, and the [CIBERSORT tool](https://cibersort.stanford.edu/index.php) 

### tumor colonality and evolution

* [A step-by-step guide to estimate tumor clonality/purity from variant allele frequency data](https://github.com/hammerlab/vaf-experiments)
* [densityCut: an efficient and versatile topological approach for automatic clustering of biological data](http://m.bioinformatics.oxfordjournals.org/content/early/2016/04/23/bioinformatics.btw227.short?rss=1) can be used to cluster allel frequence.
* [phyC: Clustering cancer evolutionary trees](http://biorxiv.org/content/early/2016/08/12/069302)
* [CloneCNA](http://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-016-1174-7): detecting subclonal somatic copy number alterations in heterogeneous tumor samples from whole-exome sequencing data
* [paper: Distinct evolution and dynamics of epigenetic and genetic heterogeneity in acute myeloid leukemia](http://www.nature.com/nm/journal/v22/n7/full/nm.4125.html)
* [paper: Visualizing Clonal Evolution in Cancer](http://www.cell.com/molecular-cell/pdf/S1097-2765(16)30188-5.pdf)
* [An R package for inferring the subclonal architecture of tumors:sciclone](https://github.com/genome/sciclone)
* [Inferring and visualizing clonal evolution in multi-sample cancer sequencing: clonevol](https://github.com/hdng/clonevol)
* [fishplot: Create timecourse "fish plots" that show changes in the clonal architecture of tumors](https://github.com/chrisamiller/fishplot)
* [tools from OMICS tools website](https://omictools.com/tumor-purity-and-heterogeneity-category)
* [PhyloWGS](https://github.com/morrislab/phylowgs): Reconstructing subclonal composition and evolution from whole-genome sequencing of tumors.
* [SCHISM](http://karchinlab.org/apps/appSchism.html) SubClonal Hierarchy Inference from Somatic Mutation



### mutual exclusiveness of mutations
* [MEGSA](http://biorxiv.org/content/early/2015/04/09/017731): A powerful and flexible framework for analyzing mutual exclusivity of tumor mutations.
* [CoMet](https://github.com/raphael-group/comet)  

### mutation enrich in pathways
*[PathScore: a web tool for identifying altered pathways in cancer data](http://pathscore.publichealth.yale.edu/)

### Non-coding mutations
* [Large-scale Analysis of Variants in noncoding Annotations:LARVA](http://larva.gersteinlab.org/)


### CRISPR
* [The caRpools package - Analysis of pooled CRISPR Screens](https://cran.r-project.org/web/packages/caRpools/vignettes/CaRpools.html)
* [CRISPR Library Designer (CLD): a software for the multispecies design of sgRNA libraries](https://github.com/boutroslab/cld)

### long reads
[Quality Assessment Tools for Oxford Nanopore MinION data](https://bioconductor.org/packages/3.2/bioc/html/IONiseR.html)
[Signal-level algorithms for MinION data](https://github.com/jts/nanopolish)

### Single-cell DNA sequencing

* A review paper 2016: [Single-cell genome sequencing:current state of the science](http://www.nature.com/nrg/journal/v17/n3/abs/nrg.2015.16.html) 
* [Monovar](http://www.nature.com/nmeth/journal/vaop/ncurrent/full/nmeth.3835.html): single-nucleotide variant detection in single cells

