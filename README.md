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

### 3.1) - Modbus - 

Das Modbus-Protokoll ist ein Kommunikationsprotokoll, welches auf einem Request/Response Prinzip basiert. Es wurde 1979 von Gould-Modicon für die Kommunikation mit seinen SPS ins Leben gerufen. In der Industrie hat sich der Modbus zu einem Standard entwickelt, da es sich um ein offenes Protokoll handelt. 
Beispiel: Arduino Nano über UART - Standardisierte Bussysteme (zB UART) haben den Vorteil der Kompartibilität. 

![]()

 Bei der eigentlichen Datenübertragung werden drei Varianten unterschieden:

| Art | Übertragung |  
| --------------------------------------- | -------- | 
| Modbus ASCII | Textuelle byteweise Übertragung von Daten - Frames beginnen mit einem Doppelpunkt | 
| Modbus RTU | Binäre byteweise Übertragung von Daten | 
|  Modbus TCP | Übertragung der Daten in TCP Paketen | 

Der Kommunikationsablauf beruht auf einem **Server/Client Prinzip**. Der Client (z.B. PC) sendet einen Request zum Server (z.B. Aktor). Dieser antworter mit einer Response. 

![]()

Jeder Busteilnehmer muss eine eindeutige Adresse haben, wobei Adresse 0 für einen Broadcast (an alle Knoten) reserviert ist. 
Der Function-Code ist ein Byte, dass die Art des Requests bzw. der Response genauer festlegt. Für Requests und gültige Responses sind die Werte 1 bis 127 vorgesehen. Für Exception-Responses, also die Rückmeldung eines Fehlers, sind die Werte von 128 bis 255 zu verwenden. Der Function-Code 0 ist nicht erlaubt. 

Der Socket ist der sog. Modbusserver. Er besitzt die Portnummer 502. Erst über die IP-Adresse und die Portnummer (Socket) kann der Rechner etwas mit der Information anfangen. 
-> Warum keine Adresse + Errorcheck? 
Aufgrund der IP-Adresse und der Prüfsumme (Checksum) 

### Datenmodell

1.1 

Daten-Modell

Das Modbus Daten-Modell unterscheidet vier Tabellen (Adressräume) für:

| Tabelle | Beschreibung | Beispiel | 
| ----------- | ---------- | ---------- | 
| Discrete Input | Ein Discrete Input ist ein einzelnes Bit, das nur gelesen werden kann | Taster |  
| Coils (Spulen) | Eine Coil ist ein Bit das gelesen und beschrieben werden kann | LED | 
| Input Registers | Ein Input-Register ist ein 16-Bit Wert der nur gelesen werden kann | Temperatursensor | 
| Hold-Registers | Ein Hold-Register ist ein 16-Bit Wert der gelesen und beschrieben werden kann | 7-Segment-Anzeige | 

Pro Tabelle können in einer Protocol Data Unit Werte von 0 bis 65535 (dual codierbar in 16-Bit) verwendet werden. Im Modbus data model werden hingegen Adresswerte von 1 bis 65536 verwendet. Ein Adress-Mapping ist daher erforderlich. 
z.B. Adresse 23 bekommen bei Wert 22 


___
