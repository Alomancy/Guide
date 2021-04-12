# Download

## Download

### **Download the content of this README.md \(the one your are viewing now\)**

```text
curl https://raw.githubusercontent.com/onceupon/Bash-Oneliner/master/README.md | pandoc -f markdown -t man | man -l -

# or w3m (a text based web browser and pager)
curl https://raw.githubusercontent.com/onceupon/Bash-Oneliner/master/README.md | pandoc | w3m -T text/html

# or using emacs (in emac text editor)
emacs --eval '(org-mode)' --insert <(curl https://raw.githubusercontent.com/onceupon/Bash-Oneliner/master/README.md | pandoc -t org)

# or using emacs (on terminal, exit using Ctrl + x then Ctrl + c)
emacs -nw --eval '(org-mode)' --insert <(curl https://raw.githubusercontent.com/onceupon/Bash-Oneliner/master/README.md | pandoc -t org)
```

### **Download all from a page**

```text
wget -r -l1 -H -t1 -nd -N -np -A mp3 -e robots=off http://example.com

# -r: recursive and download all links on page
# -l1: only one level link
# -H: span host, visit other hosts
# -t1: numbers of retries
# -nd: don't make new directories, download to here
# -N: turn on timestamp
# -nd: no parent
# -A: type (separate by ,)
# -e robots=off: ignore the robots.txt file which stop wget from crashing the site, sorry example.com
```

### **Upload a file to web and download \(https://transfer.sh/\)**

```text
#  Upload a file (e.g. filename.txt):
curl --upload-file ./filename.txt https://transfer.sh/filename.txt
# the above command will return a URL, e.g: https://transfer.sh/tG8rM/filename.txt

# Next you can download it by:
curl https://transfer.sh/tG8rM/filename.txt -o filename.txt
```

### **Download file if necessary**

```text
data=file.txt
url=http://www.example.com/$data
if [ ! -s $data ];then
    echo "downloading test data..."
    wget $url
fi
```

### **Wget to a filename \(when a long name\)**

```text
wget -O filename "http://example.com"
```

### **Wget files to a folder**

```text
wget -P /path/to/directory "http://example.com"
```

### **Instruct curl to follow any redirect until it reaches the final destination:**

```text
curl -L google.com
```

