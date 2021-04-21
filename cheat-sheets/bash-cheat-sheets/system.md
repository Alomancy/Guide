# System

## System

### **Work with yum history**

```text
# List yum history (e.g install, update)
sudo yum history
# Example output:
# Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
# ID     | Login user               | Date and time    | Action(s)      | Altered
# -------------------------------------------------------------------------------
#     11 |  ... <myuser>       | 2020-04-10 10:57 | Install        |    1 P<
#     10 |  ... <myuser>       | 2020-03-27 05:21 | Install        |    1 >P
#      9 |  ... <myuser>       | 2020-03-05 11:57 | I, U           |   56 *<
# ...

# Show more details of a yum history (e.g. history #11)
sudo yum history info 11

# Undo a yum history (e.g. history #11, this will uninstall some packages)
sudo yum history undo 11
```

### **Audit files to see who made changes to a file \[RedHat based system only\]**

```text
# To audit a directory recursively for changes (e.g. myproject)
auditctl -w /path/to/myproject/ -p wa

# If you delete a file name "VIPfile", the deletion is recorded in /var/log/audit/audit.log
sudo grep VIPfile /var/log/audit/audit.log
#type=PATH msg=audit(1581417313.678:113): item=1 name="VIPfile" inode=300115 dev=ca:01 mode=0100664 ouid=1000 ogid=1000 rdev=00:00 nametype=DELETE cap_fp=0000000000000000 cap_fi=0000000000000000 cap_fe=0 cap_fver=0
```

### **Check out whether SELinux is enabled**

```text
sestatus
# SELinux status:                 enabled
# SELinuxfs mount:                /sys/fs/selinux
# SELinux root directory:         /etc/selinux
# Loaded policy name:             targeted
# Current mode:                   enforcing
# Mode from config file:          enforcing
# Policy MLS status:              enabled
# Policy deny_unknown status:     allowed
# Max kernel policy version:      31
```

### **Generate public key from private key**

```text
ssh-keygen -y -f ~/.ssh/id_rsa > ~/.ssh/id_rsa.pub
```

### **Copy your default public key to remote user**

```text
ssh-copy-id <user_name>@<server_IP>
# then you need to enter the password
# and next time you won't need to enter password when ssh to that user
```

### **Copy default public key to remote user using the required private key \(e.g. use your mykey.pem key to copy your id\_rsa.pub to the remote user\)**

```text
# before you need to use mykey.pem to ssh to remote user.
ssh-copy-id -i ~/.ssh/id_rsa.pub -o "IdentityFile ~/Downloads/mykey.pem" <user_name>@<server_IP>
# now you don't need to use key to ssh to that user.
```

### **SSH Agent Forwarding**

```text
# To bring your key with you when ssh to serverA, then ssh to serverB from serverA using the key.
ssh-agent
ssh-add /path/to/mykey.pem
ssh -A <username>@<IP_of_serverA>
# Next you can ssh to serverB
ssh <username>@<IP_of_serverB>
```

### **Set the default user and key for a host when using SSH**

```text
# add the following to ~/.ssh/config
Host myserver
  User myuser
  IdentityFile ~/path/to/mykey.pem

# Next, you could run "ssh myserver" instead of "ssh -i ~/path/to/mykey.pem myuser@myserver"
```

### **Follow the most recent logs from service**

```text
journalctl -u <service_name> -f
```

### **Eliminate the zombie**

```text
# A zombie is already dead, so you cannot kill it. You can eliminate the zombie by killing its parent.
# First, find PID of the zombie
ps aux| grep 'Z'
# Next find the PID of zombie's parent
pstree -p -s <zombie_PID>
# Then you can kill its parent and you will notice the zombie is gone.
sudo kill 9 <parent_PID>
```

### **Show memory usage**

```text
free -c 10 -mhs 1
# print 10 times, at 1 second interval
```

### **Display CPU and IO statistics for devices and partitions.**

```text
# refresh every second
iostat -x -t 1
```

### **Display bandwidth usage on an network interface \(e.g. enp175s0f0\)**

```text
iftop -i enp175s0f0
```

### **Tell how long the system has been running and number of users**

```text
uptime
```

### **Check if it's root running**

```text
if [ "$EUID" -ne 0 ]; then
        echo "Please run this as root"
        exit 1
fi
```

### **Change shell of a user \(e.g. bonnie\)**

