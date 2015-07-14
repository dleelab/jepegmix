##Citing JEPEGMIX
**_JEPEGMIX: a summary statistics based tool for gene-level joint testing of functional variants_**, Donghyung Lee; Vernell S. Williamson; Tim B. Bigdeli; Brien P. Riley; Bradley T. Webb; Ayman H. Fanous; Kenneth S. Kendler; Vladimir I. Vladimirov; Silviu-Alin Bacanu; **Submitted**.

##Acknowledgement
**This work is supported by the National Institutes of Health with grants R25DA26119, R21MH100560, R21AA022717 and P50AA022537.**

<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/6/6a/US-NIH-NIDA-Logo.svg/440px-US-NIH-NIDA-Logo.svg.png" height="100px">
<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/4/4d/US-NIH-NIMH-Logo.svg/280px-US-NIH-NIMH-Logo.svg.png" height="100px">
<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/7/72/US-NIH-NIAAA-Logo.svg/440px-US-NIH-NIAAA-Logo.svg.png" height="100px">

##Download JEPEGMIX
The current release (Version 0.1.0) of JEPEGMIX is for a Linux user. The pre-compiled executables for other operating systems (e.g.,  Windows, MacOS) will be available soon. The latest source codes of JEPEGMIX are available upon request (dustorm_at_gmail_dot_com)

|**Direct download link**|**Version**|**Release Date**|
|:---|:---|:---|
|[JEPEGMIX for a Linux user]()|v0.1.0|07/13/2015|

##Download Reference Panels
|**Direct download link**|**Number of Samples**|**Number of populations**|**NCBI build**|**Release Date**|**Note**|
|:---|:---|:---|:---|:---|:---|
|[1000 Genomes Phase1 Release3](https://drive.google.com/file/d/0B_9H56XID17SLWJaWjlYekxkVkU/view?usp=sharing)|1092|14|build 37 (hg19)|Nov. 23 2010|Includes chr1-chr22|

Here are the 1000 Genome population abbreviations used by JEPEGMIX. AFR is an abbreviation for African; AMR for admixed American; ASN for East Asian; EUR for European. 

|**Population Abbreviation**|**Number of Subjects**|**Super Population**|**Population Description**|
|:---|:---|:---|:---|
|ASW|61|AFR|African Ancestry in Southwest US|
|CEU|85|EUR|Utah residents (CEPH) with Northern and Western European ancestry|
|CHB|97|ASN|Han Chinese in Beijing, China|
|CHS|100|ASN|Southern Han Chinese|
|CLM|60|AMR|Colombian in Medellin, Colombia|
|FIN|93|EUR|Finnish in Finland|
|GBR|89|EUR|British in England and Scotlant|
|IBS|14|EUR|Iberian populations in Spain|
|JPT|89|ASN|Japanese in Tokyo, Japan|
|LWK|97|AFR|Luhya in Wenbuye, Kenya|
|MXL|66|AMR|Mexican Ancestry from Los Angeles, USA|
|PUR|55|AMR|Puerto Rican in Puerto Rico|
|TSI|98|EUR|Toscani in Italia|
|YRI|88|AFR|Yoruba in Ibadan, Nigeria|

##Download SNP Annotation Data

|**Direct download link**|**Version**|**Release Date**|
|:---|:---|:---|
|[SNP annotations](https://drive.google.com/file/d/0B8CSKKDoI0UmNVdNenRPNmtYbkk/view?usp=sharing)|v0.2.0|11/20/2014|

##JEPEGMIX Input File Format

###When study allele frequency information is available
JEPEGMIX takes as input a plain text file with rows and columns denoting SNPs and variables, respectively. The first line of the input file should be column names/headers. Data entries on each line should be separated by white space. 
The file should contain eight columns: 1) rsid (SNP ID), 2) chr (chromosome number), 3) bp (base pair position), 4) a1 (reference allele), 5) a2 (alternative allele), 6) z (normally distributed GWAS/meta-analysis summary statistic, i.e. two-tailed Z-score), 7) info (imputation information) and 8) af1 (cohort reference allele frequency (RAF)). JEPEGMIX does not require the input data to be sorted in ascending order by chromosome number and base pair position or SNP ID. Here is a sample JEPEGMIX input file.

