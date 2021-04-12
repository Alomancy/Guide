# Xargs

## Xargs

### **Set tab as delimiter \(default:space\)**

```text
xargs -d\t
```

### **Prompt commands before running commands**

```text
ls|xargs -L1 -p head
```

### **Display 3 items per line**

```text
echo 1 2 3 4 5 6| xargs -n 3
# 1 2 3
# 4 5 6
```

### **Prompt before execution**

```text
echo a b c |xargs -p -n 3
```

### **Print command along with output**

```text
xargs -t abcd
# bin/echo abcd
# abcd
```

### **With find and rm**

```text
find . -name "*.html"|xargs rm

# when using a backtick
rm `find . -name "*.html"`
```

### **Delete files with whitespace in filename \(e.g. "hello 2001"\)**

```text
find . -name "*.c" -print0|xargs -0 rm -rf
```

### **Show limits on command-line length**

```text
xargs --show-limits
# Output from my Ubuntu:
# Your environment variables take up 3653 bytes
# POSIX upper limit on argument length (this system): 2091451
# POSIX smallest allowable upper limit on argument length (all systems): 4096
# Maximum length of command we could actually use: 2087798
# Size of command buffer we are actually using: 131072
# Maximum parallelism (--max-procs must be no greater): 2147483647
```

### **Move files to folder**

```text
find . -name "*.bak" -print 0|xargs -0 -I {} mv {} ~/old

# or
find . -name "*.bak" -print 0|xargs -0 -I file mv file ~/old
```

### **Move first 100th files to a directory \(e.g. d1\)**

```text
ls |head -100|xargs -I {} mv {} d1
```

### **Parallel**

```text
time echo {1..5} |xargs -n 1 -P 5 sleep

# a lot faster than:
time echo {1..5} |xargs -n1 sleep
```

### **Copy all files from A to B**

```text
find /dir/to/A -type f -name "*.py" -print 0| xargs -0 -r -I file cp -v -p file --target-directory=/path/to/B

# v: verbose|
# p: keep detail (e.g. owner)
```

### **With sed**

```text
ls |xargs -n1 -I file sed -i '/^Pos/d' filename
```

### **Add the file name to the first line of file**

```text
ls |sed 's/.txt//g'|xargs -n1 -I file sed -i -e '1 i\>file\' file.txt
```

### **Count all files**

```text
ls |xargs -n1 wc -l
```

### **Turn output into a single line**

```text
ls -l| xargs
```

### **Count files within directories**

```text
echo mso{1..8}|xargs -n1 bash -c 'echo -n "$1:"; ls -la "$1"| grep -w 74 |wc -l' --
# "--" signals the end of options and display further option processing
```

### **Count lines in all file, also count total lines**

```text
ls|xargs wc -l
```

### **Xargs and grep**

```text
cat grep_list |xargs -I{} grep {} filename
```

### **Xargs and sed \(replace all old ip address with new ip address under /etc directory\)**

```text
grep -rl '192.168.1.111' /etc | xargs sed -i 's/192.168.1.111/192.168.2.111/g'
```

