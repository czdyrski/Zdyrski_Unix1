#Zdyrski_Unix_HW
#UNIX Assignment

##Data Inspection

###Attributes of `fang_et_al_genotypes`

```
wc fang_et_al_genotypes.txt
du -h fang_et_al_genotypes.txt
grep -v "^#" fang_et_al_genotypes.txt | awk -F "\t" '{print NF; exit}'
```

By inspecting this file I learned that:

1. The file size is 6.1M.
2. There are 2783 lines, 2744038 words and 11051939 bytes.
3. There are 986 columns in this file.

###Attributes of `snp_position.txt`

```
wc snp_position.txt
du -h snp_position.txt
grep -v "^#" snp_position.txt | awk -F "\t" '{print NF; exit}'
```

By inspecting this file I learned that:

1. The file size is 38K.
2. There are 984 lines, 13198 words and 82763 bytes.
3. There are 15 columns in this file.

##Data Processing

###Maize Data

First transpose the genotype file to swap the rows and columns

```
awk -f transpose.awk fang_et_al_genotypes.txt > transposed_genotypes.txt
```

Check if sorted, its not
```
sort -c snp_position.txt
```

Sort snp file based off column 1, "SNP_ID"
```
sort -k1,1n snp_position.txt > sorted_snp_position.txt^C
```

Sort file based off column 1, "SNP_ID"
```
sort -k1,1n transposed_genotypes.txt > sorted_transposed_genotypes.txt
```

Get rid of both headers
```
tail -n +3 sorted_transposed_genotypes.txt > headerless_sorted_transposed_genotypes.txt
tail -n +2 sorted_snp_position.txt > headerless_sorted_snp_position.txt
```

Join files
```
join -1 1 -2 1 -t '\t' headerless_sorted_snp_position.txt headerless_sorted_transposed_genotypes.txt > joined_file.txt
```

Awk out all the 40 files
```
awk something joined_file.txt
```
Then use setd to change "?" to "-"
```
sed 's/?/-/g' joined_file.txt

```
###Teosinte Data
