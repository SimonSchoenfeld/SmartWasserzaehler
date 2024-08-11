# SmartWasserzähler
Dieses Repository befasst sich mit einem Raspberry Pi Projekt, bei dem die Werte eines Wasserzählers ausgelesen und graphisch auf einer localen Website dargestellt werden. 

>![NOTE]
> Das Projekt ist (noch) unvollständig und nicht funktionsfähig

 ## Auslesen des Zählers:
 
 Als Grundstein des Projektes wird ein Programm benötigt, welches den aktuellen Wert des Wasserzählers auslesen kann.
 
 ### Reed Sensor 
 In der Mechanik eines Wasserzählers ist ein Magnet verbaut, welcher sich mit den Zahnrädern mit dreht. Mit Hilfe eines Reed Sensor oder eines Hall-Sensors kann man die Magnetischen impulse Messen und mitzählen, wie viel Wasser durch den Sensor läuft. Sollte man das System allerdings deaktivieren oder es fällt während eines Stromausfalls aus, so stimmt der Zählstand nicht mehr überein und er muss manuell korigiert werden, da nicht der direkte Zählerstand ausgelesen werden kann. 

 ### Kamera
 Mit Hilfe einer Kamera können die Ziffern und Zeiger des Wasserzählers aufgenommen und ausgelesen werden. Das Programm muss somit nicht dauerhaft aktiv sein, sondern kann einfach den aktuellen Zählerstand auslesen. 

Obwohl die zweite Methode zugegebenermaßen deutlich komplizierter und aufwändiger ist als es sein müsste entschied ich mich dazu eine Kamera zu nutzen. Dies lag zum einen daran, dass ich die nötigen Materialien bei mir hatte und dass die Programierung deutlich spannender wirkte. Eventuell baue ich irgendwann eine weitere Version mit einem ESP32 und einem Hall-Sensor

## Datenbank: 

Das Kameraprogramm erfasst den Stand des Wasserzälers alle 2-5 Minuten. Dieser wird dann, zuammen mit dem aktuellen Datum und Uhrzeit in einer Datenbank abgespeichert. Um die Ungenauigkeiten in den Werten einfacher zu finden wird zudem die Differenz zum vorherigen Wert abgespeichert. 

## Website: 
Der Raspberry Pi soll eine Website hosten, welche den Wasserverbrauch in einem Graphen darstellt. Zudem sollen die Ausschnitte der Zeiger und des Zahlen zu sehen sein. 
In einem Einstellungs Menü sollen zudem die Bildbereiche ausgewählt werden, welche von dem Kameraprogramm ausgelesen werden. 

