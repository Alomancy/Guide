# Networking

## Networking

### **Resolve a domain to IP address\(es\)**

```text
dig +short www.example.com

# or
host www.example.com
```

### **Get DNS TXT record a of domain**

```text
dig -t txt www.example.com

# or
host -t txt www.example.com
```

### **Send a ping with a limited TTL to 10 \(TTL: Time-To-Live, which is the maximum number of hops that a packet can travel across the Internet before it gets discarded.\)**

```text
ping 8.8.8.8 -t 10
```

### **Print the route packets trace to network host**

```text
traceroute google.com
```

### **Check connection to host \(e.g. check connection to port 80 and 22 of google.com\)**

```text
nc -vw5 google.com 80
# Connection to google.com 80 port [tcp/http] succeeded!

nc -vw5 google.com 22
# nc: connect to google.com port 22 (tcp) timed out: Operation now in progress
# nc: connect to google.com port 22 (tcp) failed: Network is unreachable
```

### **Nc as a chat tool!**

```text
# From server A:
$ sudo nc -l 80
# then you can connect to the 80 port from another server (e.g. server B):
# e.g. telent <server A IP address> 80
# then type something in server B
# and you will see the result in server A!
```

### **Check which ports are listening for TCP connections from the network**

```text
#notice that some companies might not like you using nmap
nmap -sT -O localhost

# check port 0-65535
nmap  -p0-65535 localhost
```

### **Check if a host is up and scan for open ports, also skip host discovery.**

```text
#skips checking if the host is alive which may sometimes cause a false positive and stop the scan.
$ nmap google.com -Pn

# Example output:
# Starting Nmap 7.01 ( https://nmap.org ) at 2020-07-18 22:59 CST
# Nmap scan report for google.com (172.217.24.14)
# Host is up (0.013s latency).
# Other addresses for google.com (not scanned): 2404:6800:4008:802::200e
# rDNS record for 172.217.24.14: tsa01s07-in-f14.1e100.net
# Not shown: 998 filtered ports
# PORT    STATE SERVICE
# 80/tcp  open  http
# 443/tcp open  https
#
# Nmap done: 1 IP address (1 host up) scanned in 3.99 seconds
```

### **Scan for open ports and OS and version detection \(e.g. scan the domain "scanme.nmap.org"\)**

```text
$ nmap -A -T4 scanme.nmap.org
# -A to enable OS and version detection, script scanning, and traceroute; -T4 for faster execution
```

### **Look up website information \(e.g. name server\), searches for an object in a RFC 3912 database.**

```text
whois google.com
```

### **Show the SSL certificate of a domain**

```text
openssl s_client -showcerts -connect www.example.com:443
```

### **Display IP address**

```text
ip a
```

### **Display route table**

```text
ip r
```

### **Display ARP cache \(ARP cache displays the MAC addresses of device in the same network that you have connected to\)**

```text
ip n
```

### **Add transient IP addres \(reset after reboot\) \(e.g. add 192.168.140.3/24 to device eno16777736\)**

```text
ip address add 192.168.140.3/24 dev eno16777736
```

### **Persisting network configuration changes**

```text
sudo vi /etc/sysconfig/network-scripts/ifcfg-enoxxx
# then edit the fields: BOOTPROT, DEVICE, IPADDR, NETMASK, GATEWAY, DNS1 etc
```

### **Refresh NetworkManager**

```text
sudo nmcli c reload
```

### **Restart all interfaces**

```text
sudo systemctl restart network.service
```

### **To view hostname, OS, kernal, architecture at the same time!**

```text
hostnamectl
```

### **Set hostname \(set all transient, static, pretty hostname at once\)**

```text
hostnamectl set-hostname "mynode"
```

### **Find out the web server \(e.g Nginx or Apache\) of a website**

```text
curl -I http://example.com/
# HTTP/1.1 200 OK
# Server: nginx
# Date: Thu, 02 Jan 2020 07:01:07 GMT
# Content-Type: text/html
# Content-Length: 1119
# Connection: keep-alive
# Vary: Accept-Encoding
# Last-Modified: Mon, 09 Sep 2019 10:37:49 GMT
# ETag: "xxxxxx"
# Accept-Ranges: bytes
# Vary: Accept-Encoding
```

### **Find out the http status code of a URL**

```text
curl -s -o /dev/null -w "%{http_code}" https://www.google.com
```

### **Unshorten a shortended URL**

```text
curl -s -o /dev/null -w "%{redirect_url}" https://bit.ly/34EFwWC
```

### **Perform network throughput tests**

```text
# server side:
$ sudo iperf -s -p 80

# client side:
iperf -c <server IP address> --parallel 2 -i 1 -t 2 -p 80
```

### **To block port 80 \(HTTP server\) using iptables.**

```text
sudo iptables -A INPUT -p tcp --dport 80 -j DROP

# only block connection from an IP address
sudo iptables –A INPUT –s <IP> -p tcp –dport 80 –j DROP
```

