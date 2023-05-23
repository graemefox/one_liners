# Various useful one liners

### 1) Read a comma delimited file on SNPs giving contig IDs, SNP positions etc, pull out surrounding +/- 250bp from the original contig, & write out to .fasta file
Change values as appropriate
Column 1 contains contig ID ($1)
Column 2 contains the SNP position ($2)
Get +/- 250 from appropriate contig in path/to/genome and write out to output.fasta file
```
awk -F ',' 'NR>1 {print $1, $2}' file_of_SNPs_to_extract.csv | while read var1 var2 ; do position1=$(($var2 - 250)) ; position2=$(($var2 + 250)) ; samtools faidx path/to/genome/ref_contigs.fasta $var1:$position1-$position2 >> output_file.fasta ; done
```


### 2) generate md5 for whole dir 
```
find <input_dir> -type f -exec md5sum {} + | awk '{print $1}' | sort | md5sum
```

### 3) calculate binary md5 and convert to base64 (Azure blobs use base64)
```
md5sum --binary <input_file> | awk '{print $1}' | xxd -p -r | base64
```

### 4) Merge multiple .fq.gz with the same file name stem. I.e. get L001 - L004 for a single sample.
```
# pass file_list.txt of the file name stems (the common bit)
while read file ; do out=_merged_R1.fq.gz ; echo $file ; zcat $file* | gzip > $file$out ; done < file_list.txt
```

### 5) Attach to a running slurm job
```
srun --pty --jobid $JOBID /bin/bash
```

