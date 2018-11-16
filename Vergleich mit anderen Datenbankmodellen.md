# Verlgeich mit anderen Datenbankmodellen


Neben dokumentenorientierten Datenbanken gibt es noch weitere Datenbankmodelle. Der Unterschied der Datenbankmodelle zueinander besteht im wesentlichen darin auf welche Art und Weise der Datenbestand gespeichert und auf ihn zugegriffen wird. Der Unterschied der Datenbankmodelle soll anhand des  Beispieles Dozenten und Vorlesungen näher erläutert werden.

## Relationale Datenbanken

Relationale Datenbanken gehören zu den am weitesten verbreiteten Datenbankmodellen. Dargestellt werden sie häufig im Entity-Relationship-Modell nach Chen. Entwickelt wurde das relationale Datenbankmodell von Edgar F. Codd in den 1960er/70er Jahren. Oracle veröffentlichte einige Jahre später die erste funktioniertende Datenbank nach diesem Modell. [1] Die Daten werden in 2-dimensionelle Tabellen gespeichert und über SQL abgefragt. Über einen Schlüssel (Primärschlüssel) und einem Fremdschlüssel (foreign Key) werden die Tabellen miteinander verknüpft. Ein Datensazt (Record) befindet sich immer innerhalb einer Tabellenzeile (Tupel). Des Weiteren beinhaltet jede Zeile eine Reihen von Merkmalen (Attributen). Diese stellen die Tabellenspalten dar. Anhand des Beispieles Dozenten und Vorlesungen soll eine relationale Datenbank visualisiert werden. Die tutor_id stellt in diesem Beispiel den foreign Key dar. [2]

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

Trotz ihrer übersichtlichen Darstellung und Beliebtheit bringen relationale Datenbanken auch einige Nachteile mit. Zum Einen sind dies Permormance-Prombleme. Diese resulieren daraus, dass Tabellen zueinander geführt werden müssen, um diese auswerten können. Jede Menge wird mit einer anderen Menge verknüpft und erst aus der Endmenge werden die Ergebnisse gefiltert. Vor allem bei einer Vielzahl von Tabellen führt das zu großen temporären Speicheraktionen, weshalb die Rechenvorgänge viel Zeit in Anspruch nehmen. Einen weiterer Nachteil stellt die Datenintegriät dar. Diese liefert teilweise unzulängliche Ergebnisse wenn die Interität falsch programmiert wurde.[2]

<hr>
ab hier nur reinkopiert

Nachteile des relationalen Datenbankmodells:
1. Die Datenbestände sind segmentiert und jedes Segment kann wieder weitere Segmente in sich tragen (jedes Buch kann in mehreren Verlagen verlegt worden sein, von denen jeder mehrere Niederlassungen hat, …). Mit Erhöhung der Anzahl der abgefragten Segmente verringert sich die Performanz der Abfrageverarbeitung.
2. Für die Manipulation der Abfrageergebnisse ist in den allermeisten Fällen eine Schnittstelle zu einer weiteren Programmiersprache notwendig, da die ggf. in der relationalen Datenbank zur Verfügung stehende dafür wenig Möglichkeiten bietet.


## Objektorientierte Datenbanken


Das objektorientierte Datenbankmodell ist eine relativ neue Entwicklung. Der Inhalt der Records sind Objekte im Sinne der OOP. Diese Objekte können auch Unterobjekte enthalten (siehe Vererbung in der OOP). Innerhalb der Objekte findet keine getrennte Speicherung von Methoden und Attributen statt. Dies bietet den Vorteil, dass eventuell benötigte Operatoren sofort in die Datensätze mit eingegliedert werden. Außerdem wird der Datenbank so mehr Semantik (logische Folge von Informationen) verliehen.

Dieses Modell konnte sich jedoch trotz guter Speicherzugriffe bis jetzt noch nicht am Markt etablieren.

Zuvor: Um das DBMS in diesem Fall als Objektdatenbankmanagementsystem zu kennzeichnen, wird ihm ein ‘O’ vorangestellt (kurz: ODBMS).
Die Struktur der Datenablage folgt den Richtlinien der Objektorientierung. Das heisst, die zu einem Objekt gehörenden Daten werden im Objekt selbst abgelegt. Die interne Organisation und Verwaltung der Daten wird komplett vom ODBMS übernommen. Für die Abfrage und Manipulation der Daten stellt das ODBMS geeignete Objektsprachen bereit.


<hr>
[1] http://www.info-wsf.de/index.php/Datenbankmodelle <br>
[2] https://blog.adacor.com/big-data-sql-nosql-richtig-einordnen_4308.html
<hr>

