# Usage
The package provides numerous analyses for both upstream and downstream research, including circRNA detection, coding ability identification, single feature analyses and visualization of meta-features. Furthermore, the users can visualize the read mapping for each back-splice junction of circRNA by using Rcirc with sequencing data.  

**NOTE:** Many functions require gff files as input. Make sure there are no lines in the gff file that begin with '#'.

## Download data

**downloadCircRNA()** can help to download the circRNA data from published database, usage:

```R
# download
downloadCircRNA(speices = 'ath', out = '/path/to/out/file') 

# Note: speices should bed one of: 'ath' 'zma' 'asa' 'mm10' 'rat' 'zeb' 'fly' 'worm'.
```
 

## Prediction

**TranslateCirc()** can help to deal raw data and map to circRNA genome.
```R
# load the data
out = '/path/to/output/bam/file'
fastq = '/path/to/Ribo-seq/fastq'
adapter = '/path/to/adapter'
trimmomatic = '/path/to/trimmomatic/jre/file'
genome = '/path/to/genome'
tmp = '/path/to/tmp/file'
circgenome = '/path/to/circRNA/genome'
rRNA = '/path/to/rRNA'

# analysis
TranslateCirc(out,fastq,adapter,trimmomatic,genome,tmp,circgenome,rRNA)
```


**PredictCirc()** can help to predict circRNA by RNA-seq data.

```R
# load the data
sam = '/path/to/sam/file'
fa = '/path/to/fasta/file'
out = '/path/to/output/floder'
gtf = '/path/to/genome/gtf/file'  

# analysis
PredictCirc(sam = sam, fa = fa, out = out, gtf = gtf)

```

## Downstream analysis

**NOTE:** Many functions require gff files as input. Make sure there are no lines in the gff file that begin with '#'.

### Find the stem-ring structure

**stemRing()** function can help to find out the stem-ring stucture from the given **circRNAs bed file** and **genome fasta file** by compare the upstream and downstrean sequence. It can output a csv file which contains all the information.

```R
# load the data
circbed = '/path/to/circRNA/bed/file'
genomefasta = '/path/to/genome/fasta/file'
out = '/path/to/the/output/file'  
len = 1000   # The length (bp) of upstream and downstream to find the stem-ring structure

# analysis
stemRing(circbed = circbed, genomefasta = genomefasta, out = out)
```

### View the splice-signal
**showJunction()** can help to check the splice-signal from given circRNAs and draw a barplot by **circRNA fasta file**.
```R
# load the data
data = '/path/to/circRNA/fasta/file'  
max = 30  # the number of splice-signal types to show in barplot

# analysis
showJunction(data = data, max = 30)
```

### View the codon
**showCodon()** can help to display triplet codon composition frequency.
```R
# load the data
x = '/path/to/circRNA/fasta/file'  

# analysis
showCodon(x = x)
```


### Analysis the type distribution
**classByType()** can help to classify the given circRNAs into different type, you need to input **2** file to run this function: **circRNA bed file** and **genome annotation file** in gff format.

```R
# load the data
circbed = '/path/to/circRNA/bed/file/'
gff = '/path/to/genome/gff/file'  

# analysis
classByType(circbed = circbed, gff = gff)

```

### View the meta-feature
Rcirc can help to veiw the meta-feature of mount of circRNA by the function **showOverview()**, include their distribution, length and so on. In this function, you need to input **5** parameter: *circbed*, *genomefasta*, *gff*, *ribo* and *rna*.  

```R
# load the data
circbed = '/path/to/circRNA/bed/file/'
gff = '/path/to/genome/gff/file'  
genomefasta = '/path/to/genome/fasta'
# you can use 'bedtools bamtobed' to transform 'bam file' to 'bed file'
ribo = '/path/to/ribo-seq/bed/file'   # A bed file from bam file that align Ribo-seq data to genome
rna = '/path/to/rna-seq/bed/file'     # A bed file from bam file that align RNA-seq data to genome

# analysis 
showOverview(circbed = circbed,
 	gff = gff,
 	genomefasta = genomefasta,
 	ribo = ribo, 
 	rna = rna
)
```

### Analysis the reads mapping on sequences
You can use **circ_summary()** to analyse the mapping situation, it need **2** file as input: *bam* file and *gff* file,The bam file is obtained by aligning the Ribo-seq data to the virtual genome. The creation of the virtual genome can be automatically performed by the **makeGenome()** function. The gff file is automatically generated when **makeGenome()** creates the virtual genome.   

```R
# load the data
bam = '/path/to/bam/file'
gff = '/path/to/gff/file'  

# analysis 
summary <- circ_summary(bamfile = bam, gff = gff)
```

*summary* is a dataframe which contains all the information of mapping reads, *summary* can also be used as the input of function **mappingPlot()**.

### View the mapping result of single circRNA
Rcirc can also help to view the mapping situation on sequences like IGV by the function **mappingPlot()**, it can show each reads that mapped to junction site, you need **2** file as input: **virtual genome fasta** file and *summary*, usage:  

```R
# load data, note: this 2 file are generated by function makeGenome()
# bam file is the result that map the ribo-seq reads to virtual genome file.
# Ribo-seq data can get from RPFdb
fa = '/path/to/virtual/genome/fasta/file'
gff = '/path/to/gff/file/of/virtual/genome/fasta/file'
summary <- circ_summary(bamfile = bam, gff = gff)  

# parameter
index = 1         # The index of circRNA you want to view 
upstream = 100    # Upstream distance to junction (bp)
downstream = 100  # Downstream distance to junction (bp)
  
# analysis  
pic <- showMapping(summary = summary,
                   circ_index = index,
 	           genomefile = fa,
		   upstream = upstream,
		   downstream = downstream,
                   style = 'aside'
)
```






