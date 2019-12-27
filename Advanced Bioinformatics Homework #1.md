#Jad Elgaali
#Bioinformatics Homework #1 
#4/20/19

1 Download the Generic Feature Format (GFF) version of the Saccharomyces Cerevisiae yeast genome to your home directory.

```
[t.cri.biowksp17@cri16in001 ~]$ wget http://downloads.yeastgenome.org/curation/chromosomal_feature/saccharomyces_cerevisiae.gff

--2019-04-16 11:10:57--  http://downloads.yeastgenome.org/curation/chromosomal_feature/saccharomyces_cerevisiae.gff
Resolving downloads.yeastgenome.org... 171.67.205.104
Connecting to downloads.yeastgenome.org|171.67.205.104|:80... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://downloads.yeastgenome.org/curation/chromosomal_feature/saccharomyces_cerevisiae.gff [following]
--2019-04-16 11:10:57--  https://downloads.yeastgenome.org/curation/chromosomal_feature/saccharomyces_cerevisiae.gff
Connecting to downloads.yeastgenome.org|171.67.205.104|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 18136762 (17M)
Saving to: `saccharomyces_cerevisiae.gff.8'

100%[=================================================================================================================>] 18,136,762  17.8M/s   in 1.0s    

2019-04-16 11:10:58 (17.8 MB/s) - `saccharomyces_cerevisiae.gff.8' saved [18136762/18136762]
```

2 Using the Linux command line, answer the following questions:

a. How many genes are there in the data?

```
grep "gene" saccharomyces_cerevisiae.gff.4 | wc -l
7277

```
b. How many genes are there on chromosome 2?

```
grep "\chrII\b" saccharomyces_cerevisiae.gff.5 | grep "gene" | wc -l
485
```
c. How many mRNAs are there on chromosome 10?

```
grep "\chrX\b" saccharomyces_cerevisiae.gff.5 | grep "mRNA" | wc -l
846
```

d. Describe what the following command do: sed '/#/d' saccharomyces_cerevisiae.gff > features.gff

```
#This command takes some lines from the initial file
"saccharomyces_cerevisiae.gff" and makes a new file from
containing those lines which is called "features.gff".
```

e. How many features (lines) are there in the file features.gff

```
[t.cri.biowksp17@cri16in001 ~]$ wc -l features.gff 
175048 features.gff
```
f. Describe what the following command do: cut -f 1 features.gff | sort | uniq -c | sort -k1n

```
#To begin the "cut -f 1 features.gff" portion extracts the
column 1 (field) of the file features.gff, then that output
piped into sort, and after being sorted, that output is then
piped into the "uniq -c" which detects adjacent duplicates
and then the -c counts how many times the line was duplicated
and displays that to the left of the field, then the "sort -k1n"
sorts the table by the first column in numerical order, so from 
the least to most number of unique reads for each chromosome. 
Here was the end of the output with the numerically sorted data:
    214 chrmt
    424 chrI
    532 chrVI
    700 chrIII
    838 chrIX
   1118 chrVIII
   1156 chrV
   1171 chrXI
   1389 chrX
   1476 chrXIV
   1556 chrII
   1766 chrXIII
   1770 chrXVI
   2007 chrXV
   2049 chrXII
   2053 chrVII
   2839 chrIV
```
g. Which chromosome is the longest and which one is the shortest?

```
#chrmt is the shortest and chrIV is the longest
[t.cri.biowksp17@cri16in001 ~]$ grep "\<chromosome\>" saccharomyces_cerevisiae.gff.9 | cut -f 1,5 | sort -k2n
chrmt	85779
chrI	230218
chrVI	270161
chrIII	316620
chrIX	439888
chrVIII	562643
chrV	576874
chrII	628309
chrXI	666816
chrX	745751
chrXIV	784333
chrII	813184
chrXIII	924431
chrXVI	948066
chrXII	1078177
chrVII	1090940
chrXV	1091291
chrIV	1531933
```
h. Describe what the following command do: sed 's/chrI/chr1/g' features.gff > new_features.gff

```
#This command replaces all occurances of chrI with chr1 and 
makes a new file out of that data in a new file called
"new_features.gff".
```
 
3 Develop a Linux Shell script to generate the first n numbers of the Fibonacci series.

```
#shell script

echo "How many Fibonacci numbers would you like?"
read num
a=0
b=1
i=2
echo "Here are your $num Fibonacci numbers: "
echo "$a"
echo "$b"
while [ $i -lt $num ]
do
  	i=`expr $i + 1`
	c=`expr $a + $b`
echo $c
a=$b
b=$c
done

#execution

[t.cri.biowksp17@cri16in001 ~]$ nano fibonacci.sh 
[t.cri.biowksp17@cri16in001 ~]$ chmod u+x fibonacci.sh 
[t.cri.biowksp17@cri16in001 ~]$ ./fibonacci.sh
How many Fibonacci numbers would you like?
5
Here are your 5 Fibonacci numbers: 
0
1
1
2
3
[t.cri.biowksp17@cri16in001 ~]$ ./fibonacci.sh
How many Fibonacci numbers would you like?
12
Here are your 12 Fibonacci numbers: 
0
1
1
2
3
5
8
13
21
34
55
89
```
4 Measure and report the time it takes to execute your script

```
[t.cri.biowksp17@cri16in001 ~]$ time ./fibonacci.sh
How many Fibonacci numbers would you like?
5
Here are your 5 Fibonacci numbers: 
0
1
1
2
3

Wall Time	0m4.735s
User Mode	0m0.007s
Kernel Mode	0m0.012s
CPU Usage	0.40%
```
