# Terminal

## Terminal Tricks

### **Using Ctrl keys**

```text
Ctrl + n : same as Down arrow.
Ctrl + p : same as Up arrow.
Ctrl + r : begins a backward search through command history.(keep pressing Ctrl + r to move backward)
Ctrl + s : to stop output to terminal.
Ctrl + q : to resume output to terminal after Ctrl + s.
Ctrl + a : move to the beginning of line.
Ctrl + e : move to the end of line.
Ctrl + d : if you've type something, Ctrl + d deletes the character under the cursor, else, it escapes the current shell.
Ctrl + k : delete all text from the cursor to the end of line.
Ctrl + x + backspace : delete all text from the beginning of line to the cursor.
Ctrl + t : transpose the character before the cursor with the one under the cursor, press Esc + t to transposes the two words before the cursor.
Ctrl + w : cut the word before the cursor; then Ctrl + y paste it
Ctrl + u : cut the line before the cursor; then Ctrl + y paste it
Ctrl + _ : undo typing.
Ctrl + l : equivalent to clear.
Ctrl + x + Ctrl + e : launch editor defined by $EDITOR to input your command. Useful for multi-line commands.
```

### **Change case**

```text
Esc + u
# converts text from cursor to the end of the word to uppercase.
Esc + l
# converts text from cursor to the end of the word to lowercase.
Esc + c
# converts letter under the cursor to uppercase.
```

### **Run history number \(e.g. 53\)**

```text
!53
```

### **Run last command**

```text
!!
# run the previous command using sudo
sudo !!
# of course you need to enter your password
```

**Run last command and change some parameter using caret substitution \(e.g. last command: echo 'aaa' -&gt; rerun as: echo 'bbb'\)**

```text
#last command: echo 'aaa'
^aaa^bbb

#echo 'bbb'
#bbb

#Notice that only the first aaa will be replaced, if you want to replace all 'aaa', use ':&' to repeat it:
^aaa^bbb^:&
#or
!!:gs/aaa/bbb/
```

### **Run past command that began with \(e.g. cat filename\)**

```text
!cat
# or
!c
# run cat filename again
```

### **Bash globbing**

```text
# '*' serves as a "wild card" for filename expansion.
/b?n/?at      #/bin/cat

# '?' serves as a single-character "wild card" for filename expansion.
/etc/pa*wd    #/etc/passwd

# ‘[]’ serves to match the character from a range.
ls -l [a-z]*   #list all files with alphabet in its filename.

# ‘{}’ can be used to match filenames with more than one patterns
ls {*.sh,*.py}   #list all .sh and .py files
```

### **Some handy environment variables**

```text
$0   :name of shell or shell script.
$1, $2, $3, ... :positional parameters.
$#   :number of positional parameters.
$?   :most recent foreground pipeline exit status.
$-   :current options set for the shell.
$$   :pid of the current shell (not subshell).
$!   :is the PID of the most recent background command.

$DESKTOP_SESSION     current display manager
$EDITOR   preferred text editor.
$LANG   current language.
$PATH   list of directories to search for executable files (i.e. ready-to-run programs)
$PWD    current directory
$SHELL  current shell
$USER   current username
$HOSTNAME   current hostname
```

