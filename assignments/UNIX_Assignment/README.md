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

grep out teosinte (ZMPBA, ZMPIL, and ZMPJA) and maize (ZMMIL OR ZMMLR OR ZMMMR )
```
grep ZMM fang_et_al_genotypes.txt > maize_genotypes.txt
grep ZMP fang_et_al_genotypes.txt > teosinte_genotypes.txt
```

Put header in own file
```
head -n 1 fang_et_al_genotypes.txt > header_genotypes.txt
```

add headers to both teosinte and maize files
```
cat header_genotypes.txt maize_genotypes.txt > header_maize_genotypes.txt
cat header_genotypes.txt teosinte_genotypes.txt > header_teosinte_genotypes.txt
```

Transpose both genotype files to swap the rows and columns

```
awk -f transpose.awk header_maize_genotypes.txt > transposed_header_maize_genotypes.txt
awk -f transpose.awk header_teosinte_genotypes.txt > transposed_header_teosinte_genotypes.txt
```

Sort genotpye + snp file based off column 1, "SNP_ID"
```
sort -k1,1 transposed_header_maize_genotypes.txt >  sorted_transposed_header_maize_genotypes.txt
sort -k1,1 transposed_header_teosinte_genotypes.txt >  sorted_transposed_header_teosinte_genotypes.txt
sort -k1,1 snp_position.txt > sorted_snp_position.txt
```

Check if sorted, it is
```
sort -k1,1 -c sorted_transposed_header_maize_genotypes.txt
sort -k1,1 -c sorted_transposed_header_teosinte_genotypes.txt
sort -k1,1 -c sorted_snp_position.txt
```

Join files
```
join -1 1 -2 1 -t '\t' sorted_snp_position.txt sorted_transposed_header_maize_genotypes.txt > maize_joined_file.txt
join -1 1 -2 1 -t '\t' sorted_snp_position.txt sorted_transposed_header_teosinte_genotypes.txt > teosinte_joined_file.txt
```




Get rid of both headers
```
tail -n +3 transposed_genotypes.txt > headerless_transposed_genotypes.txt
tail -n +2 snp_position.txt > headerless_snp_position.txt
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
