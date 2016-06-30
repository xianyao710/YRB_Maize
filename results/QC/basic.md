#This file describes the trimmning process on CAGE reads retrieved from Bo73 and Mo17 shoots and roots tissues.

##raw data and processed data statistics

|sample_id   | read_id 			 | read_counts | barcode |read_counts after trimming|read_counts after cut|
|------------|:----------------:|------------:|---------|-----------|---------|
|Bo73 shoot1 |SRR2078285.fastq  |	11,111,236 |GAT|10696868|10180236|
|Bo73 shoot2 |SRR2078286.fastq  |	7,062,416 |ACA|6749262|5566704|
|Bo73 root1	 |SRR2078287.fastq |	7,226,801|ACT|6933951|5988163|
|Bo73 root2	 |SRR2078288.fastq|	5,663,024|ACG|5444756|4645246|
|Mo17 shoot1  |SRR2078289.fastq|	9,871,904|AGA|9171255|7316461|
|Mo17 shoot2|SRR2078290.fastq|	16,304,719|ATC|15609514|11927809|
|Mo17 shoot3|SRR2078291.fastq|	13,697,357|ATG|7395652|6099676|
|Mo17 shoot4|SRR2078292.fastq|	11,925,108|CTT|11446751|9733753|
|In total||82,862,565|88.64%|73,448,009|61458048|

## Trimming procedure
1)remove 3'-linker TCGTATGCCGTCTT which lies on 37-50 bp region
cutadapt -a TCGTATGCCGTCTT -m 25
2)retrieve reads containing different barcode, throwing reads that don't start with barcode
fastx-barcode_splitter
3)trim 3'barcode + Ecol linker (CAGCAG) which lie on 1-9 bp region
cutadapt -g <9bp>  -m 25 -o .fastq --untrimmed-output .untrim

After this trimming process, around 27 bp reads should be produced. 





