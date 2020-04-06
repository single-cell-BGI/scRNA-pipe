# A WDL-based pipeline to process DNBelab C4 fastq to gene expression matrix

## News
* v0.5, Update PISA to v0.2, STAR to 2.7.3a
* Aug. 2019, v0.1


## Prepare the software and data

- *Language* Workflow Description Language (WDL) and R scripts. 
- *Hardware/Software requirements* 
  - x86-64 compatible processors
  - require at least 16GB of RAM, ideally 32GB. 
  - 64bit Linux 


## Third party softwars
* [java](www.java.com)
* [Cromwell](https://github.com/broadinstitute/cromwell/releases)
* [R](https://www.r-project.org/)  (3.5+) #  with following R packages installed
  * ggplot2
  * getopt
  * cowplot
  * DropletUtils


## Downlod the lastest binary [release]() and uncompress it.

Directory contents
- *bin*  pre-compiled executables for Linux
- *config*  read structure configure files
- *pipelines*  WDL pipeline
- *scripts*  miscellaneous scripts


## A tiny dataset

- Step 0: Build reference index
```
$ cd example/tiny_datasets

# Create fold for star index
$ mkdir ref/star
$ STAR --runThreadN 4 --runMode genomeGenerate --genomeDir ref/star --genomeFastaFiles ref/fasta/genome.fa --genomeSAindexNbases 11
...
Aug 18 20:34:27 ..... finished successfully 
```
- Step 1: Setup configure file.
```
# Check configure file
$ cat config.json
  {
      "main.ID": "tiny",
      "main.fastq1": "Path to  example/tiny_datasets/fastq/read_1.fastq.gz", 
      "main.fastq2": "Path to example/tiny_datasets/fastq/read_2.fastq.gz",
      "main.outdir": "Path to example/tiny_datasets/result",
      "main.root": "Path to this repo",
      "main.config": "Path /config/Testdata_ReadStruct.json",
      "main.Rscript": "Path to Rscript",
      "main.gtf": "Path to example/tiny_datasets/ref/genes/genes.gtf.gz",
      "main.refdir": "Path to example/tiny_datasets/ref/star"
  }
  
```
- Step 2:  Run this pipeline.

```
java -jar cromwell-35.jar run -i config.json  scRNA_pipe.wdl
```

- Step 3: a Cell X Gene digit matrix will be created at outs/


- Step 4: Seconday analysis from Cell X gene digit expression matrix.


# License
MIT
