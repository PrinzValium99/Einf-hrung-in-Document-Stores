# 4. Verlgeich mit anderen Datenbankmodellen 

Neben dokumentenorientierten Datenbanken gibt es noch weitere Datenbankmodelle. Der Unterschied der Datenbankmodelle zueinander besteht im wesentlichen darin auf welche Art und Weise der Datenbestand gespeichert und auf ihn zugegriffen wird. Die Datenbankmodelle relationale Datenbanken und objektorientierte Datenbanken werden kurz vorgestellt. Zudem wird der Unterschied der Datenbankmodelle anhand des Beispieles Dozenten und Vorlesungen dargestellt werden.

## 4.1 Relationale Datenbanken

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


Eine Abfrage die vereinfacht wie folgt lautet 'Zeige mir alle Vorlesungen des Dozenten Maier' würde zunächst den Datensatz aus der Tabelle 'tutors' mit dem Nachnamen Maier ermittelt. Anschließend werden alle Datensätze aus der Tabelle 'lecture' , die der tutor_id '1' ensprechen zugeordnet.

| firstname  	| lastname  	| lecture          | 
|------------	|------------	|------------------|
| Hans			| Maier 		| Quantencomputer  |   
| Hans 		| Maier   	| Mathematik 1     | 


Trotz ihrer übersichtlichen Darstellung und Beliebtheit bringen relationale Datenbanken auch einige Nachteile mit. Zum Einen sind dies Permormance-Prombleme. Diese resulieren daraus, dass Tabellen zueinander geführt werden müssen, um diese auswerten können. Jedes Segment wird mit einer anderen Menge verknüpft und erst aus der Endmenge werden die Ergebnisse gefiltert. Vor allem bei einer Vielzahl von Tabellen führt das zu großen temporären Speicheraktionen, weshalb die Rechenvorgänge viel Zeit in Anspruch nehmen. Einen weiterer Nachteil ist, dass für die Manipulation der Abfrageergensise die zur Verfügung stehende Programmiersprache von rationalen Datenbanken nicht ausrecht und meist eine Schnittstelle zu weiteren Programmiersprachen nötig ist. [2]


## 4.2 Objektorientierte Datenbanken

Objektorientierte Datenbanken ist eine relative neue Entwicklung. Die Daten werden innerhalb von Objekten verwaltet. Dies geschieht im Sinne der Objektorientierung. Objekte können wie auch in der OOP Unterobjekte enthalten. Eine getrennte Speicherung von Methoden und Attributen findet innerhalb der Objekte nicht statt, wodurch benötigte Operatoren sofort in die Datensätze eingegliedert werden können. [2] In der Praxis sind objektorientierte Datenbanken wenig verbreitet, wodurch die Implementierung durch fehlende eigene Schnittstellen und Zwischen-Layer schwierig gestaltet wird. 

Betrachtet man nun das Dozenten/Vorlesungen Beispiel könnten ein Dozentenobjekt mit dem Namen oTutor wie folgt aufgebaut sein:

`[firstname]'Hans'`<br>
`[lastname] 'Maier'`<br>
`[lecutre] 'Quantencomputer'`<br>
`[lecutre] 'Mathematik 1'`

Durch im Objekt oTutor hinterlegte Methoden wie z.B. getName, getFirstLecture können die Daten abgefragt werden.

`oTutor->getName() liefert: 'Hans Maier'`<br>
`oTutor->getFirstLecture() liefert: 'Quantencomputer'`

Ein Nachteil der objektorientierten Datenbanken ist die geringe Verbreitung, weshalb die Untestüzung von Schnittstellen und Tools noch recht gering ist. Bei einigen Anfragen haben relationale Datenbanken einen Vorteil gegenüber den objektorientierten. Durch erhöhte Komplexität kann es zu Leistungsproblemen fürhren. Dies lässt sich auf die Zugriffspfade die durch unterschiedliche Pfadarten wie Assoziationen und Vererbung bei den Objekten entstehen zurückführen.

## 4.3 Dokuemtenorientierte Datenbanken

Bei Document Stores werden die Daten nicht wie bei relationalen Datenbanken in Spalten und Tabellen abgespeichert sondern, wie bereits in vorherigen Abschnitten beschrieben, in Dokumenten. Ein Dokument stellt eine Ansammlung von Feldern und Werten dar. Jeder Eintrag wird in einem eigenen Dokument gespeichert und über eine eindeutige ID in der Datenbank indentifiziert. Die Daten werden ohne eine vorgebene Struktur für das jeweilige Dokument gespeichert, anders als über eine Tabellenstruktur in den relationalen Datenbanken oder einer festgelegeten Struktur für einen bestimmten Objekttyp in den objektorientierten Datenbanken. [6]

Anhand des Dozenten/Vorlesungen Beispiels können zwei Dozenten-Dokumente unterschiedliche Strukturen aufweisen (Json-Format):

```
{ 
“name“ : “Hans Maier“, 
“university“ : “TH Brandenburg“, 
“lectures“ : [“Quantencomputer“, “Mathematik 1“]
}
```
```
{
“firstname“ : “Peter“,
“lastname“ : “Müller“,
“lectures“ : [“Web Development“, "Softwatechnik"]
}
```

Ein Nachteil von dokuemtenorientierten Datenbanken ist, dass sie für komplexe Datenstrukturen mit hoher Beziehungstiefe eher ungeeinget sind. Müssen mit den in der Datenbank enthaltenen Dokumenten Operatationen programmiert werden, so muss zunächst eine Struktur festgelegt werden. Häufig wird in diesem Zuge eine übergeordnete Strukturfestlegung vorgenommen, um den Programmieraufwand zu verringern. Dies führt dazu, dass die Formfreiheit nur noch eingeschränkt gilt. Funktionaliäten die bei relationalen oder objektorientierten Datenbanken standardmäßig zur Verfügung stehen müssen bei dokumentorientierten Datenbanken individuell programmiert werden.[3]


<hr>
[1] http://www.info-wsf.de/index.php/Datenbankmodelle <br>
[2] https://blog.adacor.com/big-data-sql-nosql-richtig-einordnen_4308.html <br> 
[3] https://blog.secu-ring.de/software/unterschiede-der-datenbankmodelle-relationale-objektorientierte-und-doukumentenbasierte-datenbank/ <br>
[5] https://www.eu-datenbank.de/fachartikel/vor-und-nachteile-von-objektdatenbanken/ <br>
[6] NoSQL Einfuhrung - CouchDB, Mon - Oliver Kurowski
<hr>
[< Datenmodell](05_Datenmodell.md)		|   [Anwendung von Document Stores >](07_Anwendung-von-DocumentStores.md)
