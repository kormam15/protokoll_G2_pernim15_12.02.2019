# 6. Protokoll

![](https://www.htl-kaindorf.at/images/startpage/logoMecha.png) 

Name: Perl Nicolas  
Kat.-Nr.: 10  
Klasse: 4AHME  
Gruppe: 2  

| Anwesend | Abwesend |  
| --------------------------------------- | -------- |  
| M.Korrenn, A.Murko, D.Orthofer, N.Perl,  J.Skof, S.Szapacs | - | 

___

### Themen-Übersicht
 - **1)** - Easyprogrammer 
 - **2)** - Intelligenter Sensor 
 - **3)** - Feldbus 
     -  **3.1)** - Modbus 
 
___

## 1.) - Easyprogrammer -

Bei Netbeans wird unter `Properties` und `Run` ein bestimmtes Command aufgerufen.  
Dieses checkt aufgrund der übergebenen Argumente, was aufgerufen werden soll.  
-> ruft Easyprogrammer auf  

___

## 2.) - Intelligenter Sensor -

Ein intelligenter besitzt eine digitale Elektronik. Er kann selbst Informationen verarbeiten und bietet diese auf standardisierten Schnittstellen an. Standardisierte Schnittstellen haben den Vorteil der Kompatibilität. Ein Beispiel für einen intelligenten Sensor wäre der Temperatorsensor auf unserem µC.  
Ein unintelligenter Sensor (PT100) kann dies im Gegensatz dazu nicht. 

Sensoren befinden sich in der Automatisierungspyramide auf der 2. Ebene (Feldebene).  

___

## 3.) - Feldbus -

Ein Feldbus ist ein Bussystem, das in einer Anlage Feldgeräte wie Sensoren und Aktoren zwecks Kommunikation mit einem Automatisierungsgerät verbindet. Wenn mehrere Kommunikationsteilnehmer ihre Nachrichten über dieselbe Leitung senden, dann muss festgelegt sein, wer (Kennung) was (Messwert, Befehl) wann (Initiative) sagt. Hierfür gibt es normierte Protokolle. 
Quelle: [Wikipedia](https://de.wikipedia.org/wiki/Feldbus)  
LAN und WLAN-Netzwerke sind keine Feldbussysteme, da diese nicht Echtzeitfähig und viel zu kompliziert sind. 

#### Einsatzgebiete von Feldbussystemen 

| Industrie | Auto | Gebäude |  
| --------------------------------------- | -------- | ------- |  
| Profibus | LIN | KMX | 
| Powerlink | CAN | Modbus | 
| Flexray | ... | CAN | 

Wir lernen nun speziell über den Modbus, da dieser in der Praxis häufig vorkommt, komplett frei/offen ist und relativ einfach zu verstehen ist.  

-> In Zukunft werden sog. REST Server benutzt werden.  
Der Zweck von REST liegt schwerpunktmäßig auf der Maschine-zu-Maschine-Kommunikation. Der Vorteil von REST liegt darin, dass im WWW bereits ein Großteil der für REST nötigen Infrastruktur (z. B. Web- und Application-Server, HTTP-fähige Clients) vorhanden ist, und viele Web-Dienste per se REST-konform sind. Über Smartphones und Tablets kann so ein Steuern und Regeln erfolgen.  

Quelle: [Wikipedia](https://de.wikipedia.org/wiki/Representational_State_Transfer)  



___
