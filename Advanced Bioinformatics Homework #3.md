#Jad Elgaali Advanced Bioinformatics Homework #3 5/2/19

Summary File

```
#!/bin/bash

mkdir RawReadQC/


job1=$(qsub KO1.pbs)
job2=$(qsub KO2.pbs)
job3=$(qsub KO3.pbs)
job4=$(qsub WT1.pbs)
job5=$(qsub WT2.pbs)
job6=$(qsub WT3.pbs)
echo $job1
echo $job2
echo $job3
echo $job4
echo $job5
echo $job6

```

K01 

```

#!/bin/bash
#PBS -N rnaseq01
#PBS -l mem=12gb,nodes=1:ppn=8,walltime=8:00:00
#PBS -e error-log-${PBS_JOBID}.txt
#PBS -o output-log-${PBS_JOBID}.txt
#-------------------------------------------------------------
# set working directory, resource directory, and load modules
#-------------------------------------------------------------

cd "$PBS_O_WORKDIR"

fastq_dir="/gpfs/data/mscbmi/rnaseq/fastq"
reference_dir="/gpfs/data/mscbmi/rnaseq/hg38"

module load gcc/6.2.0
module load udunits
module load java-jdk/1.8.0_92
module load samtools/1.6.0

module load fastqc/0.11.5
module load STAR/2.6.1d
module load subread/1.5.3

module load R/3.5.0


#-----------------------
# Quaality Control Using FastQC (output html)
#-----------------------


fastqc \
        --extract \
        -o RawReadQC/ \
        -t 6 \
	--nogroup \
        ${fastq_dir}/KO01.fastq.gz \

        #-----------------------
# Transcriptional Quantification Using Psuedo-alignment Tool kallisto
#-----------------------

mkdir -p \
	Quant/KO01
	
kallisto \
	quant \
        --index=${reference_dir}/transcripts.idx \
        --output-dir=Quant/KO01 \
        --single \
        --fragment-length=180 \
        --sd=20 \
        --threads=8 \
        ${fastq_dir}/KO01.fastq.gz

```

K02

```
#!/bin/bash


#PBS -N rnaseq02
#PBS -l mem=12gb,nodes=1:ppn=8,walltime=8:00:00
#PBS -e error-log-${PBS_JOBID}.txt
#PBS -o output-log-${PBS_JOBID}.txt

#-------------------------------------------------------------
# set working directory, resource directory, and load modules
#-------------------------------------------------------------

cd "$PBS_O_WORKDIR"

fastq_dir="/gpfs/data/mscbmi/rnaseq/fastq"
reference_dir="/gpfs/data/mscbmi/rnaseq/hg38"


module load gcc/6.2.0
module load udunits
module load java-jdk/1.8.0_92
module load samtools/1.6.0

module load fastqc/0.11.5
module load STAR/2.6.1d
module load subread/1.5.3
module load kallisto/0.44.0

module load R/3.5.0


#-----------------------
# Quaality Control Using FastQC (output html)
#-----------------------


fastqc \
       --extract \
        -o RawReadQC/ \
        -t 6 \
	--nogroup \
        ${fastq_dir}/KO02.fastq.gz \




        #-----------------------
# Transcriptional Quantification Using Psuedo-alignment Tool kallisto
#-----------------------

mkdir -p \
	Quant/KO02
	
kallisto \
	quant \
        --index=${reference_dir}/transcripts.idx \
        --output-dir=Quant/KO02 \
        --single \
        --fragment-length=180 \
        --sd=20 \
        --threads=8 \
        ${fastq_dir}/KO02.fastq.gz

```

K03

```
#!/bin/bash


#PBS -N rnaseq03
#PBS -l mem=12gb,nodes=1:ppn=8,walltime=8:00:00
#PBS -e error-log-${PBS_JOBID}.txt
#PBS -o output-log-${PBS_JOBID}.txt

#-------------------------------------------------------------
# set working directory, resource directory, and load modules
#-------------------------------------------------------------

cd "$PBS_O_WORKDIR"

fastq_dir="/gpfs/data/mscbmi/rnaseq/fastq"
reference_dir="/gpfs/data/mscbmi/rnaseq/hg38"


module load gcc/6.2.0
module load udunits
module load java-jdk/1.8.0_92
module load samtools/1.6.0

module load fastqc/0.11.5
module load STAR/2.6.1d
module load subread/1.5.3
module load kallisto/0.44.0

module load R/3.5.0


#-----------------------
# Quaality Control Using FastQC (output html)
#-----------------------


fastqc \
       --extract \
        -o RawReadQC/ \
        -t 6 \
	--nogroup \
        ${fastq_dir}/KO03.fastq.gz \




        #-----------------------
# Transcriptional Quantification Using Psuedo-alignment Tool kallisto
#-----------------------

mkdir -p \
	Quant/KO03
	
kallisto \
	quant \
        --index=${reference_dir}/transcripts.idx \
        --output-dir=Quant/KO03 \
        --single \
        --fragment-length=180 \
        --sd=20 \
        --threads=8 \
        ${fastq_dir}/KO03.fastq.gz

```

