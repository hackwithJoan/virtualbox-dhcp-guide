# virtualbox-dhcp-guide
A step-by-step guide for setting up and removing a VirtualBox DHCP server.

## A practical guide I wrote while building my own VirtualBox lab.

This write‑up covers how I set up a DHCP server on an internal VirtualBox network, why I removed it later, and the exact commands I used. It’s clean, repeatable, and ideal for anyone building a controlled lab environment (CTFs, VulnHub machines, isolated networks, etc.).

### Why I Documented This
When I first started experimenting with internal networks in VirtualBox, I created a DHCP server to automate IP assignment. Later, after adding new machines, I didn’t need that DHCP server anymore — and removing it wasn’t immediately obvious.

This guide is the exact process I followed, written in a way that future‑me (and anyone else) can understand quickly.

### Navigate to the VirtualBox Director
VirtualBox commands only work when run from the folder containing vboxmanage.exe (unless added to PATH). On Windows, that’s here:

```cmd
cd "C:\Program Files\Oracle\VirtualBox"
```
Once you’re in this directory, you can run all VirtualBox management commands.

### 🔹 Create a DHCP Server on an Internal Network
I created a DHCP server for an internal network named intnet using this command:
```cmd
vboxmanage dhcpserver add --network=intnet --server-ip=xx.xx.x.x --lower-ip=xx.x.xxx --upper-ip=xx.x.xxx --netmask=xxx.xxx.xxx.0 --enable
```
### What this configuration means
Network name: intnet 
DHCP server IP: 10.xx.1.1  
IP range: 10.xx.1.110 → 10.xx.1.120  
Netmask: xxx.xxx.xxx.0  
Enabled: Yes

Any VM connected to intnet will automatically receive an IP in that range.

### 🔹 List All DHCP Servers
To see all DHCP servers currently registered in VirtualBox:
```cmd
vboxmanage list dhcpservers
```
#### You’ll typically see:

The default Host‑Only DHCP server

Any custom DHCP servers you’ve added (like intnet for mine)