```text
chsh -s /bin/sh bonnie
# /etc/shells: valid login shells
```

### **Change root / fake root / jail \(e.g. change root to newroot\)**

```text
chroot /home/newroot /bin/bash

# To exit chroot
exit
```

### **Display file status \(size; access, modify and change time, etc\) of a file \(e.g. filename.txt\)**

```text
stat filename.txt
```

### **Snapshot of the current processes**

```text
ps aux
```

### **Display a tree of processes**

```text
pstree
```

### **Find maximum number of processes**

```text
cat /proc/sys/kernel/pid_max
```

### **Print or control the kernel ring buffer**

```text
dmesg
```

### **Show IP address**

```text
$ip add show

# or
ifconfig
```

### **Print previous and current SysV runlevel**

```text
runlevel

# or
who -r
```

### **Change SysV runlevel \(e.g. 5\)**

```text
init 5
#or
telinit 5
```

### **Display all available services in all runlevels,**

```text
chkconfig --list
# update-rc.d equivalent to chkconfig in ubuntu
```

### **Check system version**

```text
cat /etc/*-release
```

### **Linux Programmer's Manuel: hier- description of the filesystem hierarchy**

```text
man hier
```

### **Control the systemd system and service manager**

```text
# e.g. check the status of cron service
systemctl status cron.service

# e.g. stop cron service
systemctl stop cron.service
```

### **List job**

```text
jobs -l
```

### **Run a program with modified priority \(e.g. ./test.sh\)**

```text
# nice value is adjustable from -20 (most favorable) to +19
# the nicer the application, the lower the priority
# Default niceness: 10; default priority: 80

nice -10 ./test.sh
```

### **Export PATH**

```text
export PATH=$PATH:~/path/you/want
```

### **Make file executable**

```text
chmod +x filename
# you can now ./filename to execute it
```

### **Print system information**

```text
uname -a

# Check system hardware-platform (x86-64)
uname -i
```

### **Surf the net**

```text
links www.google.com
```

### **Add user, set passwd**

```text
useradd username
passwd username
```

### **Edit PS1 variable for bash \(e.g. displaying the whole path\)**

```text
1. vi ~/.bash_profile
2. export PS1='\u@\h:\w\$'
# $PS1 is a variable that defines the makeup and style of the command prompt
# You could use emojis and add timestamp to every prompt using the following value:
# export PS1="\t@🦁:\w\$ "
3. source ~/.bash_profile
```

### **Edit environment setting \(e.g. alias\)**

```text
1. vi ~/.bash_profile
2. alias pd="pwd" //no more need to type that 'w'!
3. source ~/.bash_profile
```

### **Print all alias**

```text
alias -p
```

### **Unalias \(e.g. after alias ls='ls --color=auto'\)**

```text
unalias ls
```

### **Set and unset shell options**

```text
# print all shell options
shopt

# to unset (or stop) alias
shopt -u expand_aliases

# to set (or start) alias
shopt -s expand_aliases
```

### **List environment variables \(e.g. PATH\)**

```text
echo $PATH
# list of directories separated by a colon
```

### **List all environment variables for current user**

```text
env
```

### **Unset environment variable \(e.g. unset variable 'MYVAR'\)**

```text
unset MYVAR
```

### **Show partition format**

```text
lsblk
```

### **Inform the OS of partition table changes**

```text
partprobe
```

### **Soft link program to bin**

```text
ln -s /path/to/program /home/usr/bin
# must be the whole path to the program
```

### **Show hexadecimal view of data**

```text
hexdump -C filename.class
```

### **Jump to different node**

```text
rsh node_name
```

### **Check port \(active internet connection\)**

```text
netstat -tulpn
```

### **Print resolved symbolic links or canonical file names**

```text
readlink filename
```

### **Find out the type of command and where it link to \(e.g. python\)**

```text
type python
# python is /usr/bin/python
# There are 5 different types, check using the 'type -f' flag
# 1. alias    (shell alias)
# 2. function (shell function, type will also print the function body)
# 3. builtin  (shell builtin)
# 4. file     (disk file)
# 5. keyword  (shell reserved word)

# You can also use `which`
which python
# /usr/bin/python
```

### **List all functions names**

```text
declare -F
```

### **List total size of a directory**

```text
du -hs .

# or
du -sb
```

### **Copy directory with permission setting**

```text
cp -rp /path/to/directory
```

### **Store current directory**

