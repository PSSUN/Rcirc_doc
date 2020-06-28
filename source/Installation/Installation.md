# Installation
Before install Rcirc, you should make sure those packages has been installed:

 - Biostrings
 - GenomicAlignments
 - GenomicFeatures
 - GenomicRanges
 - IRanges
 - RColorBrewer
 - circlize
 - dplyr
 - ggplot2
 - grid
 - gtable
 - stringr
 
Use this code to check them:
```R
installed_list <- as.data.frame(installed.packages())$Package
required_list <- c(
  'Biostrings',
  'GenomicAlignments',
  'GenomicFeatures',
  'GenomicRanges',
  'IRanges',
  'RColorBrewer',
  'circlize',
  'dplyr',
  'ggplot2',
  'grid',
  'gtable',
  'stringr'
)
for (i in required_list) {
  if (i %in% installed_list) {
    print(paste(i,'has been installed'))
  }
  else{
    print('----------------------')
    print(paste(i,'is not installed!!!!!!'))
    print('----------------------')
  }
}
```

To install 'Rcirc' for R, try to open Rstudio and input:
```R
# install devtools
install.packages('devtools')
library(devtools)  

# install Rcirc
install_github('PSSUN/Rcirc')
```
