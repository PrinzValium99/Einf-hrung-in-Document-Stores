
## 6.2 MongoDB ---> LOGO FEHLT NOCH

### 6.2.1 Beschreibung


MongoDB gehört zu den beliebtesten NoSQL-Vertretern. Der Name 'Mongo' wurde abgeleitet von 'humongous' (gigantisch). MongoDB ist eine skalierbare, hochperformante, schemafreie und dokumentenorientierte Open-Source-Datenbank, die durch ihre Features im Vergleich zu anderen NoSQL-Datenbanken besticht. Zudem stellt sie das Bindeglied zwischen klassischen relationalen Datenbanken und Key/Value-Stores her. Dokumente werden im im BSON-Format verwaltet. Eine integrierte Query Language ermöglicht einfache Abfragen, Replikationen und Sharding (Replikationen und Sharding ermöglicht die Verwendung vieler nicht so leistungsstarker Rechner). Zudem kann eine Vielzahl bekannter Programmiersprachen angebunden werden. Umfangreiche Abfragemöglichkeiten mit guter Skalierbarkeit und Performance gekoppelt schaffen eine Konkurrenz zu den klassichen RDMBS (Relational Database Management System). MongoDB kann in virtuellen Umgebungen, bei Cloud Computing und in den gängigen Betriebsystemen Linux, Mac OS und Windows eingesezt werden. Das Datenbanksystem verfügt zudem über einen kommerziellen Support [1,2].

MongoDB zeichnet sich vor allem durch ein flexibles Datenbank Schema, welches dynamsich angepasst werden kann, aus. Die Daten werden in JSON-ähnlichen Dokumenten gespeichert, wodurch die Felder in den einzelnen Dokumenten variieren und die Datenstrukturen sich über die Dauer verändern. Durch Ad-hoc-Abfrgen, Indizierung und Echtzeitaggregation wird der Zugriff und die Analyse der Daten vereinfacht [3]. 
Ein großes Manko von MongoDB stellt die Sicherheit beim Zugriff dar, da dieser nur mit Einstellung der IP-Tables erfolgt. Aus diesem Grund sind Tranksaktionen und Query-Operationen im Gegensatz zu einem RDBMS nicht im vollen Umfang möglich [1]. 


### 6.2.2 Datenbankaufbau

MongoDB hält die Dokumente temporär im Speicher und übermittelt sie im BSON-Format an den Client Driver. Der Client Driver muss dazu mit dem BSON-Format umgehen können. Anders als bei relationalen Datenbanken gliedert sich die Struktur der Daten in MongoDB in beliebig viele Collections, in denen sich wiederum beliebig viele Dokumente befinden. Ein Beispiel hierfür sieht wie folgt aus:

| Datenbankname: lectures  				|
|-------------------------------------------------------|
| Collection tutors   |
| ```{_id:1, name:"Maier"} {_id:2, name:"Müller"} ``` |
| Colection lectures 						 | 
| ```{_id:1; turor_id:1,  lecture:"Quantencomputer"} {_id:1; turor_id:1,  lecture:"Mathematik 1"}``` | 