```text
pushd .

# then pop
popd

#or use dirs to display the list of currently remembered directories.
dirs -l
```

### **Show disk usage**

```text
df -h

# or
du -h

#or
du -sk /var/log/* |sort -rn |head -10
```

### **check the Inode utilization**

```text
df -i
# Filesystem      Inodes  IUsed   IFree IUse% Mounted on
# devtmpfs        492652    304  492348    1% /dev
# tmpfs           497233      2  497231    1% /dev/shm
# tmpfs           497233    439  496794    1% /run
# tmpfs           497233     16  497217    1% /sys/fs/cgroup
# /dev/nvme0n1p1 5037976 370882 4667094    8% /
# tmpfs           497233      1  497232    1% /run/user/1000
```

### **Show all file system type**

```text
df -TH
```

### **Show current runlevel**

```text
runlevel
```

### **Switch runlevel**

```text
init 3

#or
telinit 3
```

### **Permanently modify runlevel**

```text
1. edit /etc/init/rc-sysinit.conf
2. env DEFAULT_RUNLEVEL=2
```

### **Become root**

```text
su
```

### **Become somebody**

```text
su somebody
```

### **Report user quotes on device**

```text
repquota -auvs
```

### **Get entries in a number of important databases**

```text
getent database_name

# (e.g. the 'passwd' database)
getent passwd
# list all user account (all local and LDAP)

# (e.g. fetch list of grop accounts)
getent group
# store in database 'group'
```

### **Change owner of file**

```text
chown user_name filename
chown -R user_name /path/to/directory/
# chown user:group filename
```

### **Mount and unmount**

```text
# e.g. Mount /dev/sdb to /home/test
mount /dev/sdb /home/test

# e.g. Unmount /home/test
umount /home/test
```

### **List current mount detail**

```text
mount
# or
df
```

### **List current usernames and user-numbers**

```text
cat /etc/passwd
```

### **Get all username**

```text
getent passwd| awk '{FS="[:]"; print $1}'
```

### **Show all users**

```text
compgen -u
```

### **Show all groups**

```text
compgen -g
```

### **Show group of user**

```text
group username
```

### **Show uid, gid, group of user**

```text
id username

# variable for UID
echo $UID
```

### **Check if it's root**

```text
if [ $(id -u) -ne 0 ];then
    echo "You are not root!"
    exit;
fi
# 'id -u' output 0 if it's not root
```

### **Find out CPU information**

```text
more /proc/cpuinfo

# or
lscpu
```

### **Set quota for user \(e.g. disk soft limit: 120586240; hard limit: 125829120\)**

```text
setquota username 120586240 125829120 0 0 /home
```

### **Show quota for user**

```text
quota -v username
```

### **Display current libraries from the cache**

```text
ldconfig -p
```

### **Print shared library dependencies \(e.g. for 'ls'\)**

```text
ldd /bin/ls
```

### **Check user login**

```text
lastlog
```

### **Check last reboot history**

```text
last reboot
```

### **Edit path for all users**

```text
joe /etc/environment
# edit this file
```

### **Show and set user limit**

```text
ulimit -u
```

### **Print out number of cores/ processors**

```text
nproc --all
```

### **Check status of each core**

```text
1. top
2. press '1'
```

### **Show jobs and PID**

```text
jobs -l
```

### **List all running services**

```text
service --status-all
```

### **Schedule shutdown server**

```text
shutdown -r +5 "Server will restart in 5 minutes. Please save your work."
```

### **Cancel scheduled shutdown**

```text
shutdown -c
```

### **Broadcast to all users**

```text
wall -n hihi
```

### **Kill all process of a user**

```text
pkill -U user_name
```

### **Kill all process of a program**

```text
kill -9 $(ps aux | grep 'program_name' | awk '{print $2}')
```

### **Set gedit preference on server**

```text
# You might have to install the following:

apt-get install libglib2.0-bin;
# or
yum install dconf dconf-editor;
yum install dbus dbus-x11;

# Check list
gsettings list-recursively

# Change some settings
gsettings set org.gnome.gedit.preferences.editor highlight-current-line true
gsettings set org.gnome.gedit.preferences.editor scheme 'cobalt'
gsettings set org.gnome.gedit.preferences.editor use-default-font false
gsettings set org.gnome.gedit.preferences.editor editor-font 'Cantarell Regular 12'
```

