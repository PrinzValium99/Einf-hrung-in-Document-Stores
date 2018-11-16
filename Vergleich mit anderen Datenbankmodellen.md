# Verlgeich mit anderen Datenbankmodellen


Neben dokumentenorientierten Datenbanken gibt es noch weitere Datenbankmodelle. Der Unterschied der Datenbankmodellte zueinander besteht im wesentlichen darin auf welche Art und Weise der Datenbestand gespeicher und auf ihn zugegriffen wird. **Der Unterschied der Datenbankmodelle soll anhand des  Beispieles Dozenten und Vorlesungen näher erläutert werden.**

## realationale Datenbanken

Relationale Datenbanken gehören zu den am weitesten verbreiteten Datenbankmodellen. Dargestellt werden sie häufig im Entity-Relationship-Modell nach Chen. Entwickelt wurde das relationale Datenbankmodell von Edgar F. Codd in den 1960er/70er Jahren. Oracle veröffentlichte einige Jahre später die erste funktioniertende Datenbank nach diesem Modell. Die Daten werden in 2-dimensionelle Tabellen gespeichert und über SQL abgefragt. Über einen Schlüssel (Primärschlüssel) und einem Fremdschlüssel (foreign Key) werden die Tabellen miteinander verknüpft. Ein Datensazt (Record) befindet sich immer innerhalb einer Tabellenzeile (Tupel). Des Weiteren beinhaltet jede Zeile eine Reihen von Merkmalen (Attributen). Diese stellen die Tabellenspalten dar. Anhand des Beispieles Dozenten und Vorlesungen soll eine relationale Datenbank visualisiert werden. Die tutor_id stellt in diesem Beispiel den foreign Key dar.

### Tutor

| id | firstname	| lastname 	|
|----|----------	|------------	|
| 1  | Hans   	| Maier		|
| 2  | Peter	 	| Müller		|

### Lecture

| id | tutor_id	| lecture				|
|----|----------	|-------------------|
| 1  | 1  		| Quantencomputer  	|
| 2  | 1 			| Mathematik 1  		|
| 1  | 2  		| Web Development  	|
| 2  | 2 			| Softwaretechnik 	|



-
http://www.info-wsf.de/index.php/Datenbankmodelle <br>
https://blog.adacor.com/big-data-sql-nosql-richtig-einordnen_4308.html

-




Die Themen „Performance“ und „fehlende Gewährleistung der Datenintegrität“ bringen bei komplexen Relationsmodellen und vielen Daten einige Nachteile mit. Die Performance-Probleme resultieren aus der Mengenlehre. So müssen die Tabellen zueinander geführt werden, um sie auszuwerten. Das passiert mit jeder Verknüpfung in einer Menge, die dann wieder mit der neuen Verknüpfung zusammengeführt wird. In der daraus entstehenden Endmenge werden die Ergebnisse gefiltert. Dieses Vorgehen führt bei vielen Tabellen zu hoher Komplexität und großen temporären Speicheraktionen. Die Rechenvorgänge dauern deshalb entsprechend lange und verbrauchen viel Speicher. Bei der Datenintegrität hingegen gibt es potenziell falsche Ergebnisse, wenn man die Integrität nicht „programmiert“ hat. Diese Nachteile können nur teilweise über das System und die genutzte Fremdschlüsselstruktur abgefangen werden und sitzen zum Teil in der Applikation.