#### 6.2.2.1 Datenbank
Mehrere Datenbanken nebeneinander sind beim MongoDB Server zulässig. Jeder dieser Datenbanken wird einzeln behandelt und kann spezifisch gestaltet werden. Der Bestandteil einer Datenbank sind Datafiles in dem die Dokumente im BSON-Format vorliegen (Datenbankname.0, Datenbankname.1") und Namespace-Files ("Datenbankname.ns"). Eine Liste von Collections und Metadaten sind innerhalb des Namespace-Files zu finden [2].

#### 6.2.2.2 Collection
Collections lassen sich mit den Tabellen eines RDBMS vergleichen. Jedoch werden sie anders als die Tabellen erst erstellt sobald sie benötigt werden. Erst wenn ein Dokument in eine neue Collection eingefügt werden soll, wird diese erstellt. Eine Collection sollte mit einem einzelnen Buchstaben oder einem Unterstich beginngen. Das "$"-Zeichen sowie "system." sind bereits als Präfix für die Abfrageoperatoren sowie als Namespace-Präfix für die Metainformationen der jeweiligen Datenbank reserviert und dürfen deshalb nicht in der Benamung von Collections verwendet werden [2].  

Eine spezielle Form der Collections ist die **Capped Collection**, da diese in ihrer Größe beschränkt werden kann. Hierbei wird nach dem First-In-First-Out-Prinzip gearbeitet. Der Zeitpunkt indem erstmalig etwas zum Dokument hinzugefügt wurde bestimmt das Alter. Wird die vordefinierte Größe einer Capped-Collection erreicht, wird sobald etwas neues eingefügt wird das älteste Dokument automatisch gelöscht. Capped Collection bringen zwei Beschränkungen mit sich:

* nur bei unveränderter Größe können bestehende Dokumente verändert werden 
* bestehende Dokumente können nicht gelöscht werden

Aufgrund der hohen Performance beim Einfügen neuer Dokuemnte eignen sich Capped Collection vor allem für Anwendungszwecke mit einer hohen Insert-Rate  [1].

#### 6.2.2.3 Dokumente

Die einzelnen Dokumente stellen das pendant zu den Zeilen (Row) der relationalen Datenbanken dar. Die Anzahl an Feldern (Key) mit einem Wert (Value) ist beliebig. Anders als bei Tupeln gibt es keine vordefinierte Reihenfolge mit fest definierten Datentypen, sondern es werden assoziative Arrays verwendet. Wie auch in anderen Sprachen kann man innerhalb von MongoDB Objekte in Array und Objekte verschachteln. Die Key in diesen Arrays sind Zeichenketten. Wie auch für die Collections gibt es Konventionen für die Bennenung. So darf weder ein "." enthalten sein, nohc das Zeichen "$" am Anfang eines Schlüssels stehen. Abgespeichert und übertragen werden Dokumente im BSON-Format.

---
hier weiter

### 7.1.3 Speicherung der Daten

In CouchDB werden Dokumente in Form von JSON-Datenstrukturen abgelegt. Ähnlich wie bei anderen dokumentorientierten Datenbanken geschieht dies schemafrei. Allerdings gibt das JSON Format eine gewisse Struktur durch die Syntax vor. Die Dokumente werden in Unterdatenbanken gespeichert und durch Dokument-IDs bzw. Revisions-IDs indexiert. Die eindeutige Dokument-ID legt der Nutzer selbst fest, die Revisions-ID wird wiederum von CouchDB verwaltet. Sie gibt an, in welcher Version ein Dokument vorhanden ist. Wird eine Instanz aktualisiert, dann lassen sich die Änderungen später anhand der Revisions-ID nachvollziehen. Die einzelnen Dokumente stellen das pendant zu den Tupeln der relationalen Datenbanken dar. Jedes JSON-Objekt wird durch eine Liste von Eigenschaften aufgebaut, wobei jede Eigenschaft durch ein Key/Value-Paar beschrieben wird. Jeder Value kann zusätzlich eine neue Eigenschaft darstellen. Dieses System ermöglicht die beliebige Verschachtelung von Key/Value-Paaren und Listen. [1, 3]

In JSON werden die folgenden Basistypen definiert: Objekte, Arrays, Zeichenketten, Zahlen, Boolesche Werte und null. Sowohl zum Datenaustausch als auch zur Speicherung wird das kompakte JSON-Datenformat genutzt. Damit entfällt die Umwandlung in andere Formate zur Speicherung in einer Datenbank, was sich durch erhöhte Performance bemerkbar machen kann. [1, 5]

In CouchDB findet außerdem eine Unterscheidung diverser Dokumentarten statt. Die folgenden sind von besonderer Bedeutung:

- Datendokumente

- Virtuelle (nicht persistent) Dokumente

- Design Dokumente


**Datendokumente**

Datendokumente bilden eine geschlossene Einheit von Informationen. Als zusätzliche Metadaten werden die oben angesprochenen Dokument-IDs und Revisions-IDs gespeichert. Wie bereits erwähnt wird die Dokument-ID durch den Benutzer vergeben. Es wird empfohlen dafür eine Universally Unique Identifier (UUID) zu verwenden, aber auch benutzerdefinierte IDs funktionieren. Diese UUIDs kann CouchDB auch mit Hilfe eines GET-Request selbst generieren. Im folgenden Beispiel ist ein Datendokument mit den Keys   `"_id"` und `"_rev"` für die Dokument-ID und Revisions-ID zu sehen. 

{

```
	"_id"       :	"00a271787f89c0ef2e10e88a0c00048b", 
	"_rev"      :	"1-60e25d93dc12884676d037400a6fa189", 
	"item"      :	"Banane", 
	"preise"    : 
		{
			"Markt"   : 0.10, 
			"Lebensmitteldiscounter" : 0.08, 
			"Bauern"  : 0.25 
		} 
```

}



**Virtuelle Dokumente**

Alle Informationen in einem Dokument zu verwalten, entspricht dem Paradigma und bietet zu den Vorteilen eines dokumentenorientierten Persistierens einige Nachteile in der Umsetzung CouchDB (z.B. Konfliktwahrscheinlichkeit). Daher bietet es sich an, in manchen Fällen Dokumente in mehrere logische Dokument-Typen zu zerteilen. Als gängiges Beispiel seien hier Blogposts und die zugehörigen Kommentare erwähnt. In solchen Fällen möchte man dennoch mittels einer Anfrage die geteilten Informationen zusammen erhalten. Hierzu werden virtuelle Dokumente verwendet, welche Views darstellen. In ihrer nicht-persistierten Form stellen diese Views virtuelle Dokumente dar und können als Ad-Hoc-Abfragen bezeichnet werden. Im Web-Interface [Futon](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.Futon) von CouchDB können diese virtuellen Views unter dem Punkt „Temporary view“ erstellt werden.



**Design Dokumente**

Eine letzte Dokumentenart stellen die Design-Dokumente dar. Die Besonderheit, die Design-Dokumente von Daten-Dokumenten unterscheidet, ist, dass sie Quellcode enthalten, für dessen Ausführung der in CouchDB eingebaute JavaScript-Query-Server notwendig ist. Design-Dokumente können als einzelne Oberflächen von Webanwendungen verstanden werden. CouchDB speichert und behandelt Design-Dokumente wie Daten-Dokumente. Beispielsweise werden diese im Rahmen einer Replikation ebenfalls auf die Zieldatenbank kopiert. Eine Restriktion ist dennoch einzuhalten: die ID eines Design-Dokuments muss mit dem Präfix „_design/“ beginnen. Einzelne Komponenten eines Design-Dokuments können sein :



1. View-Funktionen,
2. Show-Funktionen,
3. List-Funktionen,
4. Update-Funktionen und
5. Validierungs-Funktionen. [3]

### 7.1.4 Kommunikation

Die Kommunikation mit CouchDB wird durch HTTP-Anfragen realisiert, so dass kein eigenes Kommunikationsprotokoll definiert werden muss. Die Verwendung von HTTP erleichtert zudem die Anbindung an Web-Anwendungen enorm, des Weiteren ist das Protokoll ein allgemein bekannter Standard und leicht zu verwenden. Da es sich bei HTTP um ein zustandsloses Protokoll handelt, müssen alle relevanten Transaktionsdaten in einer Anfrage übergeben werden. Man spricht in diesem Zusammenhang von [REST](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.REST) (Representational State Transfer). Um mit CouchDB zu kommunizieren, bietet sich u.a. das Kommandozeilenwerkzeug [cURL](http://curl.haxx.se/) an. Im Folgenden werden einige Beispiele der Kommunikation mit CouchDB aufgelistet. Die Eingabe wird mit *curl* in einer Kommandozeilenumgebung durchgeführt, die Ausgabe wird ebenfalls auf der Kommandozeile dargestellt. Die Ausgabe erfolgt in Form eines [JSON](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.JSON) -Objekts. [3]

### 7.1.5 Views

Um Daten innerhalb von Dokumenten abzufragen oder zu aggregieren, existieren in Apache CouchDB Views. Diese sind MapReduce-Funktionen in JavaScript-Programmiersprache. Neben dem erwähnten Einsatzbereich können View-Funktionen zudem verwendet werden, um

- Dokumente zu filtern,
- Informationen aus Dokumenten zu extrahieren und in einer spezifischen Form darzustellen,
- Nach Informationen oder Strukturen zu suchen oder
- Berechnungen durchzuführen.

Es sei explizit darauf hingewiesen, dass View-Funktionen nicht vom Anwender, sondern von Apache CouchDB ausgeführt werden. Fragt man eine View ab, wendet das DBS die Map-Funktion auf alle Dokumente an. „You query your view to retrieve the view result.“ Das Ergebnis der Map-Funktion wird als View-Ergebnismenge bzw. View-Rows bezeichnet. Die Einträge in der Ergebnismenge sind Schlüssel/Werte-Paare. Wird die Map-Funktion auf ein Dokument angewendet, können hieraus beliebig viele Einträge in der Ergebnismenge resultieren. Im Folgenden ist eine Map-Funktion dargestellt.

function(doc) {

```
	if (doc.item && doc.price) {
		emit([ doc.item, doc.price ], 1);
	}
```

}

Der Map-Funktion wird ein Parameter („doc“) übergeben, die ein Dokument darstellt. In der if-Anweisung wird überprüft, ob das Dokument bestimmte Schlüssel hat. Dies ist erforderlich, da die Map-Funktion auf alle Dokumente angewendet wird und nur Dokumente mit bestimmten Eigenschaften von Interesse sind. In diesem Beispiel sind es Dokumente, die die Eigenschaft „item“ und „price“ haben. Hiernach wird mit der emit-Funktion ein Schlüssel/Werte-Paar in die Ergebnismenge eingetragen. Die emit-Funktion kann innerhalb der Map-Funktion auch mehrere Male aufgerufen werden, wobei mehrere Einträge pro Dokument möglich sind. Von Bedeutung ist zudem, dass die Ergebnismenge nach dem Schlüssel sortiert zurückgegeben wird. In dem Beispiel wird eine Kombination aus der Eigenschaft „item“ und der Eigenschaft „price“ in einem Array als Schlüssel zurückgegeben, womit eine Sortierung der Ergebnismenge erst nach der Eigenschaft „item“ und dann nach der Eigenschaft „price“ vorgenommen wird. Um die Reduce-Funktion innerhalb einer View zu verstehen, muss bekannt sein, dass die Ergebnismenge der Map-Funktion als ein B+-Baum verwalten wird. Eine einfache Reduce-Funktion sieht wie folgt aus:

function(keys, values, rereduce) {

```
   return sum(values);
```

}

Die Reduce-Funktion wird, falls keine Filterung der Abfrage vorgenommen wird, auf jeden Knoten im B+-Baum angewendet. Im ersten Parameter befinden sich die Schlüssel und im zweiten die Werte, die in einem Knoten gespeichert sind. Das Ergebnis wird zwischengespeichert. Der dritte Parameter gibt an, ob ein Blätter-Knoten oder ein innerer Knoten bearbeitet wird. Der Wert des dritten Parameters ist „false“, wenn es sich um einen Blätter-Knoten handelt, wobei die anderen beiden Parameter wie bereits erwähnt belegt sind. Der Wert des dritten Parameters ist „true“, wenn es sich um einen inneren Knoten bei der Ausführung handelt. In diesem Fall ist der erste Parameter „null“ und der zweite Parameter ein Array aus Zwischenergebnissen der entsprechenden Kinder-Knoten. Erinnert man sich daran, dass die Nutzdaten in einem B+-Baum nur in den Blättern gespeichert werden, so versteht man in manchen Fällen die Notwendigkeit, eine Unterscheidung vorzunehmen. Während bei den Blättern Operationen bzgl. einzelner Einträge in der Ergebnismenge der Map-Funktion vorgenommen werden können, können deren Zwischenergebnisse bei der Bearbeitung der inneren Knoten weiter verwendet werden. [3]

### 7.1.6 Replikation

Die [Replikation](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.Replikation), d.h. die Übertragung der Daten auf andere Knoten, ist bei Apache CouchDB ein inkrementeller Prozess per Push und Pull. Wie die Client-Server Kommunikationsvorgänge wird auch die Replikation über HTTP-Requests abgewickelt. Die Daten werden dokumentweise auf Server übertragen, die sich an geografisch stark unterschiedlichen Orten befinden, um geringe Latenzen bieten zu können („move data more closely to clients“). Über „Continuous Replication“ kann relativ komfortabel eine unidirektionale Replikation, welche als Backup dienen kann, faktisch aber keines darstellt, eingerichtet werden, diese kann zudem zu einer bidirektionalen Replikation erweitert werden. Die Backupserver sind hierbei nicht aktiv für Abfragen eingebunden. Um die bidirektionale Replikationen im Rahmen von Load-Balancing einsetzen zu können, müssen zusätzliche Frameworks wie „CouchDB Lounge“ verwendet werden. Für Partitionierung (bzw. Sharding) wird ebenfalls einer der genannten Forks von Apache CouchDB benötigt, um im Kontext von verteilter Einrichtung besser zu skalieren. Die dokumentweise Übertragung dient dazu, um bei Unterbrechung des Kommunikationsprozesses die Übertragung dort fortzusetzen, wo sie abgebrochen worden ist. Damit ist ein Neustart der Replikation nicht erforderlich und das System wird robuster gegenüber Fehlern. 
Über [Futon](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.Futon) kann ein entsprechender Replikationsprozess couch-entsprechend bequem initialisiert werden.

Bei der Entwicklung des Replikationsverfahrens ging man davon aus, ein CouchDB-Knoten sei im Normalfall nicht erreichbar("offline by default"). Daher wurde bei CouchDB der Fokus auf eine hohe Ausfalltoleranz (siehe [CAP-Theorem](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.CAP)) gelegt.
Ein wesentliches Augenmerk bei der Entwicklung von CouchDB lag auf dem Aspekt der Verfügbarkeit. Bei Replikationsvorgängen bleiben die Daten dennoch weiter lesbar, es findet also kein Locking statt. Die Konsistenz wird dadurch jedoch nicht ignoriert, da jedes Dokument über eine Revisions-ID verfügt, so dass eventuelle Änderungen nachverfolgt werden können.

Da bei Datenbankzugriffen während des Replikationsvorgangs Versionskonflikte auftreten können, ist eine entsprechende Konfliktbehandlung nötig, welche über das Konsistenzmodell [BASE](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.BASE) mittels der Technik [MVCC](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.MVCC) gewährleistet wird. [3]

### 7.1.7 Sicherheit

### 7.1.8 Bewertung



<hr>
[1] Edlich <br>
[2] http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.MongoDB <br>
[3] https://www.mongodb.com/de/what-is-mongodb



[2] Kindle Buch <br>
[3] http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.CouchDB <br>

[5] http://guide.couchdb.org/editions/1/de/why.html <br>
[6] http://docs.couchdb.org/en/stable/ <br>
[7] https://db-engines.com/de/ranking/document+store
<hr>