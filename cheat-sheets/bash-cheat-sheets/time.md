# Time

## Time

### **Find out the time require for executing a command**

```text
time echo hi
```

### **Wait for some time \(e.g 10s\)**

```text
sleep 10
```

### **Print date with formatting**

```text
date +%F
# 2020-07-19

# or
date +'%d-%b-%Y-%H:%M:%S'
# 10-Apr-2020-21:54:40

# Returns the current time with nanoseconds.
date +"%T.%N"
# 11:42:18.664217000  

# Get the seconds since epoch (Jan 1 1970) for a given date (e.g Mar 16 2021)
date -d "Mar 16 2021" +%s
# 1615852800
# or
date -d "Tue Mar 16 00:00:00 UTC 2021"  +%s
# 1615852800  

# Convert the number of seconds since epoch back to date
date --date @1615852800
# Tue Mar 16 00:00:00 UTC 2021
```

### **wait for random duration \(e.g. sleep 1-5 second, like adding a jitter\)**

```text
sleep $[ ( $RANDOM % 5 ) + 1 ]
```

### **Log out your account after a certain period of time \(e.g 10 seconds\)**

```text
TMOUT=10
#once you set this variable, logout timer start running!
```

### **Set how long you want to run a command**

```text
#This will run the command 'sleep 10' for only 1 second.
timeout 1 sleep 10
```

### **Set when you want to run a command \(e.g 1 min from now\)**

```text
at now + 1min  #time-units can be minutes, hours, days, or weeks
warning: commands will be executed using /bin/sh
at> echo hihigithub >~/itworks
at> <EOT>   # press Ctrl + D to exit
job 1 at Wed Apr 18 11:16:00 2018
```

