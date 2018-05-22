# mipmapper
[![Travis build status](https://travis-ci.org/mrc-ide/mipmapper.svg?branch=master)](https://travis-ci.org/mrc-ide/mipmapper)
[![AppVeyor build status](https://ci.appveyor.com/api/projects/status/github/mrc-ide/mipmapper?branch=master&svg=true)](https://ci.appveyor.com/project/mrc-ide/mipmapper)
[![Coverage status](https://codecov.io/gh/mrc-ide/mipmapper/branch/master/graph/badge.svg)](https://codecov.io/github/mrc-ide/mipmapper?branch=master)

The R package *mipmapper* package contains a series of functions for analysing and visualising Molecular Inversion Probe (MIP) data. **This package is in early stages of development**, but will hopefully eventually include a range of population genetic analyses.

### Installation

In R, ensure that you have the devtools package installed by running
```r
install.packages("devtools")
```
Then simply install and load the *mipmapper* package directly from GitHub by running
```r
devtools::install_github("mrc-ide/mipmapper")
library(mipmapper)
```

### Example analysis

Load raw data from .csv file. You will need to change the file path to where you have stored the data.
```r
dat0 <- fast_read("NeutralSNPs_AheroYombo.csv")
```
Some miscellaneous filtering. Subset to SNPs only (i.e. no more complex mutations), group all alternative alleles together as a single "non-reference" allele, and drop irregular loci (for example non-integer barcode counts).
```r
dat1 <- filter_misc(dat0, SNP_only = TRUE, group_Alt = TRUE, drop_irregular = TRUE)
```
Next we want to filter based on coverage, throwing away any loci that are below a minimum coverage level. We can visualise how much data will be left at different thresholds using the following function:
```r
plot_coverage(dat1)
```
Choose a threshold that strikes a balance between data quantity and quality. Once you have chosen a threshold, apply the filtering as follows:
```r
my_threshold <- 10
dat3 <- filter_coverage(dat1, min_coverage = my_threshold)
```


