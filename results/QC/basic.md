#This file describes the trimmning process on CAGE reads retrieved from Bo73 and Mo17 shoots and roots tissues.

##raw data and processed data statistics

|sample_id   | read_id 			 | read_counts |barcode|read_count after trim|
|------------|:----------------:|------------:|---------|
|B73 shoot1 |SRR2078285.fastq  |	11,111,236 |GAT|5168085|
|B73 shoot2 |SRR2078286.fastq  |	7,062,416 |ACA|3736846|
|B73 root1	 |SRR2078287.fastq |	7,226,801|ACT|2478794|
|B73 root2	 |SRR2078288.fastq|	5,663,024|ACG|1923501|
|Mo17 shoot1  |SRR2078289.fastq|	9,871,904|AGA|3786304|
|Mo17 shoot2|SRR2078290.fastq|	16,304,719|ATC|11182894|
|Mo17 shoot3|SRR2078291.fastq|	13,697,357|ATG|3810340|
|Mo17 shoot4|SRR2078292.fastq|	11,925,108|CTT|4972563|
|In total||82,862,565|44.72%|37059327|

## Trimming procedure
1)remove 3'-linker TCGTATGCCGTCTT which lies on 37-50 bp region
cutadapt -a TCGTATGCCGTCTT -m 25
2)retrieve reads containing different barcode, throwing reads that don't start with barcode
fastx-barcode_splitter
3)trim 3'barcode + Ecol linker (CAGCAG) which lie on 1-9 bp region
cutadapt -g <9bp>  -m 25 -o .fastq --untrimmed-output .untrim

After this trimming process, around 27 bp reads should be produced. 

##bwa alignment with Z.mays Reference genome  AGPv3.31
```
samtools flagstat <seq_id>.bam
```
|sample_id|mapped percentage|
|-----------|----------|
|B73 shoot1 |76.18%	    |
|B73 shoot2 |74.15%    |
|B73 root1  |74.34%    |
|B73 root2  |62.04%    |
|Mo17 shoot1|49.01%    |
|Mo17 shoot2|69.94%    | 
|Mo17 root1 |58.98%    |
|Mo17 root2 |71.32%    |

##filtering out rRNA contamination



