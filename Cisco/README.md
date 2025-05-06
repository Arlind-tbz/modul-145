# Cisco

## 1. Navigation im IOS

Mit dem Fragezeichen `?` wird kontextbezogene Hilfe angezeigt:

* `?` listet alle verfügbaren Befehle.
* `t?` zeigt alle Befehle, die mit „t“ beginnen (z. B. `telnet`, `terminal`, `traceroute`).
* `te?` schränkt die Auswahl weiter ein (z. B. `telnet`, `terminal`).

Nach dem Start befindet man sich im User EXEC Mode (`S1>`).
Mit dem Befehl `enable` wechselt man in den Privileged EXEC Mode (`S1#`).

Beispiel:

* `S1> enable` → `S1#`
* `S1> en<Tab>` vervollständigt den Befehl zu `enable`, sofern eindeutig.

Wenn mehrere Befehle denselben Anfang haben, erfolgt keine automatische Vervollständigung.

Im Privileged EXEC Mode erfolgt der Wechsel in den Konfigurationsmodus über `configure` oder `conf`.
Eingabe: `S1# configure` → anschließend bestätigt man mit Enter, der Prompt wechselt zu `S1(config)#`.

Zurück in den EXEC-Modus gelangt man mit:

* `exit`, `end` oder `Ctrl+Z`.

Die aktuelle Uhrzeit kann mit `show clock` angezeigt werden.
Um die Uhrzeit zu setzen, wird `clock set` verwendet.

Beispiel:

```bash
S1# clock set 15:00:00 31 Jan 2035
```

Zur Kontrolle:

```bash
S1# show clock
```

Fehlermeldungen bei falscher oder unvollständiger Eingabe:

* `% Incomplete command`
* `% Invalid input detected at '^' marker`

Beispiele:

* `S1# cl<Tab>` → keine Vervollständigung möglich
* `S1# clock` → `% Incomplete command`
* `S1# clock set 25:00:00` → `% Invalid input`
* `S1# clock set 15:00:00 32` → `% Invalid input`

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

## 4. Subnetting und Routing

### 4.1 Lokale Kommunikation (Ping im selben Subnetz)

#### Beispiel: Ping von 172.16.31.5 nach 172.16.31.2

| Gerät       | Ziel-MAC             | Quell-MAC            | Quell-IP    | Ziel-IP     |
| ----------- | -------------------- | -------------------- | ----------- | ----------- |
| 172.16.31.5 | 00:0C:85\:CC:1D\:A7  | 00\:D0\:D3:11\:C7:88 | 172.16.31.5 | 172.16.31.2 |
| Switch1     | 00:0C:85\:CC:1D\:A7  | 00\:D0\:D3:11\:C7:88 | -           | -           |
| Hub         | -                    | -                    | -           | -           |
| 172.16.31.2 | 00\:D0\:D3:11\:C7:88 | 00:0C:85\:CC:1D\:A7  | 172.16.31.2 | 172.16.31.5 |

#### Weitere Tests

**Ping von 172.16.31.3 nach 172.16.31.2**

| Gerät       | Ziel-MAC            | Quell-MAC           | Quell-IP    | Ziel-IP     |
| ----------- | ------------------- | ------------------- | ----------- | ----------- |
| 172.16.31.3 | 00:0C:85\:CC:1D\:A7 | 00:60:70:36:28:49   | 172.16.31.3 | 172.16.31.2 |
| Hub         | -                   | -                   | -           | -           |
| 172.16.31.2 | 00:60:70:36:28:49   | 00:0C:85\:CC:1D\:A7 | 172.16.31.2 | 172.16.31.3 |

**Ping von 172.16.31.5 nach 172.16.31.4**

| Gerät       | Ziel-MAC             | Quell-MAC            | Quell-IP    | Ziel-IP     |
| ----------- | -------------------- | -------------------- | ----------- | ----------- |
| 172.16.31.5 | 00:0C\:CF:0B\:BC:80  | 00\:D0\:D3:11\:C7:88 | 172.16.31.5 | 172.16.31.4 |
| Switch1     | 00:0C\:CF:0B\:BC:80  | 00\:D0\:D3:11\:C7:88 | -           | -           |
| 172.16.31.4 | 00\:D0\:D3:11\:C7:88 | 00:0C\:CF:0B\:BC:80  | 172.16.31.4 | 172.16.31.5 |

### 4.2 Kommunikation mit anderem Subnetz (via Router)

**Ping von 172.16.31.5 nach 10.10.10.2**

| Gerät        | Ziel-MAC                  | Quell-MAC                 | Quell-IP    | Ziel-IP     |
| ------------ | ------------------------- | ------------------------- | ----------- | ----------- |
| 172.16.31.5  | 00\:D0\:BA:8E:74:1A       | 00\:D0\:D3:11\:C7:88      | 172.16.31.5 | 10.10.10.2  |
| Switch1      | 00\:D0\:BA:8E:74:1A       | 00\:D0\:D3:11\:C7:88      | -           | -           |
| Router       | 00:60:2F:84:4A\:B6        | 00\:D0:58:8C:24:01        | 172.16.31.5 | 10.10.10.2  |
| Switch0      | 00:60:2F:84:4A\:B6        | 00\:D0:58:8C:24:01        | -           | -           |
| Access Point | -                         | -                         | -           | -           |
| 10.10.10.2   | 00\:D0:58:8C:24:01 (WLAN) | 00:60:2F:84:4A\:B6 (WLAN) | 10.10.10.2  | 172.16.31.5 |

## 5. VLAN Setup

### 5.1 ARP-Anfrage

Ping von 172.16.31.2 nach 172.16.31.3 nach `arp -d`

* Ziel-MAC im Broadcast: `FF:FF:FF:FF:FF:FF`
* Anzahl ARP-Kopien über Switch: 3 (nur 1 erfolgreich)
* Ziel-IP: 172.16.31.3
* ARP-Antwort MACs:

  * Source: 0060.7036.2849
  * Destination: 000C.85CC.1DA7
* `arp -a`: Eintrag vorhanden, IP und MAC stimmen überein

### 5.2 MAC-Adresstabellen

**Traffic erzeugt mit:**

* `ping 172.16.31.4` von 172.16.31.2
* `ping 10.10.10.3` von 10.10.10.2
* Beide erfolgreich (je 4 Pakete)

**Switch1, `show mac-address-table`**

* Tabelle stimmt mit beobachtetem Traffic überein

**Switch0, `show mac-address-table`**

* Ebenfalls konsistent

### 5.3 ARP bei Routing

**Ping von 172.16.31.2 nach 10.10.10.1**

* `arp -a`: Neuer Eintrag für 172.16.31.1 (Gateway)
* ARP-Ziel-IP war nicht 10.10.10.1, sondern 172.16.31.1
* Grund: Ziel ist außerhalb des lokalen Netzes → ARP fragt Gateway ab

**Router1**

* `show mac-address-table`: keine Daten (Router speichern MACs nicht wie Switches)
* `show arp`: Eintrag für 172.16.31.2 vorhanden → MAC 000C.85CC.1DA7

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
