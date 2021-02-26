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
tail -n +2 snp_position.txt | sort -k1,1 > sorted_snp_position.txt
```

Check if sorted, it is
```
sort -k1,1 -c sorted_transposed_header_maize_genotypes.txt
sort -k1,1 -c sorted_transposed_header_teosinte_genotypes.txt
sort -k1,1 -c sorted_snp_position.txt
```

Join files
```
join -1 1 -2 1 -t $'\t' sorted_snp_position.txt sorted_transposed_header_teosinte_genotypes.txt > teosinte_joined_file.txt
join -1 1 -2 1 -t $'\t' sorted_snp_position.txt sorted_transposed_header_maize_genotypes.txt > maize_joined_file.txt
```


###Teosinte
Awk out all the 40 files
Then use setd to change "?" to "-"
```
cat teosinte_joined_file.txt | awk '$3 = 1' > teosinte_chrom1.txt
cat teosinte_joined_file.txt | awk '$3 = 2' > teosinte_chrom2.txt
cat teosinte_joined_file.txt | awk '$3 = 3' > teosinte_chrom3.txt
cat teosinte_joined_file.txt | awk '$3 = 4' > teosinte_chrom4.txt
cat teosinte_joined_file.txt | awk '$3 = 5' > teosinte_chrom5.txt
cat teosinte_joined_file.txt | awk '$3 = 6' > teosinte_chrom6.txt
cat teosinte_joined_file.txt | awk '$3 = 7' > teosinte_chrom7.txt
cat teosinte_joined_file.txt | awk '$3 = 8' > teosinte_chrom8.txt
cat teosinte_joined_file.txt | awk '$3 = 9' > teosinte_chrom9.txt
cat teosinte_joined_file.txt | awk '$3 = 10' > teosinte_chrom10.txt

sed 's/?/-/' teosinte_joined_file.txt | awk '$3 = 1' > teosinte_chrom1_with_dash.txt
sed 's/?/-/' teosinte_joined_file.txt | awk '$3 = 2' > teosinte_chrom2_with_dash.txt
sed 's/?/-/' teosinte_joined_file.txt | awk '$3 = 3' > teosinte_chrom3_with_dash.txt
sed 's/?/-/' teosinte_joined_file.txt | awk '$3 = 4' > teosinte_chrom4_with_dash.txt
sed 's/?/-/' teosinte_joined_file.txt | awk '$3 = 5' > teosinte_chrom5_with_dash.txt
sed 's/?/-/' teosinte_joined_file.txt | awk '$3 = 6' > teosinte_chrom6_with_dash.txt
sed 's/?/-/' teosinte_joined_file.txt | awk '$3 = 7' > teosinte_chrom7_with_dash.txt
sed 's/?/-/' teosinte_joined_file.txt | awk '$3 = 8' > teosinte_chrom8_with_dash.txt
sed 's/?/-/' teosinte_joined_file.txt | awk '$3 = 9' > teosinte_chrom9_with_dash.txt
sed 's/?/-/' teosinte_joined_file.txt | awk '$3 = 10' > teosinte_chrom10_with_dash.txt
```
###Maize
Awk out all the 40 files
Then use setd to change "?" to "-"
```
cat maize_joined_file.txt | awk '$3 = 1' > maize_chrom1.txt
cat maize_joined_file.txt | awk '$3 = 2' > maize_chrom2.txt
cat maize_joined_file.txt | awk '$3 = 3' > maize_chrom3.txt
cat maize_joined_file.txt | awk '$3 = 4' > maize_chrom4.txt
cat maize_joined_file.txt | awk '$3 = 5' > maize_chrom5.txt
cat maize_joined_file.txt | awk '$3 = 6' > maize_chrom6.txt
cat maize_joined_file.txt | awk '$3 = 7' > maize_chrom7.txt
cat maize_joined_file.txt | awk '$3 = 8' > maize_chrom8.txt
cat maize_joined_file.txt | awk '$3 = 9' > maize_chrom9.txt
cat maize_joined_file.txt | awk '$3 = 10' > maize_chrom10.txt

sed 's/?/-/' maize_joined_file.txt | awk '$3 = 1' > maize_chrom1_with_dash.txt
sed 's/?/-/' maize_joined_file.txt | awk '$3 = 2' > maize_chrom2_with_dash.txt
sed 's/?/-/' maize_joined_file.txt | awk '$3 = 3' > maize_chrom3_with_dash.txt
sed 's/?/-/' maize_joined_file.txt | awk '$3 = 4' > maize_chrom4_with_dash.txt
sed 's/?/-/' maize_joined_file.txt | awk '$3 = 5' > maize_chrom5_with_dash.txt
sed 's/?/-/' maize_joined_file.txt | awk '$3 = 6' > maize_chrom6_with_dash.txt
sed 's/?/-/' maize_joined_file.txt | awk '$3 = 7' > maize_chrom7_with_dash.txt
sed 's/?/-/' maize_joined_file.txt | awk '$3 = 8' > maize_chrom8_with_dash.txt
sed 's/?/-/' maize_joined_file.txt | awk '$3 = 9' > maize_chrom9_with_dash.txt
sed 's/?/-/' maize_joined_file.txt | awk '$3 = 10' > maize_chrom10_with_dash.txt
```

###Maize
Unknown SNPs
```
awk -F '\t' '$4 == "unknown"' maize_joined_file.txt > unknown_maize_joined_file.txt
```

Multiple Position SNPs
```
awk -F '\t' '$4 == "multiple"' maize_joined_file.txt > multiple_maize_joined_file.txt
```


###Teosinte
Unknown SNPs
```
awk -F '\t' '$4 == "unknown"' teosinte_joined_file.txt > unknown_teosinte_joined_file.txt
```

Multiple Position SNPs
```
awk -F '\t' '$4 == "multiple"' teosinte_joined_file.txt > multiple_teosinte_joined_file.txt
```
