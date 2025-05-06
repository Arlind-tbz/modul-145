# Cisco

## 1. Navigate the IOS

[Abgabe 1](./Abgaben/01_Packet%20Tracer%20-%20Navigate%20the%20IOS.pka)

### Hilfe & Befehle
```bash
?
t?
te?
enable
show running-conf
configure terminal
clock set 15:00:00 31 Jan 2035
```

## 2. Switch Grundkonfiguration

[Abgabe 2](./Abgaben/02_Packet%20Tracer%20-%20Configure%20Initial%20Switch%20Settings.pka)

### Basis Setup

```bash
enable
configure terminal
hostname S1
line console 0
password letmein
login
exit
enable password c1$c0
enable secret itsasecret
banner motd "Unauthorized Access"
service password-encryption
exit
copy running-config startup-config
```

```bash
enable
configure terminal
hostname S2
line console 0
password letmein
login
exit
enable password c1$c0
enable secret itsasecret
banner motd "Unauthorized Access"
service password-encryption
exit
copy running-config startup-config
```

## 3. Netzwerkdiagnose

[Abgabe 3](./Abgaben/03_Packet%20Tracer%20-%20Implement%20Basic%20Connectivity.pka)

```bash
enable
configure terminal
hostname S1
banner motd "Unauthorized Access"
line console 0
password cisco
login
exit
enable secret class
exit
configure terminal
interface vlan 1
ip address 192.168.1.253 255.255.255.0
no shutdown
copy running-config startup-config
```

```bash
enable
configure terminal
hostname S2
banner motd "Unauthorized Access"
line console 0
password cisco
login
exit
enable secret class
exit
configure terminal
interface vlan 1
ip address 192.168.1.254 255.255.255.0
no shutdown
copy running-config startup-config
```

```bash
PC1: 192.168.1.1 255.255.255.0
PC2: 192.168.1.2 255.255.255.0
```

## 4. Subnetting & Routing

[Abgabe 4](./Abgaben/04_Packet%20Tracer%20-%20Identify%20MAC%20and%20IP%20Addresses.pka)

### Subnet Konfiguration
```bash
interface Gig0/0
ip address 192.168.0.1 255.255.255.192
no shutdown

interface Gig0/1
ip address 192.168.0.65 255.255.255.192
no shutdown
```

## 5. VLAN Setup

[Abgabe 5](./Abgaben/05_Packet%20Tracer%20-%20Examine%20the%20ARP%20Table.pka)

### VLAN Erstellung
```bash
vlan 10
name Faculty/Staff
vlan 20
name Students
vlan 99
name Management
```

### Port Zuweisung
```bash
interface f0/11
switchport mode access
switchport access vlan 10
```

### Trunk Konfiguration
```bash
interface Gig0/1
switchport mode trunk
switchport trunk native vlan 99
```

## 6. Inter-VLAN Routing

[Abgabe 6](./Abgaben/06_Packet%20Tracer%20-%20Subnet%20an%20IPv4%20Network.pka)

### Customrouter
```bash
enable
configure terminal
hostname CustomerRouter

enable secret Class123
line console 0
password Cisco123
login
exit

interface g0/0
ip address 192.168.0.1 255.255.255.192
no shutdown
exit

interface g0/1
ip address 192.168.0.65 255.255.255.192
no shutdown
exit

interface s0/1/0
ip address 209.165.201.2 255.255.255.252
no shutdown
exit

end
write memory
```

### LAN-A

```bash
enable
configure terminal
interface vlan1
ip address 192.168.0.2 255.255.255.192
no shutdown
exit
ip default-gateway 192.168.0.1
end
write memory
```

### LAN-B

```bash
enable
configure terminal
interface vlan1
ip address 192.168.0.66 255.255.255.192
no shutdown
exit
ip default-gateway 192.168.0.65
end
write memory
```

### PC-A

```bash
192.168.0.62 255.255.255.192 192.168.0.1
```

### PC-B

```bash
192.168.0.126 255.255.255.192 192.168.0.65
```
