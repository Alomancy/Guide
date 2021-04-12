# Math

## Math

### **Arithmetic Expansion in Bash \(Operators: +, -, \*, /, %, etc\)**

```text
echo $(( 10 + 5 ))  #15
x=1
echo $(( x++ )) #1 , notice that it is still 1, since it's post-incremen
echo $(( x++ )) #2
echo $(( ++x )) #4 , notice that it is not 3 since it's pre-incremen
echo $(( x-- )) #4
echo $(( x-- )) #3
echo $(( --x )) #1
x=2
y=3
echo $(( x ** y )) #8
```

### **Print out the prime factors of a number \(e.g. 50\)**

```text
factor 50
# 50: 2 5 5
```

### **Sum up input list \(e.g. seq 10\)**

```text
seq 10|paste -sd+|bc
```

### **Sum up a file \(each line in file contains only one number\)**

```text
awk '{s+=$1} END {print s}' filename
```

### **Column subtraction**

```text
cat file| awk -F '\t' 'BEGIN {SUM=0}{SUM+=$3-$2}END{print SUM}'
```

### **Simple math with expr**

```text
expr 10+20 #30
expr 10\*20 #600
expr 30 \> 20 #1 (true)
```

### **More math with bc**

```text
# Number of decimal digit/ significant figure
echo "scale=2;2/3" | bc
#.66

# Exponent operator
echo "10^2" | bc
#100

# Using variables
echo "var=5;--var"| bc
#4
```

