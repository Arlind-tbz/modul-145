# Netzwerkdokumentation

[Auftrag](https://gitlab.com/ch-tbz-it/Stud/m145/-/tree/main/10_Netzwerkdokumentation/02_Interpretieren)

## Wie lautet die Netzwerkadresse vom Standort Samedan?
- 192.168.3.0

## Auf welcher IP-Adresse befindet sich der AccessPoint in Bellinzona?
- 192.168.4.30

## In welchem VLAN befinden sich die Arbeitsplatz-PCs?
- Die Arbeitsplatz-PCs befinden sich im VLAN-2 (Office).

## Über welche IP-Adresse erreicht man den Manageable-Switch am Standort Chur?
- 192.168.2.253

## Welche IP-Adressen LAN-seitig und tunnelseitig ist der VPN-Gateway am Standort Bellinzona konfiguriert?
- **LAN-seitig:** 192.168.4.1
- **Tunnel-seitig:** 172.200.4.2

## Wie lautet der am Standort Samedan an den Arbeitsplatz-PCs eingetragene Standardgateway?
- 192.168.3.1

## Ein Aussendienstmitarbeiter benötigt Zugriff auf das Firmennetzwerk. Wie muss er seine VPN-SW IP-mässig konfigurieren?
- Die VPN-Software muss auf den **VPN-C (RAS)** Tunnel konfiguriert werden, mit der IP-Adresse **172.200.5.1/24**.

## Wer hat im Büro CAD Wasserbau die VoIP-Telefone installiert?
- abisang

## Wann wurde im Bistro der AccessPoint installiert?
- Am 23.7.14 durch rsauter (E8/1).

## Der IT-Mitarbeiter Rene Sauter (rsauter) verlässt die Firma. Welche Arbeiten bzw. Verantwortlichkeiten sind davon betroffen? Wenn würden Sie als zukünftigen Ansprechpartner bei Problemen vorschlagen?

- **Der IT-Mitarbeiter Rene Sauter (rsauter) verlässt die Firma. Betroffen sind folgende Verantwortlichkeiten:**

- Empfang EG Arbeitsplatz-PC (E1/11)
- CAD Tiefbau Workstation (E2/1)
- Bauleitbüro MF-Kopierer (E3/2)
- Bistro Access-Point (E8/1)

**Empfohlene Ansprechpartner:**
- **blaeuchli**
- **abisang**
- **rkundert**

## Wieviele RJ45-Steckdosen stehen Ihnen im Bauleiterbüro zur Verfügung und wieviele davon sind zurzeit noch nicht belegt?
- Es gibt insgesamt 8 Anschlüsse, davon sind 6 belegt und 2 frei.

## Im Büro CAD Tiefbau muss ein weiteres VoIP-Telefon zur Verfügung stehen. Wie soll diese Verbindung gepatched werden? Verlangt wird die Patchpanelbelegung und der Switch-Port.
- Patchpanel: E2/3
- Switch-Port: Port 24-47 im VLAN-1 (Telefon)

## Im Bistro soll eine Projektpräsentation stattfinden. Dafür muss eine Ethernetkabelverbindung bereitgestellt werden.
- Eine der freien Buchsen (z. B. E9/1 oder E9/2) kann für die Präsentation genutzt werden.
- Patchen zum Switch in das entsprechende VLAN (vermutlich Office-Netzwerk).

## Im Büro CAD Wasserbau soll temporär ein weiterer Arbeitsplatz eingerichtet werden. Wie werden Sie diese Aufgabe lösen?
- Nutzen Sie einen der freien RJ45-Anschlüsse (Patchpanel-Eintrag zeigt mehrere freie Ports).

## Wieviele Switchs stehen Ihnen am Standort Chur zur Verfügung?
- Es sind 2 Switches dokumentiert.

## Frau Sommer arbeitet an der CAD-Workstation und meldet Ihnen, dass sie keine Verbindung ins Internet mehr hat. Was werden Sie überprüfen?
- Verbindungskabel und Switch-Port
- IP-Konfiguration (Statische IP oder DHCP)
- DNS-Einstellungen
- Firewall-Regeln für ihren Arbeitsplatz
- Funktionsfähigkeit des Standardgateways 192.168.2.1

## Wie lautet die SSID des Churer-AccessPoint?
- Die SSID ist nicht erwähnt
