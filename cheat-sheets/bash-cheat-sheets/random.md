# Random

## Random

### **Random generate password \(e.g. generate 5 password each of length 13\)**

```text
sudo apt install pwgen
pwgen 13 5
#sahcahS9dah4a xieXaiJaey7xa UuMeo0ma7eic9 Ahpah9see3zai acerae7Huigh7
```

### **Random pick 100 lines from a file**

```text
shuf -n 100 filename
```

### **Random order \(lucky draw\)**

```text
for i in a b c d e; do echo $i; done | shuf
```

### **Echo series of random numbers between a range \(e.g. shuffle numbers from 0-100, then pick 15 of them randomly\)**

```text
shuf -i 0-100 -n 15
```

### **Echo a random number**

```text
echo $RANDOM
```

### **Random from 0-9**

```text
echo $((RANDOM % 10))
```

### **Random from 1-10**

```text
echo $(((RANDOM %10)+1))
```

