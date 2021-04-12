# Other

## Others

### **Describe the format and characteristics of image files.**

```text
identify myimage.png
#myimage.png PNG 1049x747 1049x747+0+0 8-bit sRGB 1.006MB 0.000u 0:00.000
```

### **Bash auto-complete \(e.g. show options "now tomorrow never" when you press'tab' after typing "dothis"\)**

[More examples](https://iridakos.com/tutorials/2018/03/01/bash-programmable-completion-tutorial.html)

```text
complete -W "now tomorrow never" dothis
# ~$ dothis  
# never     now       tomorrow
# press 'tab' again to auto-complete after typing 'n' or 't'
```

### **Displays a calendar**

```text
# print the current month, today will be highlighted.
cal
# October 2019      
# Su Mo Tu We Th Fr Sa  
#    1  2  3  4  5  
# 6  7  8  9 10 11 12  
# 13 14 15 16 17 18 19  
# 20 21 22 23 24 25 26  
# 27 28 29 30 31  

# only display November
cal -m 11
```

### **Convert the hexadecimal MD5 checksum value into its base64-encoded format.**

```text
openssl md5 -binary /path/to/file| base64
# NWbeOpeQbtuY0ATWuUeumw==
```

### **Forces applications to use the default language for output**

```text
export LC_ALL=C

# to revert:
unset LC_ALL
```

### **Encode strings as Base64 strings**

```text
echo test|base64
#dGVzdAo=
```

### **Get parent directory of current directory**

```text
dirname `pwd`
```

### **Read .gz file without extracting**

```text
zmore filename

# or
zless filename
```

### **Run command in background, output error file**

```text
some_commands  &>log &

# or
some_commands 2>log &

# or
some_commands 2>&1| tee logfile

# or
some_commands |& tee logfile

# or
some_commands 2>&1 >>outfile
#0: standard input; 1: standard output; 2: standard error
```

### **Run multiple commands in background**

```text
# run sequentially
(sleep 2; sleep 3) &

# run parallelly
sleep 2 & sleep 3 &
```

### **Run process even when logout \(immune to hangups, with output to a non-tty\)**

```text
# e.g. Run myscript.sh even when log out.
nohup bash myscript.sh
```

### **Send mail**

```text
echo 'heres the content'| mail -a /path/to/attach_file.txt -s 'mail.subject' me@gmail.com
# use -a flag to set send from (-a "From: some@mail.tld")
```

### **Convert .xls to csv**

```text
xls2csv filename
```

### **Make BEEP sound**

```text
speaker-test -t sine -f 1000 -l1
```

### **Set beep duration**

```text
(speaker-test -t sine -f 1000) & pid=$!;sleep 0.1s;kill -9 $pid
```

### **Editing your history**

```text
history -w
vi ~/.bash_history
history -r

#or
history -d [line_number]
```

### **Interacting with history**

```text
# list 5 previous command (similar to `history |tail -n 5` but wont print the history command itself)
fc -l -5
```

### **Delete current bash command**

```text
Ctrl+U

# or
Ctrl+C

# or
Alt+Shift+#
# to make it to history
```

### **Add something to history \(e.g. "addmetohistory"\)**

```text
# addmetodistory
# just add a "#" before~~
```

### **Get last history/record filename**

```text
head !$
```

### **Clean screen**

```text
clear
# or simply Ctrl+l
```

### **Backup with rsync**

```text
rsync -av filename filename.bak
rsync -av directory directory.bak
rsync -av --ignore_existing directory/ directory.bak
rsync -av --update directory directory.bak

rsync -av directory user@ip_address:/path/to/directory.bak
# skip files that are newer on receiver (i prefer this one!)
```

### **Make all directories at one time!**

```text
mkdir -p project/{lib/ext,bin,src,doc/{html,info,pdf},demo/stat}
# -p: make parent directory
# this will create project/doc/html/; project/doc/info; project/lib/ext ,etc
```

### **Run command only if another command returns zero exit status \(well done\)**

```text
cd tmp/ && tar xvf ~/a.tar
```

### **Run command only if another command returns non-zero exit status \(not finish\)**

```text
cd tmp/a/b/c ||mkdir -p tmp/a/b/c
```

### **Use backslash "" to break long command**

```text
cd tmp/a/b/c \
> || \
>mkdir -p tmp/a/b/c
```

### **List file type of file \(e.g. /tmp/\)**

```text
file /tmp/
# tmp/: directory
```

### **Writing Bash script \('\#!'' is called shebang \)**

```text
#!/bin/bash
file=${1#*.}
# remove string before a "."
```

### **Python simple HTTP Server**

```text
python -m SimpleHTTPServer
# or when using python3:
python3 -m http.server
```

### **Read user input**

```text
read input
echo $input
```

### **Array**

```text
declare -a array=()

# or
declare array=()

# or associative array
declare -A array=()
```

### **Send a directory**

```text
scp -r directoryname user@ip:/path/to/send
```

### **Fork bomb**

```text
# Don't try this at home!
# It is a function that calls itself twice every call until you run out of system resources.
# A '# ' is added in front for safety reason, remove it when seriously you are testing it.
# :(){:|:&};:
```

### **Use the last argument**

```text
!$
```

### **Check last exit code**

```text
echo $?
```

### **Extract .xz**

```text
unxz filename.tar.xz
# then
tar -xf filename.tar
```

### **Unzip tar.bz2 file \(e.g. file.tar.bz2\)**

```text
tar xvfj file.tar.bz2
```

### **Unzip tar.xz file \(e.g. file.tar.xz\)**

```text
unxz file.tar.xz
tar xopf file.tar
```

### **Extract to a path**

```text
tar xvf -C /path/to/directory filename.gz
```

### **Zip the content of a directory without including the directory itself**

```text
# First cd to the directory, they run:
zip -r -D ../myzipfile .
# you will see the myzipfile.zip in the parent directory (cd ..)
```

### **Output a y/n repeatedly until killed**

```text
# 'y':
yes

# or 'n':
yes n

# or 'anything':
yes anything

# pipe yes to other command
yes | rm -r large_directory
```

### **Create large dummy file of certain size instantly \(e.g. 10GiB\)**

```text
fallocate -l 10G 10Gigfile
```

### **Create dummy file of certain size \(e.g. 200mb\)**

```text
dd if=/dev/zero of=//dev/shm/200m bs=1024k count=200
# or
dd if=/dev/zero of=//dev/shm/200m bs=1M count=200

# Standard output:
# 200+0 records in
# 200+0 records out
# 209715200 bytes (210 MB) copied, 0.0955679 s, 2.2 GB/s
```

### **Keep /repeatedly executing the same command \(e.g Repeat 'wc -l filename' every 1 second\)**

```text
watch -n 1 wc -l filename
```

### **Print commands and their arguments when execute \(e.g. echo expr 10 + 20 \)**

```text
set -x; echo `expr 10 + 20 `
```

### **Print some meaningful sentences to you \(install fortune first\)**

```text
fortune
```

### **Colorful \(and useful\) version of top \(install htop first\)**

```text
htop
```

### **Press any key to continue**

```text
read -rsp $'Press any key to continue...\n' -n1 key
```

### **Run sql-like command on files from terminal**

```text
# download:
# https://github.com/harelba/q
# example:
q -d "," "select c3,c4,c5 from /path/to/file.txt where c3='foo' and c5='boo'"
```

### **Using Screen for multiple terminal sessions**

```text
# Create session and attach:
screen

# Create a screen and name it 'test'
screen -S test

# Create detached session foo:
screen -S foo -d -m

# Detached session foo:
screen: ^a^d

# List sessions:
screen -ls

# Attach last session:
screen -r

# Attach to session foo:
screen -r foo

# Kill session foo:
screen -r foo -X quit


# Scroll:
# Hit your screen prefix combination (C-a / control+A), then hit Escape.
# Move up/down with the arrow keys (↑ and ↓).  

# Redirect output of an already running process in Screen:
# (C-a / control+A), then hit 'H'  

# Store screen output for Screen:
# Ctrl+A, Shift+H  
# You will then find a screen.log file under current directory.  
```

### **Using Tmux for multiple terminal sessions**

```text
# Create session and attach:
tmux

# Attach to session foo:
tmux attach -t foo

# Detached session foo:
^bd

# List sessions:
tmux ls

# Attach last session:
tmux attach

# Kill session foo:
tmux kill-session -t foo

# Create detached session foo:
tmux new -s foo -d

# Send command to all panes in tmux:
Ctrl-B
:setw synchronize-panes

# Some tmux pane control commands:
Ctrl-B
#   Panes (splits), Press Ctrl+B, then input the following symbol:
#   %  horizontal split
#   "  vertical split
#   o  swap panes
#   q  show pane numbers
#   x  kill pane
#   space - toggle between layouts

#   Distribute Vertically (rows):
select-layout even-vertical
#   or
Ctrl+b, Alt+2

# Distribute horizontally (columns):
select-layout even-horizontal
#   or
Ctrl+b, Alt+1

# Scroll
Ctrl-b then \[ then you can use your normal navigation keys to scroll around.
Press q to quit scroll mode.
```

### **Pass password to ssh**

```text
sshpass -p mypassword ssh root@10.102.14.88 "df -h"
```

### **Wait for a pid \(job\) to complete**

```text
wait %1
# or
wait $PID
wait ${!}
#wait ${!} to wait till the last background process ($! is the PID of the last background process)
```

### **Convert pdf to txt**

```text
sudo apt-get install poppler-utils
pdftotext example.pdf example.txt
```

### **List only directory**

```text
ls -d */
```

### **List one file per line.**

```text
ls -1
# or list all, do not ignore entries starting with .
ls -1a
```

### **Capture/record/save terminal output \(capture everything you type and output\)**

```text
script output.txt
# start using terminal
# to logout the screen session (stop saving the contents), type exit.
```

### **List contents of directories in a tree-like format.**

```text
tree
# go to the directory you want to list, and type tree (sudo apt-get install tree)
# output:
# home/
# └── project
#     ├── 1
#     ├── 2
#     ├── 3
#     ├── 4
#     └── 5
#

# set level directories deep (e.g. level 1)
tree -L 1
# home/
# └── project
```

### **Set up virtualenv\(sandbox\) for python**

```text
# 1. install virtualenv.
sudo apt-get install virtualenv
# 2. Create a directory (name it .venv or whatever name your want) for your new shiny isolated environment.
virtualenv .venv
# 3. source virtual bin
source .venv/bin/activate
# 4. you can check check if you are now inside a sandbox.
type pip
# 5. Now you can install your pip package, here requirements.txt is simply a txt file containing all the packages you want. (e.g tornado==4.5.3).
pip install -r requirements.txt
```