```
rsid        chr  bp         a1  a2  z          info    af1

rs1000109   9    117908733  C   T  -0.714464   0.890   0.384

rs10001109  4    44904653   C   T   0.721919   0.731   0.198

rs1000112   22   28273339   C   G  -0.583666   0.445   0.042 

rs10001127  4    130547376  T   C   0.069329   0.999   0.210 

rs1000113   5    150240076  T   C  -1.447288   1.0     0.189
```

###When study allele frequency information is not available
Genome-wide association studies/meta-analyses typically do not provide study allele frequency information due to privacy issues. However, information about ethnic proportion of the study samples is usually available from the publications. By using the prior ethnic information, users can run JEPEGMIX for association summary data lacking allele frequency information. In this case, JEPEGMIX does not require study allele frequency information (the column ‘af1’) in the input file, but additionally JEPEGMIX needs one more input text file (population weight file) specifying ethnic proportion of the study samples. Here is a sample JEPEGMIX input file with 5 SNPs, which should be used when allele frequency information is not available.

```
rsid        chr  bp         a1  a2   z         info  

rs1000109   9    117908733  C   T   -0.714464  0.890

rs10001109  4    44904653   C   T    0.721919  0.731

rs1000112   22   28273339   C   G   -0.583666  0.445

rs10001127  4    130547376  T   C    0.069329  0.999

rs1000113   5    150240076  T   C   -1.447288  1.0
```

**Note:** If the input summary data comes a different genome assembly (e.g. NCBI build 36 (hg18)) than NCBI build 37 (hg19), it needs to be converted by the user to NCBI build 37 (hg19) using a software, called [liftover](https://genome.ucsc.edu/cgi-bin/hgLiftOver), from UCSC.


Here is a sample JEPEGMIX population weight file, which is needed when cohort allele frequency information is not available. 

```
pop	wgt   

ASW	0.1

GBR	0.3

FIN 0.2

CEU	0.25

IBS	0.15
```

The first line of the population weight file should be column names/headers. The file should contain two columns: 1) pop (population abbreviation) and 2) wgt (population proportion). The columns of data should be separated by white space. The weight file name should be specified with the ‘--populationWeight’ option.
   
##JEPEGMIX output file format

The JEPEGMIX/JEPEG output file has nine columns: 1)  gene name (geneid), 2) chi-square test statistic value (chisq), 3) degrees of freedom (df), 4) JEPEGMIX p-value (jepegmix_pval), 5) number of functional SNPs associated with gene (num_snp), 6) top functional category (top_categ), 7) top category p-value (top_categ_pval), 8) top functional SNP ID (top_snp) and 9) top SNP p-value (top_snp_pval). The first line of the output file is column names/headers.  Here is a sample JEPEGMIX(JEPEG) output file, with 5 genes:

```
geneid    chisq    df  jepeg_pval   num_snp   top_categ   top_categ_pval   top_snp      top_snp_pval

FCGR3B    14.926   1   1.80E-05     2         PFS         1.10E-04         rs5030738    5.08E-05
 
CSPG4P2Y  14.774   2   3.29E-05     5         TRN         1.21E-04         rs10828664   5.55E-05
		
SLC7A7    19.902   3   3.40E-05     33        TRN         3.51E-04         rs9304810    1.07E-03

EDARADD   13.957   2   3.93E-05     2         PFS         1.86E-04         rs966365     7.80E-06
 
FAM71D    13.026   1   4.34E-05     26        TAR         3.07E-04         rs45515505   1.53E-04
```


##Options

|**Option**|**Short Flag**|**Parameter**|**Default**|**Description**|
|:---|:---|:---|:---|:---|
|--version|-v|none|none|Prints version information.|
|--help|-h|none|none|Outputs a full description of all JEPEGMIX options.|
|--impute|none|none|none|Imputes summary statistics of unmeasured functional SNPs using DISTMIX before JEPEGMIX analysis.|
|--reference|-r|filename|none|The filename of the reference population data.|
|--referenceIndex|-i|filename|none|The filename of the reference population index data.|
|--annotation|-a|filename|none|The filename of the SNP annotation data set.|
|--output|-o|filename|out.jepegmix|The filename of JEPEGMIX(JEPEG) output|
|--windowSize|-n|decimal|1.0|The size of the DISTMIX prediction window (Mb).|
|--wingSize|-m|decimal|0.5|The size of the wing padded on the left and right of the DISTMIX prediction window (Mb).|
|--populationWeight|-w|filename|none|The filename of the population weight data.|
|--impInfoCutoff|none|decimal|0.3|The imputation information cutoff.|

