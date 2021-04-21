# Data Manipulation

## Data wrangling

### **Print some words that start with a particular string \(e.g. words start with 'phy'\)**

```text
# If file is not specified, the file /usr/share/dict/words is used.
look phy|head -n 10
# Phil
# Philadelphia
# Philadelphia's
# Philby
# Philby's
# Philip
# Philippe
# Philippe's
# Philippians
# Philippine
```

### **Repeat printing string n times \(e.g. print 'hello world' five times\)**

```text
printf 'hello world\n%.0s' {1..5}
```

### **Do not echo the trailing newline**

```text
username=`echo -n "bashoneliner"`
```

### **Copy a file to multiple files \(e.g copy fileA to file\(B-D\)\)**

```text
tee <fileA fileB fileC fileD >/dev/null
```

### **Delete all non-printing characters**

```text
tr -dc '[:print:]' < filename
```

### **Remove newline / nextline**

```text
tr --delete '\n' <input.txt >output.txt
```

### **Replace newline**

```text
tr '\n' ' ' <filename
```

### **To uppercase/lowercase**

```text
tr /a-z/ /A-Z/
```

### **Translate a range of characters \(e.g. substitute a-z into a\)**

```text
echo 'something' |tr a-z a
# aaaaaaaaa
```

### **Compare two files \(e.g. fileA, fileB\)**

```text
diff fileA fileB
# a: added; d:delete; c:changed

# or
sdiff fileA fileB
# side-to-side merge of file differences
```

### **Compare two files, strip trailing carriage return/ nextline \(e.g. fileA, fileB\)**

```text
 diff fileA fileB --strip-trailing-cr
```

### **Number a file \(e.g. fileA\)**

```text
nl fileA

#or
nl -nrz fileA
# add leading zeros

#or
nl -w1 -s ' '
# making it simple, blank separate
```

### **Join two files field by field with tab \(default join by the first column of both file, and default separator is space\)**

```text
# fileA and fileB should have the same ordering of lines.
join -t '\t' fileA fileB

# Join using specified field (e.g. column 3 of fileA and column 5 of fileB)
join -1 3 -2 5 fileA fileB
```

### **Combine/ paste two or more files into columns \(e.g. fileA, fileB, fileC\)**

```text
paste fileA fileB fileC
# default tab separate
```

### **Group/combine rows into one row**

```text
# e.g.
# AAAA
# BBBB
# CCCC
# DDDD
cat filename|paste - -
# AAAABBBB
# CCCCDDDD
cat filename|paste - - - -
# AAAABBBBCCCCDDDD
```

### **Fastq to fasta \(fastq and fasta are common file formats for bioinformatics sequence data\)**

```text
cat file.fastq | paste - - - - | sed 's/^@/>/g'| cut -f1-2 | tr '\t' '\n' >file.fa
```

### **Reverse string**

```text
echo 12345| rev
```

### **Generate sequence 1-10**

```text
seq 10
```

### **Find average of input list/file of integers**

```text
i=`wc -l filename|cut -d ' ' -f1`; cat filename| echo "scale=2;(`paste -sd+`)/"$i|bc
```

### **Generate all combination \(e.g. 1,2\)**

```text
echo {1,2}{1,2}
# 1 1, 1 2, 2 1, 2 2
```

### **Generate all combination \(e.g. A,T,C,G\)**

```text
set = {A,T,C,G}
group= 5
for ((i=0; i<$group; i++));do
    repetition=$set$repetition;done
    bash -c "echo "$repetition""
```

### **Read file content to variable**

```text
foo=$(<test1)
```

### **Echo size of variable**

```text
echo ${#foo}
```

### **Echo a tab**

```text
echo -e ' \t '
```

### **Split file into smaller file**

```text
# Split by line (e.g. 1000 lines/smallfile)
split -d -l 1000 largefile.txt

# Split by byte without breaking lines across files
split -C 10 largefile.txt
```

### **Create a large amount of dummy files \(e.g 100000 files, 10 bytes each\):**

```text
#1. Create a big file
dd if=/dev/zero of=bigfile bs=1 count=1000000

#2. Split the big file to 100000 10-bytes files
 split -b 10 -a 10 bigfile
```

### **Rename all files \(e.g. remove ABC from all .gz files\)**

```text
rename 's/ABC//' *.gz
```

### **Remove file extension \(e.g remove .gz from filename.gz\)**

```text
basename filename.gz .gz

zcat filename.gz> $(basename filename.gz .gz).unpacked
```

### **Add file extension to all file\(e.g add .txt\)**

```text
rename s/$/.txt/ *
# You can use rename -n s/$/.txt/ * to check the result first, it will only print sth like this:
# rename(a, a.txt)
# rename(b, b.txt)
# rename(c, c.txt)
```

### **Squeeze repeat patterns \(e.g. /t/t --&gt; /t\)**

```text
tr -s "/t" < filename
```

### **Do not print nextline with echo**

```text
echo -e 'text here \c'
```

### **View first 50 characters of file**

```text
head -c 50 file
```

### **Cut and get last column of a file**

```text
cat file|rev | cut -d/ -f1 | rev
```

### **Add one to variable/increment/ i++ a numeric variable \(e.g. $var\)**

```text
((var++))
# or
var=$((var+1))
```

### **Cut the last column**

```text
cat filename|rev|cut -f1|rev
```

### **Cat to a file**

```text
cat >myfile
let me add sth here
exit by control + c
^C
```

### **Clear the contents of a file \(e.g. filename\)**

```text
>filename
```

### **Append to file \(e.g. hihi\)**

```text
echo 'hihi' >>filename
```

### **Working with json data**

```text
#install the useful jq package
#sudo apt-get install jq
#e.g. to get all the values of the 'url' key, simply pipe the json to the following jq command(you can use .[]. to select inner json, i.e jq '.[].url')
cat file.json | jq '.url'
```

### **Decimal to Binary \(e.g get binary of 5\)**

```text
D2B=({0..1}{0..1}{0..1}{0..1}{0..1}{0..1}{0..1}{0..1})
echo -e ${D2B[5]}
#00000101
echo -e ${D2B[255]}
#11111111
```

### **Wrap each input line to fit in specified width \(e.g 4 integers per line\)**

```text
echo "00110010101110001101" | fold -w4
# 0011
# 0010
# 1011
# 1000
# 1101
```

### **Sort a file by column and keep the original order**

```text
sort -k3,3 -s
```

### **Right align a column \(right align the 2nd column\)**

```text
cat file.txt|rev|column -t|rev
```

### **To both view and store the output**

```text
echo 'hihihihi' | tee outputfile.txt
# use '-a' with tee to append to file.
```

### **Show non-printing \(Ctrl\) characters with cat**

```text
cat -v filename
```

### **Convert tab to space**

```text
expand filename
```

### **Convert space to tab**

```text
unexpand filename
```

### **Display file in octal \( you can also use od to display hexadecimal, decimal, etc\)**

```text
od filename
```

### **Reverse cat a file**

```text
tac filename
```

### **Reverse the result from uniq -c**

```text
while read a b; do yes $b |head -n $a ;done <test.txt
```

