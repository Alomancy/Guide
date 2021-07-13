# Parrot OS customisation

## VPNpanel.sh 

```text
#!/bin/bash
htbip=$(ip addr | grep tun0 | grep inet | grep 10. | tr -s " " | cut -d " " -f 3 | cut -d "/" -f 1)
lab=$(cat /etc/openvpn/*.conf | grep "remote " | cut -d " " -f 2 | cut -d "." -f 1 | cut -d "-" -f 2-)

if [[ $htbip == *"10."* ]]
then
   gwip=$(ip route | grep tun0 | grep via | cut -d " " -f 3)
   ping=$(ping -c 1 $gwip -W 1 | sed '$!d;s|.*/\([0-9.]*\)/.*|\1|' | cut -c1-4)
   echo "VPN: $lab ($htbip) [$ping ms]"
else
   echo "VPN: Disconnected"
fi

```

![](../.gitbook/assets/image%20%2841%29.png)

