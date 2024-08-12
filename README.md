# SmartWasserzähler
Dieses Repository befasst sich mit einem Raspberry Pi Projekt, bei dem die Werte eines Wasserzählers ausgelesen und graphisch auf einer localen Website dargestellt werden. 

>[!NOTE]
> Das Projekt ist (noch) unvollständig und nicht funktionsfähig

## Aufbau:
 ### Auslesen des Zählers:
 
 Als Grundstein des Projektes wird ein Programm benötigt, welches den aktuellen Wert des Wasserzählers auslesen kann.
 
 #### Reed Sensor 
 In der Mechanik eines Wasserzählers ist ein Magnet verbaut, welcher sich mit den Zahnrädern mit dreht. Mit Hilfe eines Reed Sensor oder eines Hall-Sensors kann man die Magnetischen impulse Messen und mitzählen, wie viel Wasser durch den Sensor läuft. Sollte man das System allerdings deaktivieren oder es fällt während eines Stromausfalls aus, so stimmt der Zählstand nicht mehr überein und er muss manuell korigiert werden, da nicht der direkte Zählerstand ausgelesen werden kann. 

 #### Kamera
 Mit Hilfe einer Kamera können die Ziffern und Zeiger des Wasserzählers aufgenommen und ausgelesen werden. Das Programm muss somit nicht dauerhaft aktiv sein, sondern kann einfach den aktuellen Zählerstand auslesen. 

Obwohl die zweite Methode zugegebenermaßen deutlich komplizierter und aufwändiger ist als es sein müsste entschied ich mich dazu eine Kamera zu nutzen. Dies lag zum einen daran, dass ich die nötigen Materialien bei mir hatte und dass die Programierung deutlich spannender wirkte. Eventuell baue ich irgendwann eine weitere Version mit einem ESP32 und einem Hall-Sensor

### Datenbank: 

Das Kameraprogramm erfasst den Stand des Wasserzälers alle 2-5 Minuten. Dieser wird dann, zuammen mit dem aktuellen Datum und Uhrzeit in einer Datenbank abgespeichert. Um die Ungenauigkeiten in den Werten einfacher zu finden wird zudem die Differenz zum vorherigen Wert abgespeichert. 

### Website: 
Der Raspberry Pi soll eine Website hosten, welche den Wasserverbrauch in einem Graphen darstellt. Zudem sollen die Ausschnitte der Zeiger und des Zahlen zu sehen sein. 
In einem Einstellungs Menü sollen zudem die Bildbereiche ausgewählt werden, welche von dem Kameraprogramm ausgelesen werden. 

## Interface: 
In den Einstellungen auf der Website ist das Gesamte Bild der Kamera zu sehen. Durch das Drücken von Tasten lassen sich die zu scanneden Bereiche auswählen, welche die Ziffern anzeigen. Für die tatsächlichen Ziffern sind diese Bereiche Rechtecke, für die Zeiger sind es Kreise.
Speichert man die Einstellungen, werden die jeweiligen Koordinaten in einer .json Datei im Backend abgespeichert. 

## Kameraprogramm:
Auf dem Raspberry Pi läuft ein Python Programm, welches für die Dokumentierung der Daten zuständig ist. Es nutzt die Koordinaten aus der .json Datei und extrahiert die Ziffern mit folgenden Methoden:

### Zeiger auslesen:
Um die Postition des Zeigers innerhalb des ausgewählten Kreises zu ermitteln, wird der Mittelpunkt des Kreises genutz. Dieser liegt, sofern der Kreis richtig plaziert wurde, auf dem Mittelpunkt des Zeigers. Von diesem Mittelpunkt wird der Farbwert entnommen. Danach wird in einem Festgelegten Radius um den Mittelpunkt geguckt, an welcher Stelle der Farbwert am weitesten mit dem des Zeigers übereinstimmt. Dann wird eine Linie zwischen Mittelpunkt und diesem Punkt eingezeichnet und der Winkel dieser Linie zu einer Senkrechten berechnet, aus dem schließlich der Zeigerstand berechnet werden kann. 

### Ziffern auslesen: 
>[!NOTE]
> Dieser Teil bereitet momentan die meisten Probleme. Wenn diese Ziffern falsch ausgelesen werden, ist der gesamte Datensatz nicht verwendbar. 

#### pytesseract:


#### mnist Model:
