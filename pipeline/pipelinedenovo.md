# Brazilian Symposium on Bioinformatics 2018

## MC3 - Bioinformática básica

Este workflow consiste em uma montagem de novo de um isolado da bactéria Enterobacter kobei, a qual é multiresistente a drogas.
O DNA da E. kobei foi sequenciado usando a plataforma Illumina HiSeq, gerando reads com 100 bp paired-end [1].

### Obtendo os dados de sequenciamento
* wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR885/ERR885455/ERR885455_1.fastq.gz
* wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR885/ERR885455/ERR885455_2.fastq.gz

### Filtragem com Trimmomatic [2]
* java -jar Trimmomatic-0.36/trimmomatic-0.36.jar PE -phred33 ERR885455_1.fastq.gz ERR885455_2.fastq.gz  ERR885455_1_FILTERED.fastq ERR885455_1_UNPAIRED.fastq   ERR885455_2_FILTERED.fastq ERR885455_2_UNPAIRED.fastq ILLUMINACLIP:Trimmomatic-0.36/adapters/TruSeq3-PE.fa:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36 -validatePairs

### Montagem com Spades [2]
* python3 Spades/bin/spades.py --pe1-1 ERR885455_1_FILTERED.fastq --pe1-2 ERR885455_2_FILTERED.fastq --careful --only-assembler --cov-cutoff auto -t 2 -o minha_montagem

### Relatório de resultados da montagem com Quast [4]
* python Quast/quast.py -o ERR885455_stats minha_montagem/scaffolds.fasta 

## Referências

[1] Kim Judge, Martin Hunt, Sandra Reuter, Alan Tracey, Michael A Quail,
Julian Parkhill, and Sharon J Peacock. Comparison of bacterial genome
assembly software for minion data and their applicability to medical micro-
biology. Microbial genomics, 2(9), 2016.

[2] Anthony M Bolger, Marc Lohse, and Bjoern Usadel. Trimmomatic: a flexible
trimmer for illumina sequence data. Bioinformatics, 30(15):2114–2120, 2014.

[3] Anton Bankevich, Sergey Nurk, Dmitry Antipov, Alexey A Gurevich,
Mikhail Dvorkin, Alexander S Kulikov, Valery M Lesin, Sergey I Nikolenko,
Son Pham, Andrey D Prjibelski, et al. Spades: a new genome assembly
algorithm and its applications to single-cell sequencing. Journal of compu-
tational biology, 19(5):455–477, 2012.

[4] Alexey Gurevich, Vladislav Saveliev, Nikolay Vyahhi, and Glenn Tesler.
Quast: quality assessment tool for genome assemblies. Bioinformatics,
29(8):1072–1075, 2013.

