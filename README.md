# Various useful one liners

### 1) Read a comma delimited file on SNPs giving contig IDs, SNP positions etc, pull out surrounding +/- 250bp from the original contig, & write out to .fasta file
Change values as appropriate
Column 1 contains contig ID ($1)
Column 2 contains the SNP position ($2)
Get +/- 250 from appropriate contig in path/to/genome and write out to output.fasta file
```
awk -F ',' 'NR>1 {print $1, $2}' file_of_SNPs_to_extract.csv | while read var1 var2 ; do position1=$(($var2 - 250)) ; position2=$(($var2 + 250)) ; samtools faidx path/to/genome/ref_contigs.fasta $var1:$position1-$position2 >> output_file.fasta ; done
```


### 3) generate md5 for whole dir 
```
find <input_dir> -type f -exec md5sum {} + | awk '{print $1}' | sort | md5sum
```