### **Add user to a group \(e.g add user 'nice' to the group 'docker', so that he can run docker without sudo\)**

```text
sudo gpasswd -a nice docker
```

### **Pip install python package without root**

```text
1. pip install --user package_name
2. You might need to export ~/.local/bin/ to PATH: export PATH=$PATH:~/.local/bin/
```

### **Removing old linux kernels \(when /boot almost full...\)**

```text
1. uname -a  #check current kernel, which should NOT be removed
2. sudo apt-get purge linux-image-X.X.X-X-generic  #replace old version
```

### **Change hostname**

```text
sudo hostname your-new-name

# if not working, do also:
hostnamectl set-hostname your-new-hostname
# then check with:
hostnamectl
# Or check /etc/hostname

# If still not working..., edit:
/etc/sysconfig/network
/etc/sysconfig/network-scripts/ifcfg-ensxxx
#add HOSTNAME="your-new-hostname"
```

### **List installed packages**

```text
apt list --installed

# or on Red Hat:
yum list installed
```

### **Check for package update**

```text
apt list --upgradeable

# or
sudo yum check-update
```

### **Run yum update excluding a package \(e.g. do not update php packages\)**

```text
sudo yum update --exclude=php*
```

### **Check which file make the device busy on umount**

```text
lsof /mnt/dir
```

### **When sound not working**

```text
killall pulseaudio
# then press Alt-F2 and type in pulseaudio
```

### **When sound not working**

```text
killall pulseaudio
```

### **List information about SCSI devices**

```text
lsscsi
```

### **Tutorial for setting up your own DNS server**

