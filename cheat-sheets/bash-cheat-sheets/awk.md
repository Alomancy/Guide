# Awk

## Awk

### **Set tab as field separator**

```text
awk -F $'\t'
```

### **Output as tab separated \(also as field separator\)**

```text
awk -v OFS='\t'
```

### **Pass variable**

```text
a=bbo;b=obb;
awk -v a="$a" -v b="$b" "$1==a && $10=b" filename
```

### **Print line number and number of characters on each line**

```text
awk '{print NR,length($0);}' filename
```

### **Find number of columns**

```text
awk '{print NF}'
```

### **Reverse column order**

```text
awk '{print $2, $1}'
```

### **Check if there is a comma in a column \(e.g. column $1\)**

```text
awk '$1~/,/ {print}'
```

### **Split and do for loop**

```text
awk '{split($2, a,",");for (i in a) print $1"\t"a[i]}' filename
```

### **Print all lines before nth occurrence of a string \(e.g stop print lines when 'bbo' appears 7 times\)**

```text
awk -v N=7 '{print}/bbo/&& --N<=0 {exit}'
```

### **Print filename and last line of all files in directory**

```text
ls|xargs -n1 -I file awk '{s=$0};END{print FILENAME,s}' file
```

### **Add string to the beginning of a column \(e.g add "chr" to column $3\)**

```text
awk 'BEGIN{OFS="\t"}$3="chr"$3'
```

### **Remove lines with string \(e.g. 'bbo'\)**

```text
awk '!/bbo/' file
```

### **Remove last column**

```text
awk 'NF{NF-=1};1' file
```

### **Usage and meaning of NR and FNR**

```text
# For example there are two files:
# fileA:
# a
# b
# c
# fileB:
# d
# e
awk 'print FILENAME, NR,FNR,$0}' fileA fileB
# fileA    1    1    a
# fileA    2    2    b
# fileA    3    3    c
# fileB    4    1    d
# fileB    5    2    e
```

### **AND gate**

```text
# For example there are two files:
# fileA:
# 1    0
# 2    1
# 3    1
# 4    0
# fileB:
# 1    0
# 2    1
# 3    0
# 4    1

awk -v OFS='\t' 'NR=FNR{a[$1]=$2;next} NF {print $1,((a[$1]=$2)? $2:"0")}' fileA fileB
# 1    0
# 2    1
# 3    0
# 4    0
```

### **Round all numbers of file \(e.g. 2 significant figure\)**

```text
awk '{while (match($0, /[0-9]+\[0-9]+/)){
    \printf "%s%.2f", substr($0,0,RSTART-1),substr($0,RSTART,RLENGTH)
    \$0=substr($0, RSTART+RLENGTH)
    \}
    \print
    \}'
```

### **Give number/index to every row**

```text
awk '{printf("%s\t%s\n",NR,$0)}'
```

### **Break combine column data into rows**

```text
# For example, seperate the following content:
# David    cat,dog
# into
# David    cat
# David    dog

awk '{split($2,a,",");for(i in a)print $1"\t"a[i]}' file

# Detail here:　http://stackoverflow.com/questions/33408762/bash-turning-single-comma-separated-column-into-multi-line-string
```

### **Average a file \(each line in file contains only one number\)**

```text
awk '{s+=$1}END{print s/NR}'
```

### **Print field start with string \(e.g Linux\)**

```text
awk '$1 ~ /^Linux/'
```

### **Sort a row \(e.g. 1 40 35 12 23 --&gt; 1 12 23 35 40\)**

```text
awk ' {split( $0, a, "\t" ); asort( a ); for( i = 1; i <= length(a); i++ ) printf( "%s\t", a[i] ); printf( "\n" ); }'
```

### **Subtract previous row values \(add column6 which equal to column4 minus last column5\)**

```text
awk '{$6 = $4 - prev5; prev5 = $5; print;}'
```

