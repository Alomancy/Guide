# Hardware

## Hardware

### **Collect and summarize all hardware info of your machine**

```text
lshw -json >report.json
# Other options are: [ -html ]  [ -short ]  [ -xml ]  [ -json ]  [ -businfo ]  [ -sanitize ] ,etc
```

### **Finding Out memory device detail**

```text
sudo dmidecode -t memory
```

### **Print detail of CPU hardware**

```text
dmidecode -t 4
#          Type   Information
#          0   BIOS
#          1   System
#          2   Base Board
#          3   Chassis
#          4   Processor
#          5   Memory Controller
#          6   Memory Module
#          7   Cache
#          8   Port Connector
#          9   System Slots
#         11   OEM Strings
#         13   BIOS Language
#         15   System Event Log
#         16   Physical Memory Array
#         17   Memory Device
#         18   32-bit Memory Error
#         19   Memory Array Mapped Address
#         20   Memory Device Mapped Address
#         21   Built-in Pointing Device
#         22   Portable Battery
#         23   System Reset
#         24   Hardware Security
#         25   System Power Controls
#         26   Voltage Probe
#         27   Cooling Device
#         28   Temperature Probe
#         29   Electrical Current Probe
#         30   Out-of-band Remote Access
#         31   Boot Integrity Services
#         32   System Boot
#         34   Management Device
#         35   Management Device Component
#         36   Management Device Threshold Data
#         37   Memory Channel
#         38   IPMI Device
#         39   Power Supply
```

### **Count the number of Segate hard disks**

```text
lsscsi|grep SEAGATE|wc -l
# or
sg_map -i -x|grep SEAGATE|wc -l
```

### **Get UUID of a disk \(e.g. sdb\)**

```text
lsblk -f /dev/sdb

# or
sudo blkid /dev/sdb
```

### **Generate an UUID**

```text
uuidgen
```

### **Print detail of all hard disks**

```text
lsblk -io KNAME,TYPE,MODEL,VENDOR,SIZE,ROTA
#where ROTA means rotational device / spinning hard disks (1 if true, 0 if false)
```

### **List all PCI \(Peripheral Component Interconnect\) devices**

```text
lspci
# List information about NIC
lspci | egrep -i --color 'network|ethernet'
```

### **List all USB devices**

```text
lsusb
```

### **Linux modules**

```text
# Show the status of modules in the Linux Kernel
lsmod

# Add and remove modules from the Linux Kernel
modprobe

# or
# Remove a module
rmmod

# Insert a module
insmod
```

### **Controlling IPMI-enabled devices \(e.g. BMC\)**

```text
# Remotely finding out power status of the server
ipmitool -U <bmc_username> -P <bmc_password> -I lanplus -H <bmc_ip_address> power status

# Remotely switching on server
ipmitool -U <bmc_username> -P <bmc_password> -I lanplus -H <bmc_ip_address> power on

# Turn on panel identify light (default 15s)
ipmitool chassis identify 255

# Found out server sensor temperature
ipmitool sensors |grep -i Temp

# Reset BMC
ipmitool bmc reset cold

# Prnt BMC network
ipmitool lan print 1

# Setting BMC network
ipmitool -I bmc lan set 1 ipaddr 192.168.0.55
ipmitool -I bmc lan set 1 netmask 255.255.255.0
ipmitool -I bmc lan set 1 defgw ipaddr 192.168.0.1
```