WT01

```
#!/bin/bash


#PBS -N rnaseq04
#PBS -l mem=12gb,nodes=1:ppn=8,walltime=8:00:00
#PBS -e error-log-${PBS_JOBID}.txt
#PBS -o output-log-${PBS_JOBID}.txt

#-------------------------------------------------------------
# set working directory, resource directory, and load modules
#-------------------------------------------------------------

cd "$PBS_O_WORKDIR"

fastq_dir="/gpfs/data/mscbmi/rnaseq/fastq"
reference_dir="/gpfs/data/mscbmi/rnaseq/hg38"


module load gcc/6.2.0
module load udunits
module load java-jdk/1.8.0_92
module load samtools/1.6.0

module load fastqc/0.11.5
module load STAR/2.6.1d
module load subread/1.5.3
module load kallisto/0.44.0

module load R/3.5.0


#-----------------------
# Quaality Control Using FastQC (output html)
#-----------------------


fastqc \
       --extract \
        -o RawReadQC/ \
        -t 6 \
	--nogroup \
        ${fastq_dir}/WT01.fastq.gz \




        #-----------------------
# Transcriptional Quantification Using Psuedo-alignment Tool kallisto
#-----------------------

mkdir -p \
	Quant/WT01
	
kallisto \
	quant \
        --index=${reference_dir}/transcripts.idx \
        --output-dir=Quant/WT01 \
        --single \
        --fragment-length=180 \
        --sd=20 \
        --threads=8 \
        ${fastq_dir}/WT01.fastq.gz

```

WT02

```
#!/bin/bash


#PBS -N rnaseq05
#PBS -l mem=12gb,nodes=1:ppn=8,walltime=8:00:00
#PBS -e error-log-${PBS_JOBID}.txt
#PBS -o output-log-${PBS_JOBID}.txt

#-------------------------------------------------------------
# set working directory, resource directory, and load modules
#-------------------------------------------------------------

cd "$PBS_O_WORKDIR"

fastq_dir="/gpfs/data/mscbmi/rnaseq/fastq"
reference_dir="/gpfs/data/mscbmi/rnaseq/hg38"


module load gcc/6.2.0
module load udunits
module load java-jdk/1.8.0_92
module load samtools/1.6.0

module load fastqc/0.11.5
module load STAR/2.6.1d
module load subread/1.5.3
module load kallisto/0.44.0

module load R/3.5.0


#-----------------------
# Quaality Control Using FastQC (output html)
#-----------------------


fastqc \
       --extract \
        -o RawReadQC/ \
        -t 6 \
	--nogroup \
        ${fastq_dir}/WT02.fastq.gz \




        #-----------------------
# Transcriptional Quantification Using Psuedo-alignment Tool kallisto
#-----------------------

mkdir -p \
	Quant/WT02
	
kallisto \
	quant \
        --index=${reference_dir}/transcripts.idx \
        --output-dir=Quant/WT02 \
        --single \
        --fragment-length=180 \
        --sd=20 \
        --threads=8 \
        ${fastq_dir}/WT02.fastq.gz

```
WT03

```
#!/bin/bash


#PBS -N rnaseq06
#PBS -l mem=12gb,nodes=1:ppn=8,walltime=8:00:00
#PBS -e error-log-${PBS_JOBID}.txt
#PBS -o output-log-${PBS_JOBID}.txt

#-------------------------------------------------------------
# set working directory, resource directory, and load modules
#-------------------------------------------------------------

cd "$PBS_O_WORKDIR"

fastq_dir="/gpfs/data/mscbmi/rnaseq/fastq"
reference_dir="/gpfs/data/mscbmi/rnaseq/hg38"


module load gcc/6.2.0
module load udunits
module load java-jdk/1.8.0_92
module load samtools/1.6.0

module load fastqc/0.11.5
module load STAR/2.6.1d
module load subread/1.5.3
module load kallisto/0.44.0

module load R/3.5.0


#-----------------------
# Quaality Control Using FastQC (output html)
#-----------------------


fastqc \
       --extract \
        -o RawReadQC/ \
        -t 6 \
	--nogroup \
        ${fastq_dir}/WT03.fastq.gz \




        #-----------------------
# Transcriptional Quantification Using Psuedo-alignment Tool kallisto
#-----------------------

mkdir -p \
	Quant/WT03
	
kallisto \
	quant \
        --index=${reference_dir}/transcripts.idx \
        --output-dir=Quant/WT03 \
        --single \
        --fragment-length=180 \
        --sd=20 \
        --threads=8 \
        ${fastq_dir}/WT03.fastq.gz

```

Second to last file

```                                


Rscript --vanilla \
        /gpfs/data/mscbmi/rnaseq/SRC/tximport.R


#-----------------------
# Sample Association Using PCA Plot
#-----------------------


Rscript --vanilla \
        /gpfs/data/mscbmi/rnaseq/SRC/pca.R


```




