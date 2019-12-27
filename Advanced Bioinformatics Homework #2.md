Jad Elgaali Homework 2 4/27/19

Create an analysis pipeline that efficiently performs the raw data QC for heart and kidney files, then perform the mapping of those files using both bwa and bowtie2 tools.

shell script

```
#!/bin/bash
qsub run_fastqc_heart.pbs
sleep 2
qsub run_fastqc_kidney.pbs
sleep 2
qsub run_bwa_heart.pbs
sleep 2
qsub run_bwa_kidney.pbs
sleep 2
qsub run_bowtie2_heart.pbs
sleep 2
qsub run_bowtie2_kidney.pbs
```

execution

```
nano homework2.sh
./homework2.sh
watch qstat

Every 2.0s: qstat                                       Fri Apr 26 09:10:57 2019

Job ID                    Name             User            Time Use S Queue
------------------------- ---------------- --------------- -------- - -----
13324952.cri16sc001        run_fastqc_heart t.cri.biowksp17 00:00:13 C express

13324953.cri16sc001        ...fastqc_kidney t.cri.biowksp17        0 R express

13324954.cri16sc001        run_bwa_heart    t.cri.biowksp17 00:00:01 R standard

13324955.cri16sc001        run_bwa_kidney   t.cri.biowksp17        0 R standard

13324956.cri16sc001        ...bowtie2_heart t.cri.biowksp17        0 R standard

13324957.cri16sc001        ...owtie2_kidney t.cri.biowksp17        0 R standard
```

