# Sed

## Sed

### **Remove the 1st line**

```text
sed 1d filename
```

### **Remove the first 100 lines \(remove line 1-100\)**

```text
sed 1,100d filename
```

### **Remove lines with string \(e.g. 'bbo'\)**

```text
sed "/bbo/d" filename
# case insensitive:
sed "/bbo/Id" filename
```

### **Remove lines whose nth character not equal to a value \(e.g. 5th character not equal to 2\)**

```text
sed -E '/^.{5}[^2]/d'
#aaaa2aaa (you can stay)
#aaaa1aaa (delete!)
```

### **Edit infile \(edit and save to file\), \(e.g. deleting the lines with 'bbo' and save to file\)**

```text
sed -i "/bbo/d" filename
```

### **When using variable \(e.g. $i\), use double quotes " "**

```text
# e.g. add >$i to the first line (to make a bioinformatics FASTA file)
sed "1i >$i"
# notice the double quotes! in other examples, you can use a single quote, but here, no way!
# '1i' means insert to first line
```

### **Using environment variable and end-of-line pattern at the same time.**

```text
# Use backslash for end-of-line $ pattern, and double quotes for expressing the variable
sed -e "\$s/\$/\n+--$3-----+/"
```

### **Delete/remove empty lines**

```text
sed '/^\s*$/d'

# or

sed '/^$/d'
```

### **Delete/remove last line**

```text
sed '$d'
```

### **Delete/remove last character from end of file**

```text
sed -i '$ s/.$//' filename
```

### **Add string to beginning of file \(e.g. "\["\)**

```text
sed -i '1s/^/[/' file
```

### **Add string at certain line number \(e.g. add 'something' to line 1 and line 3\)**

```text
sed -e '1isomething -e '3isomething'
```

### **Add string to end of file \(e.g. "\]"\)**

```text
sed '$s/$/]/' filename
```

### **Add newline to the end**

```text
sed '$a\'
```

### **Add string to beginning of every line \(e.g. 'bbo'\)**

```text
sed -e 's/^/bbo/' file
```

### **Add string to end of each line \(e.g. "}"\)**

```text
sed -e 's/$/\}\]/' filename
```

### **Add \n every nth character \(e.g. every 4th character\)**

```text
sed 's/.\{4\}/&\n/g'
```

### **Concatenate/combine/join files with a seperator and next line \(e.g separate by ","\)**

```text
sed -s '$a,' *.json > all.json
```

### **Substitution \(e.g. replace A by B\)**

```text
sed 's/A/B/g' filename
```

### **Substitution with wildcard \(e.g. replace a line start with aaa= by aaa=/my/new/path\)**

```text
sed "s/aaa=.*/aaa=\/my\/new\/path/g"
```

### **Select lines start with string \(e.g. 'bbo'\)**

```text
sed -n '/^@S/p'
```

### **Delete lines with string \(e.g. 'bbo'\)**

```text
sed '/bbo/d' filename
```

### **Print/get/trim a range of line \(e.g. line 500-5000\)**

```text
sed -n 500,5000p filename
```

### **Print every nth lines**

```text
sed -n '0~3p' filename

# catch 0: start; 3: step
```

### **Print every odd \# lines**

```text
sed -n '1~2p'
```

### **Print every third line including the first line**

```text
sed -n '1p;0~3p'
```

### **Remove leading whitespace and tabs**

```text
sed -e 's/^[ \t]*//'
# Notice a whitespace before '\t'!!
```

### **Remove only leading whitespace**

```text
sed 's/ *//'

# notice a whitespace before '*'!!
```

### **Remove ending commas**

```text
sed 's/,$//g'
```

### **Add a column to the end**

```text
sed "s/$/\t$i/"
# $i is the valuable you want to add

# To add the filename to every last column of the file
for i in $(ls);do sed -i "s/$/\t$i/" $i;done
```

### **Add extension of filename to last column**

```text
for i in T000086_1.02.n T000086_1.02.p;do sed "s/$/\t${i/*./}/" $i;done >T000086_1.02.np
```

### **Remove newline\ nextline**

```text
sed ':a;N;$!ba;s/\n//g'
```

### **Print a particular line \(e.g. 123th line\)**

```text
sed -n -e '123p'
```

### **Print a number of lines \(e.g. line 10th to line 33 rd\)**

```text
sed -n '10,33p' <filename
```

### **Change delimiter**

```text
sed 's=/=\\/=g'
```

### **Replace with wildcard \(e.g A-1-e or A-2-e or A-3-e....\)**

```text
sed 's/A-.*-e//g' filename
```

### **Remove last character of file**

```text
sed '$ s/.$//'
```

### **Insert character at specified position of file \(e.g. AAAAAA --&gt; AAA\#AAA\)**

```text
sed -r -e 's/^.{3}/&#/' file
```

