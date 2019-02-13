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

### 3.2) - Kommunikation -

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

#### **Modbus ASCII:** 
Hierbei werden die Frame-Bytes als ASCII-Text versendet. Für die Konfiguration der seriellen Schnittstelle wird standardmäßig 7E1 oder 7N2 verwendet -> nur 7 Daten-Bits! Geräte dürfen im Bedarfsfall aber auch eine davon abweichende Festlegung haben. 

|  | 7 | E | 1 |  | 
| --- | --- | --- | --- | --- | 
| Startbit | 7 Daten-Bits | Even Parity | 1 Stop-Bit | = 10 Bits | 


### 3.3) - Datenmodell - 

Das Modbus Daten-Modell unterscheidet vier Tabellen (Adressräume) für: 

| Tabelle | Beschreibung | Beispiel | 
| ----------- | ---------- | ---------- | 
| Discrete Input | Ein Discrete Input ist ein einzelnes Bit, das nur gelesen werden kann | Taster |  
| Coils (Spulen) | Eine Coil ist ein Bit das gelesen und beschrieben werden kann | LED | 
| Input Registers | Ein Input-Register ist ein 16-Bit Wert der nur gelesen werden kann | Temperatursensor | 
| Hold-Registers | Ein Hold-Register ist ein 16-Bit Wert der gelesen und beschrieben werden kann | 7-Segment-Anzeige | 

Pro Tabelle können in einer Protocol Data Unit Werte von 0 bis 65535 (dual codierbar in 16-Bit) verwendet werden. Im Modbus data model werden hingegen Adresswerte von 1 bis 65536 verwendet. Ein Adress-Mapping ist daher erforderlich. 
z.B. Adresse 23 bekommen bei Wert 22 

### 3.4) - Function-Codes - 

Der Function-Code in einem Modbus-Frame definiert die Bedeutung des Frames. 
Für Requests und Non-Error-Responses sind Werte zwischen 1 und 127 zulässig. Dieser Bereich ist in drei Kategorien unterteilt: Function Codes in den Bereichen 65-72 und 100-110 können vom Benutzer individuell vergeben werden, unter den übrigen Werten werden manche von Unternehmen für Produkte verwendet, andere widerum werden von der Modbus community definiert. 
Folgende Public Function Codes sind definiert: 

| Function-Code | Hex | Name | Typ | 
| --------------- | --------- | --------- | --- | 
| 1 | 01 | Read Coils | Bit | 
| 2 | 02 | Read Discrete Inputs | Bit | 
| 3 | 03 | Read Holding Registers | 16-Bit | 
| 4 | 04 | Read Input Register | 16-Bit | 
| 5 | 05 | Write Single Coil | Bit | 
| 6 | 06 | Write Single Register | 16-Bit | 
| 15 | 0F | Write Multiple Coils |	Bit | 
| 16 | 10 | Write Multiple Registers | 16-Bit | 

### 3.5) - Protokoll Definition - 

Ein Modbus-Gateway ist in der Lage verschiedene Modbus-Varianten miteinander zu verbinden, also zum Beispiel die Verbindung eines über die UART-Schnittstelle erreichbaren Sensors mit einem über TCP/IP erreichbaren PC. 
Das Modbus Application Layer Protocol definiert dabei als Frame sogenannte **Protocol Data Units** (PDU). Diese enthalten noch kein Adressierungsschema, da unterschiedliche Varianten (UART, TCP, ...) auch unterschiedliche Adressierungsarten verwenden. 
Die zusätzlichen Spezifikationen für die jeweiligen Varianten definieren dann auch zusätzliche Frame-Felder für die Adressierung und Fehlererkennung, wodurch dann die **Application Data Unit** (ADU) entsteht. 

Die maximale Größe einer ADU liegt bei Modbus ASCII/RTU bei 256 Bytes und bei Modbus TCP bei 260 Bytes. 

Der *Socket* ist der sog. Modbusserver. Er besitzt die Portnummer 502. Erst über die IP-Adresse und die Portnummer (Socket) kann der Rechner etwas mit der Information anfangen. Aufgrund der IP-Adresse und der Prüfsumme (Checksum) ist keine Adresse und kein Errorcheck nötig.  
Quelle: [http://modbus.org/](http://modbus.org/)

![](https://www.kynetics.com/docs/2018/images/xpduAdu.png.pagespeed.ic.56QXaR8Aqh.png)


| Function-Code | Adresse | Anzahl | 
| --------------- | --------- | -------- | 
| 04 | 0000 | 0001 | 

### 3.6) - Request PC -> µC -

Jeder Modbus Serial Line ASCII Frame hat folgenden Aufbau: 

| : | 0C | 04 | 0000 0001 | A8 | \r | \n |  
| --- | --- | --- | --------- | --- | --- | --- | 
| 3a | Korrenns Adresse | Function Code | Daten | LRC-Prüfsumme | CR | LF | 

Die **LRC-Prüfsumme** bildet sich so:

| : | 0C | 04 | 0000 0001 | ? | \r | \n |  | 
| --- | --- | --- | --------- | --- | --- | --- | --- |
|  | 30H 43H | 30H 34H | 30H * 7 + 31H | |  |  | ->Summe = 258 Hex. = 600 Dez. | 

600 - 256 * 2 = 88 Dez.
-88 Dez. + 256 Dez. = A8 Hex = LRC-Prüfsumme

### 3.7) - Response µC -> PC -

| : | 0C | 04 | 02 | **1752*** | F8 | \r | \n |  
| --- | --- | --- | --------- | --- | --- | --- | --- |  
| 3a | Korrenns Adresse | Function Code | Anzahl der Byte | **Temperatur** | LRC-Prüfsumme | CR | LF | 

-> Um den Wert einer Temperatur (zB 23.32°C) darstellen zu können, kann man verschiedene Varianten verwenden. 

##### Festkommadarstellung 

Vorteil: Faktoren im Binär-Bereich, besseres Ausnutzen der Bits 
23,32°C * 256 = ~5970 Dez. (**1752 Hex.**) -> 5979 : 256 = 23,32°C 

##### Scale Factor 

zB Scale Factor = *10*
23,3°C * *10* = 233 Dez. (00E9 Hex.)
-> Faktoren im Dezimalbereich
Vorteil: Man kann als Mnesch besser damit agieren

___
