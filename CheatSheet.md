# Cheat Sheet FVAN

CyberSecurity and virtualisation

## Crack the zip

The zip file can be easily cracked using John the ripper using the default (builtin) word list:

```console
zip2john wifi-captures.zip > hash.txt
john hash.txt
```

## Crack the wifi

### WEP encryption 64 bit

```console
aircrack-ng -n 64 wep-easy-01.ivs
```

### WEP encryption 128 bit

```console
aircrack-ng -n 128 wep-medium-01.ivs
```

### WPA encryption

```console
aircrack-ng -w /usr/share/wordlists/rockyou.txt wpa-easy-01.cap
```

### WPA encryption (only one 4-way handshakes) (use **crunch**)

```console
sudo locale-gen en_US.UTF-8       # configure locale UTF-8
crunch 6 8 abcdef -o custom.txt   # create custom wordlist
aircrack-ng -w custom.txt wpa-medium-01.cap
```

### aircrack usage examples

<https://www.kali.org/tools/aircrack-ng/>

## Update locate

```console
sudo updatedb
```

## Wordlist

### Search wordlist (**locate**)

```console
locate wordlist
```

### Unzip wordlist

```console
cd /usr/share/wordlist/
sudo gzip -d rockyou.txt.gz
```

## Gateway + DNS

### Remove firewall

```console
dnf remove firewalld
```

### Enable routing

```console
modprobe iptable_nat
echo "net.ipv4.ip_forward = 1" >> /etc/sysctl.conf
sysctl -p /etc/sysctl.conf # reload sysctl.conf variables
sysctl net.ipv4.ip_forward       # Verify if IP forwarding is active
```

### check if nat is installed

```console
iptables -t nat -L
```

### Configure static IP

```console
dnf install nano          # Install basic text editor
nano /etc/sysconfig/network-scripts/ifcfg-enp0s8
```

```console
TYPE=Ethernet
BOOTPROTO=none
IPADDR=192.168.22.1
NETMASK=255.255.255.0
NAME=enp0s8
DEVICE=enp0s8
ONBOOT=yes
```

```console
systemctl reboot -i
```

Save the file, reboot the VM and verify the IP configuration (using ip a s).

### Configure NAT (enp0s3 connected to NAT, enp0s8 connected to internal)

```Console
iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
iptables -A FORWARD -i enp0s8 -j ACCEPT
```
