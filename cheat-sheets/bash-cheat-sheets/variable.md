# Variable

## Variable

### **Variable substitution within quotes**

```text
# foo=bar
 echo "'$foo'"
#'bar'
# double/single quotes around single quotes make the inner single quotes expand variables
```

### **Get the length of variable**

```text
var="some string"
echo ${#var}
# 11
```

### **Get the first character of the variable**

```text
var=string
echo "${var:0:1}"
#s

# or
echo ${var%%"${var#?}"}
```

### **Remove the first or last string from variable**

```text
var="some string"
echo ${var:2}
#me string
```

### **Replacement \(e.g. remove the first leading 0 \)**

```text
var="0050"
echo ${var[@]#0}
#050
```

### **Replacement \(e.g. replace 'a' with ','\)**

```text
{var/a/,}
```

### **Replace all \(e.g. replace all 'a' with ','\)**

```text
{var//a/,}
```

```text
#with grep
 test="god the father"
 grep ${test// /\\\|} file.txt
 # turning the space into 'or' (\|) in grep
```

### **To change the case of the string stored in the variable to lowercase \(Parameter Expansion\)**

```text
var=HelloWorld
echo ${var,,}
helloworld
```

### **Expand and then execute variable/argument**

```text
cmd="bar=foo"
eval "$cmd"
echo "$bar" # foo
```

