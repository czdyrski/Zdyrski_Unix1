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

```
awk -f transpose.awk fang_et_al_genotypes.txt > transposed_genotypes.txt

```

First transpose the genotype file to swap the rows and columns
Then, sort both files
Join the files
Awk out all teh 40 files
Then use setd to change ? to something

###Teosinte Data

```
here is my snippet of code used for data processing
```

Here is my brief description of what this code does