[http://onceuponmine.blogspot.tw/2017/08/set-up-your-own-dns-server.html](http://onceuponmine.blogspot.tw/2017/08/set-up-your-own-dns-server.html)

### **Tutorial for creating a simple daemon**

[http://onceuponmine.blogspot.tw/2017/07/create-your-first-simple-daemon.html](http://onceuponmine.blogspot.tw/2017/07/create-your-first-simple-daemon.html)

### **Tutorial for using your gmail to send email**

[http://onceuponmine.blogspot.tw/2017/10/setting-up-msmtprc-and-use-your-gmail.html](http://onceuponmine.blogspot.tw/2017/10/setting-up-msmtprc-and-use-your-gmail.html)

### **Using telnet to test open ports, test if you can connect to a port \(e.g 53\) of a server \(e.g 192.168.2.106\)**

```text
telnet 192.168.2.106 53
```

### **Change network maximum transmission unit \(mtu\) \(e.g. change to 9000\)**

```text
ifconfig eth0 mtu 9000
```

### **Get pid of a running process \(e.g python\)**

```text
pidof python

# or
ps aux|grep python
```

### **Check status of a process using PID**

```text
ps -p <PID>

#or
cat /proc/<PID>/status
cat /proc/<PID>/stack
cat /proc/<PID>/stat
```

### **NTP**

```text
# Start ntp:
ntpd

# Check ntp:
ntpq -p
```

### **Remove unnecessary files to clean your server**

```text
sudo apt-get autoremove
sudo apt-get clean
sudo rm -rf ~/.cache/thumbnails/*

# Remove old kernal:
sudo dpkg --list 'linux-image*'
sudo apt-get remove linux-image-OLDER_VERSION
```

### **Increase/ resize root partition \(root partition is an LVM logical volume\)**

```text
pvscan
lvextend -L +130G /dev/rhel/root -r
# Adding -r will grow filesystem after resizing the volume.
```

### **Create a UEFI Bootable USB drive \(e.g. /dev/sdc1\)**

```text
sudo dd if=~/path/to/isofile.iso of=/dev/sdc1 oflag=direct bs=1048576
```

### **Locate and remove a package**

```text
sudo dpkg -l | grep <package_name>
sudo dpkg --purge <package_name>
```

### **Create a ssh tunnel**

```text
ssh -f -L 9000:targetservername:8088 root@192.168.14.72 -N
#-f: run in background; -L: Listen; -N: do nothing
#the 9000 of your computer is now connected to the 8088 port of the targetservername through 192.168.14.72
#so that you can see the content of targetservername:8088 by entering localhost:9000 from your browser.
```

### **Get process ID of a process \(e.g. sublime\_text\)**

```text
#pidof
pidof sublime_text

#pgrep, you don't have to type the whole program name
pgrep sublim

#pgrep, echo 1 if process found, echo 0 if no such process
pgrep -q sublime_text && echo 1 || echo 0

#top, takes longer time
top|grep sublime_text
```

### **Some benchmarking tools for your server**

[aio-stress](https://openbenchmarking.org/test/pts/aio-stress) - AIO benchmark.  
[bandwidth](https://zsmith.co/bandwidth.html) - memory bandwidth benchmark.  
[bonnie++](https://www.coker.com.au/bonnie++/) - hard drive and file system performance benchmark.  
[dbench](https://dbench.samba.org/) - generate I/O workloads to either a filesystem or to a networked CIFS or NFS server.  
[dnsperf](https://www.dnsperf.com/) - authorative and recursing DNS servers.  
[filebench](https://github.com/filebench/filebench) - model based file system workload generator.  
[fio](https://linux.die.net/man/1/fio) - I/O benchmark.  
[fs\_mark](https://github.com/josefbacik/fs_mark) - synchronous/async file creation benchmark.  
[httperf](https://github.com/httperf/httperf) - measure web server performance.  
[interbench](https://github.com/ckolivas/interbench) - linux interactivity benchmark.  
[ioblazer](https://labs.vmware.com/flings/ioblazer) - multi-platform storage stack micro-benchmark.  
[iozone](http://www.iozone.org/) - filesystem benchmark.  
[iperf3](https://iperf.fr/iperf-download.php) - measure TCP/UDP/SCTP performance.  
[kcbench](https://github.com/knurd/kcbench) - kernel compile benchmark, compiles a kernel and measures the time it takes.  
[lmbench](http://www.bitmover.com/lmbench/) - Suite of simple, portable benchmarks.  
[netperf](https://github.com/HewlettPackard/netperf) - measure network performance, test unidirectional throughput, and end-to-end latency.  
[netpipe](https://linux.die.net/man/1/netpipe) - network protocol independent performance evaluator.  
[nfsometer](http://wiki.linux-nfs.org/wiki/index.php/NFSometer) - NFS performance framework.  
[nuttcp](https://www.nuttcp.net/Welcome%20Page.html) - measure network performance.  
[phoronix-test-suite](https://www.phoronix-test-suite.com/) - comprehensive automated testing and benchmarking platform.  
[seeker](https://github.com/fidlej/seeker) - portable disk seek benchmark.  
[siege](https://github.com/JoeDog/siege) - http load tester and benchmark.  
[sockperf](https://github.com/Mellanox/sockperf) - network benchmarking utility over socket API.  
[spew](https://linux.die.net/man/1/spew) - measures I/O performance and/or generates I/O load.  
[stress](https://people.seas.harvard.edu/~apw/stress/) - workload generator for POSIX systems.  
[sysbench](https://github.com/akopytov/sysbench) - scriptable database and system performance benchmark.  
[tiobench](https://github.com/mkuoppal/tiobench) - threaded IO benchmark.  
[unixbench](https://github.com/kdlucas/byte-unixbench) - the original BYTE UNIX benchmark suite, provide a basic indicator of the performance of a Unix-like system.  
[wrk](https://github.com/wg/wrk) - HTTP benchmark.

### **Performance monitoring tool - sar**

```text
# installation
# It collects the data every 10 minutes and generate its report daily. crontab file (/etc/cron.d/sysstat) is responsible for collecting and generating reports.
yum install sysstat
systemctl start sysstat
systemctl enable sysstat

# show CPU utilization 5 times every 2 seconds.
sar 2 5

# show memory  utilization 5 times every 2 seconds.
sar -r 2 5

# show paging statistics 5 times every 2 seconds.
sar -B 2 5

# To generate all network statistic:
sar -n ALL

# reading SAR log file using -f
sar -f /var/log/sa/sa31|tail
```

### **Reading from journal file**

```text
journalctl --file ./log/journal/a90c18f62af546ccba02fa3734f00a04/system.journal  --since "2020-02-11 00:00:00"
```

### **Show a listing of last logged in users.**

```text
lastb
```

### **Show a listing of current logged in users, print information of them**

```text
who
```

### **Show who is logged on and what they are doing**

```text
w
```

### **Print the user names of users currently logged in to the current host.**

```text
users
```

### **Stop tailing a file on program terminate**

```text
tail -f --pid=<PID> filename.txt
# replace <PID> with the process ID of the program.
```

### **List all enabled services**

```text
systemctl list-unit-files|grep enabled
```

