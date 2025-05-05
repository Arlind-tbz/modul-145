# Cisco

## 1. Navigate the IOS

[Abgabe 1](./Abgaben/01_Packet%20Tracer%20-%20Navigate%20the%20IOS.pka)

### Hilfe & Befehle
```bash
?
t?
te?
enable
show running-config
configure terminal
clock set 15:00:00 31 Jan 2035
```

## 2. Switch Grundkonfiguration

[Abgabe 2](./Abgaben/02_Packet%20Tracer%20-%20Configure%20Initial%20Switch%20Settings.pka)

### Basis Setup
```bash
hostname S1
line console 0
password letmein
login
enable secret itsasecret
banner motd "Unauthorized Access"
service password-encryption
copy running-config startup-config
```

### Interface Konfiguration
```bash
interface vlan 1
ip address 192.168.1.253 255.255.255.0
no shutdown
```

## 3. Netzwerkdiagnose

[Abgabe 3](./Abgaben/03_Packet%20Tracer%20-%20Implement%20Basic%20Connectivity.pka)

### Ping & ARP
```bash
ping 192.168.1.254
arp -d
arp -a
show mac-address-table
show arp
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

### Sub-Interfaces
```bash
interface Gig0/1.10
encapsulation dot1Q 10
ip address 172.17.10.1 255.255.255.0

interface Gig0/1.20
encapsulation dot1Q 20
ip address 172.17.20.1 255.255.255.0
```
