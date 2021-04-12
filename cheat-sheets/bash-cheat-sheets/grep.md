# Grep

## Grep

### **Type of grep**

```text
grep = grep -G # Basic Regular Expression (BRE)
fgrep = grep -F # fixed text, ignoring meta-charachetrs
egrep = grep -E # Extended Regular Expression (ERE)
pgrep = grep -P # Perl Compatible Regular Expressions (PCRE)
rgrep = grep -r # recursive
```

### **Grep and count number of empty lines**

```text
grep -c "^$"
```

### **Grep and return only integer**

```text
grep -o '[0-9]*'
#or
grep -oP '\d'
```

### **Grep integer with certain number of digits \(e.g. 3\)**

```text
grep ‘[0-9]\{3\}’
# or
grep -E ‘[0-9]{3}’
# or
grep -P ‘\d{3}’
```

### **Grep only IP address**

```text
grep -Eo '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}'
# or
grep -Po '\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}'
```

### **Grep whole word \(e.g. 'target'\)**

```text
grep -w 'target'

#or using RE
grep '\btarget\b'
```

### **Grep returning lines before and after match \(e.g. 'bbo'\)**

```text
# return also 3 lines after match
grep -A 3 'bbo'

# return also 3 lines before match
grep -B 3 'bbo'

# return also 3 lines before and after match
grep -C 3 'bbo'
```

### **Grep string starting with \(e.g. 'S'\)**

```text
grep -o 'S.*'
```

### **Extract text between words \(e.g. w1,w2\)**

```text
grep -o -P '(?<=w1).*(?=w2)'
```

### **Grep lines without word \(e.g. 'bbo'\)**

```text
grep -v bbo filename
```

### **Grep lines not begin with string \(e.g. \#\)**

```text
grep -v '^#' file.txt
```

### **Grep variables with space within it \(e.g. myvar="some strings"\)**

```text
grep "$myvar" filename
#remember to quote the variable!
```

### **Grep only one/first match \(e.g. 'bbo'\)**

```text
grep -m 1 bbo filename
```

### **Grep and return number of matching line\(e.g. 'bbo'\)**

```text
grep -c bbo filename
```

### **Count occurrence \(e.g. three times a line count three times\)**

```text
grep -o bbo filename |wc -l
```

### **Case insensitive grep \(e.g. 'bbo'/'BBO'/'Bbo'\)**

```text
grep -i "bbo" filename
```

### **COLOR the match \(e.g. 'bbo'\)!**

```text
grep --color bbo filename
```

### **Grep search all files in a directory\(e.g. 'bbo'\)**

```text
grep -R bbo /path/to/directory
# or
grep -r bbo /path/to/directory
```

### **Search all files in directory, do not ouput the filenames \(e.g. 'bbo'\)**

```text
grep -rh bbo /path/to/directory
```

### **Search all files in directory, output ONLY the filenames with matches\(e.g. 'bbo'\)**

```text
grep -rl bbo /path/to/directory
```

### **Grep OR \(e.g. A or B or C or D\)**

```text
grep 'A\|B\|C\|D'
```

### **Grep AND \(e.g. A and B\)**

```text
grep 'A.*B'
```

### **Regex any single character \(e.g. ACB or AEB\)**

```text
grep 'A.B'
```

### **Regex with or without a certain character \(e.g. color or colour\)**

```text
grep ‘colou?r’
```

### **Grep all content of a fileA from fileB**

```text
grep -f fileA fileB
```

### **Grep a tab**

```text
grep $'\t'
```

### **Grep variable from variable**

```text
$echo "$long_str"|grep -q "$short_str"
if [ $? -eq 0 ]; then echo 'found'; fi
#grep -q will output 0 if match found
#remember to add space between []!
```

### **Grep strings between a bracket\(\)**

```text
grep -oP '\(\K[^\)]+'
```

### **Grep number of characters with known strings in between\(e.g. AAEL000001-RA\)**

```text
grep -o -w "\w\{10\}\-R\w\{1\}"
# \w word character [0-9a-zA-Z_] \W not word character
```

### **Skip directory \(e.g. 'bbo'\)**

```text
grep -d skip 'bbo' /path/to/files/*
```

