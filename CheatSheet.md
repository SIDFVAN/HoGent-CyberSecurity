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
