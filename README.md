# curated_databse
**Curating a tblastn database** 

First concatenate the downlaoded genomes into a single fna file 
```
cat *.fna > database.fna
```
Then denote the single file as a nucleotide blast database, this will provide you with serveral output files 
```
makeblastdb -in database.fna -dbtype nucl
```

**Preforming a blast search**
Depending on whether you want to query with amino acid or nucleotide sequenced you can run respective blast options.
If you have individual text files with amino acid sequences in and you want to compare this against a nucloetide database then you would run tblastn. The flags of the command can be altered baased on what output you desire, additionally a e-value cut-off can be implemented to reduce low quality hits. The output should be presented in an tabulated file that can be opened as a csv file for easy annotation. 

```
tblastn -query query.fasta -db database -outfmt 6 -num_threads 3 -max_target_seqa 2000 -out DB.tab
```

**Matching contig name to accession name**
The above tblastn search will retrieve a match for the contig name and not produce the associated accession name. Therefore you will need to match up the contig to the accession number yourself by preformining an grep and echo script

```
#!/bin/bash
while read line;
do
genome=$(grep $line .*fna | cut -f1 -d':')
echo $line $genome >> capA_contig_and_accession
echo $line $genome
done <capA_contig
```

**Using excel to match genome information**
```
=RIGHT(A1, LEN(A1)-SEARCH(" ",A1))
=LEFT(B1,15)
```
```
=MATCH(H1,$F$1:$f$1000,0)
=INDEX($B$1:$B$1000,1)
```

You can edit this accordingly with the genome informatin you need. It will be useful to match the contig name to the accession name and the species. 
From here you can set coverage and percentage identity to the refernce cut-offs. 

**Pulling a gene from a genome file***




