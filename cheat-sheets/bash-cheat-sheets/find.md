# Find

## Find

### **List all sub directory/file in the current directory**

```text
find .
```

### **List all files under the current directory**

```text
find . -type f
```

### **List all directories under the current directory**

```text
find . -type d
```

### **Edit all files under current directory \(e.g. replace 'www' with 'ww'\)**

```text
find . -name '*.php' -exec sed -i 's/www/w/g' {} \;

# if there are no subdirectory
replace "www" "w" -- *
# a space before *
```

### **Find and output only filename \(e.g. "mso"\)**

```text
find mso*/ -name M* -printf "%f\n"
```

### **Find large files in the system \(e.g. &gt;4G\)**

```text
find / -type f -size +4G
```

### **Find and delete file with size less than \(e.g. 74 byte\)**

```text
find . -name "*.mso" -size -74c -delete

# M for MB, etc
```

### **Find empty \(0 byte\) files**

```text
find . -type f -empty
# to further delete all the empty files
find . -type f -empty -delete
```

### **Recursively count all the files in a directory**

```text
find . -type f | wc -l
```

