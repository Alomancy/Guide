# Condition and Loop

## Condition and loop

### **If statement**

```text
# if and else loop for string matching
if [[ "$c" == "read" ]]; then outputdir="seq"; else outputdir="write" ; fi

# Test if myfile contains the string 'test':
if grep -q hello myfile; then echo -e "file contains the string!" ; fi

# Test if mydir is a directory, change to it and do other stuff:
if cd mydir; then
  echo 'some content' >myfile
else
  echo >&2 "Fatal error. This script requires mydir."
fi

# if variable is null
if [ ! -s "myvariable" ]; then echo -e "variable is null!" ; fi
#True of the length if "STRING" is zero.

# Using test command (same as []), to test if the length of variable is nonzero
test -n "$myvariable" && echo myvariable is "$myvariable" || echo myvariable is not set

# Test if file exist
if [ -e 'filename' ]
then
  echo -e "file exists!"
fi

# Test if file exist but also including symbolic links:
if [ -e myfile ] || [ -L myfile ]
then
  echo -e "file exists!"
fi

# Test if the value of x is greater or equal than 5
if [ "$x" -ge 5 ]; then echo -e "greater or equal than 5!" ; fi

# Test if the value of x is greater or equal than 5, in bash/ksh/zsh:
if ((x >= 5)); then echo -e "greater or equal than 5!" ; fi

# Use (( )) for arithmetic operation
if ((j==u+2)); then echo -e "j==u+2!!" ; fi

# Use [[ ]] for comparison
if [[ $age -gt 21 ]]; then echo -e "forever 21!!" ; fi
```

### [More if commands](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_07_01.html)

### **For loop**

```text
# Echo the file name under the current directory
for i in $(ls); do echo file $i;done
#or
for i in *; do echo file $i; done

# Make directories listed in a file (e.g. myfile)
for dir in $(<myfile); do mkdir $dir; done

# Press any key to continue each loop
for i in $(cat tpc_stats_0925.log |grep failed|grep -o '\query\w\{1,2\}');do cat ${i}.log; read -rsp $'Press any key to continue...\n' -n1 key;done

# Print a file line by line when a key is pressed,
oifs="$IFS"; IFS=$'\n'; for line in $(cat myfile); do ...; done
while read -r line; do ...; done <myfile

#If only one word a line, simply
for line in $(cat myfile); do echo $line; read -n1; done

#Loop through an array
for i in "${arrayName[@]}"; do echo $i;done
```

### **While loop,**

```text
# Column subtraction of a file (e.g. a 3 columns file)
while read a b c; do echo $(($c-$b));done < <(head filename)
#there is a space between the two '<'s

# Sum up column subtraction
i=0; while read a b c; do ((i+=$c-$b)); echo $i; done < <(head filename)

# Keep checking a running process (e.g. perl) and start another new process (e.g. python) immediately after it. (BETTER use the wait command! Ctrl+F 'wait')
while [[ $(pidof perl) ]];do echo f;sleep 10;done && python timetorunpython.py
```

### **switch \(case in bash\)**

```text
read type;
case $type in
  '0')
    echo 'how'
    ;;
  '1')
    echo 'are'
    ;;
  '2')
    echo 'you'
    ;;
esac
```

## 

