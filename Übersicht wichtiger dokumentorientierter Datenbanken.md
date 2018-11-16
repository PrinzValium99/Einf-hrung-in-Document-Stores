# 7 Übersicht wichtiger dokumentorientierter Datenbanken

## 7.1 CouchDB

### 7.1.1 Beschreibung

der Anspruch von Apache CouchDB, über einfache Grundkonzepte im [NoSQL](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.NoSQL) -Bereich selbst für Laien gebrauchstauglich zu sein, wird bereits bei den ersten Kontakten sichtbar. Apache CouchDB ist eine Implementierung des [dokumentenorientierten Datenbankparadigmas](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.DokumentenorientierteDatenbank), die unter der Apache 2.0-Lizenz zur Verfügung gestellt wird und orientiert sich an Google BigTable. Dabei ist CouchDB ein Akronym und steht für **C**luster **o**f **u**nreliable **c**ommodity **h**ardware **D**ata **B**ase. Die herauszustellenden Merkmale dieses dokumentenorientierten DBS sind:

1. [JSON](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.JSON) -Dokumente als Datenspeicher,
2. HTTP (per REST) für Anfragen, und
3. Zuverlässigkeit sowie
4. Konsistenz der Datenspeicherung.

Da es für dokumentenorientierte Datenbanken keine mit [SQL](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.SQL) vergleichbare Standardisierung gibt, unterscheiden sich die jeweiligen Anwendungsprogramme deutlich stärker als beispielsweise bei [relationalen Datenbanken](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.RDBMS). Mit "Couch is Lotus Notes built from the ground up for the Web" setzte Damien Katz, der Erfinder von CouchDB, den primären Einsatzbereich des DBS auf die Entwicklung von Webanwendungen. Des Weiteren ist Apache CouchDB über die zugrundeliegende Apache Lizenz 2.0 nach der Open Source Initiative als Open Source Software einzuordnen, nutzt MapReduce über JavaScript, und stellt die eingebetteten Anwendungen CouchApps  im Sinne eines Anwendungsservers bereit. [3]



CouchDB ist wie viele andere NoSQL-Datenbanken auch entwickelt worden, um den wachsenden
Anforderungen der Web 2.0-Zeitalters gerecht werden zu können. Dieser Document
Store orientiert sich an Googles BigTable und damit auch an der Zugriffsmöglichkeit
auf Daten mittels Map/Reduce sowie am Dokumentmanagement-Framework Lotus Notes.
Inspiriert durch die Vorteile dieser Technologien hat der ehemalige Senior-Entwickler von
Lotus Notes, Damien Katz, im Jahre 2005 mit der Entwicklung der dokumentorientierten
Datenbank CouchDB begonnen. Die zuerst auf privater Basis und später als Apache-Projekt
entstandene Datenbank erfreut sich seitdem wachsender Beliebtheit. [1]

Auf der offiziellen Website der Datenbank CouchDB fällt einem sofort das CouchDB-Logo
mit der plakativ dargestellten entspannten Person und der Schriftzug „relax“ auf. Dieses
Logo symbolisiert das grundsätzliche Prinzip des Projektes, denn CouchDB setzt auf bewährte
Prinzipien. Entwickler, die sich mit CouchDB beschäftigen und schon Erfahrung
im Bereich der Webentwicklung haben, werden sich in CouchDB daher schnell zurechtfinden.
Die CouchDB-Entwickler legten und legen den Fokus ihrer Arbeiten auf eine einfache
unkomplizierte Nutzung der Datenbank. Entspannung ist auch im Kontext der Fehlertoleranz,
Fehlersuche, Skalierbarkeit (über die CouchDB-Lounge) und Performance angesagt,
auch in diesen Bereichen wird es den Entwicklern leicht gemacht. CouchDB rechnet damit,
dass nicht immer und überall eine Netzwerkverbindung vorhanden ist, und dass Fehler in verteilten Systemen nichts Ungewöhnliches sind. Der Name CouchDB steht deshalb
ironischer Weise für: „Cluster of unreliable commodity hardware Data Base“ [1]



### 7.1.1 Architektur und Implementierung

Dokumente werden über eine HTTP API ( REST) erstellt, gelesen oder aktualisiert. Dabei nutzt die Anfragespache wie beschrieben JavaScript und MapReduce, um auf die internen Module zuzugreifen. CouchDB ist auf der Erlang OTP Plattform aufgebaut. Das Modul für Views nutzt die JavaScript-Engine SpiderMonkey und Unicode Collation für die Kodierung von Zeichen, legt aber auch Views (genauer permanente Views) im physischen Speicher ab. Apache Lucene kann für Textsuche und Indizierung hinzugefügt werden. Ad-hoc-Abfragen sind über Virtuelle Dokumente (Temporary Views) möglich, somit kann jedes Field eines Dokuments jederzeit abgefragt werden, und der User kann eine Anfrage formulieren, „ohne ein vollständiges Programm schreiben zu müssen“. CouchDB wendet asynchrone Replikation an, des Weiteren handelt es sich um ein Disk-basierend speicherndes DBS, alle Schreibvorgänge werden direkt auf die Festplatte geschrieben, ohne länger im Arbeitsspeicher oder dergleichen temporär gespeichert zu werden. Das Modul *mod_couch* sammelt und wandelt [JSON](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.JSON) -Dokumente über URL's des Datenbankzugriffs entsprechend um, dabei ersetzt hauptsächlich dieses Modul die mittlere Software-Schicht hin zu einer 2-Schichten-Architektur. [3]

### 7.1.1 Speicherung der Daten

Es existieren im Rahmen von CouchDB diverse Dokumentarten, die jeweils eine eigene Verantwortung haben. Von zentraler Bedeutung sind

1. Daten-,
2. Virtuelle (nicht persistent) und
3. Design Dokumente.

Die Dokumente in CouchDB werden in der Java Script Object Notation ([JSON](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.JSON)) gespeichert, wobei dies schemafrei abläuft. Dennoch werden für ein korrektes Auslesen semi-strukturierte Daten benötigt, denn die (Web-)Anwendungen, nicht die Datenbank selbst, haben die Schemaverantwortung, zudem gibt [JSON](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.JSON) eine gewisse Ordnung durch die Syntax vor. Die Dokumente selbst können in benennbaren Unterdatenbanken, die man sich am besten als Dokumentenverzeichnisse vorstellen kann, gespeichert werden. Dabei verfügt jedes persistente Dokument über eine vom Benutzer bestimmbare Dokument-ID, die innerhalb einer Datenbank eindeutig sein muss, und über eine von CouchDB verwaltete Revisions-ID, die angibt, in welcher Version ein Dokument vorliegt. Die einfachste Form, Dokumente zu erzeugen, ist über eine REST-Konforme HTTP-Anfrage, welche in einem internen [B-Plus-Bäumen](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.B-Plus-Baum) gespeichert werden. [3]

### 7.1.1 Kommunikation

Die Kommunikation mit CouchDB wird durch HTTP-Anfragen realisiert, so dass kein eigenes Kommunikationsprotokoll definiert werden muss. Die Verwendung von HTTP erleichtert zudem die Anbindung an Web-Anwendungen enorm, des Weiteren ist das Protokoll ein allgemein bekannter Standard und leicht zu verwenden. Da es sich bei HTTP um ein zustandsloses Protokoll handelt, müssen alle relevanten Transaktionsdaten in einer Anfrage übergeben werden. Man spricht in diesem Zusammenhang von [REST](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.REST) (Representational State Transfer). Um mit CouchDB zu kommunizieren, bietet sich u.a. das Kommandozeilenwerkzeug [cURL](http://curl.haxx.se/) an. Im Folgenden werden einige Beispiele der Kommunikation mit CouchDB aufgelistet. Die Eingabe wird mit *curl* in einer Kommandozeilenumgebung durchgeführt, die Ausgabe wird ebenfalls auf der Kommandozeile dargestellt. Die Ausgabe erfolgt in Form eines [JSON](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.JSON) -Objekts. [3]

### 7.1.1 Views

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

### 7.1.2 Performance ???

### 7.1.2 Replikation

Die [Replikation](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.Replikation), d.h. die Übertragung der Daten auf andere Knoten, ist bei Apache CouchDB ein inkrementeller Prozess per Push und Pull. Wie die Client-Server Kommunikationsvorgänge wird auch die Replikation über HTTP-Requests abgewickelt. Die Daten werden dokumentweise auf Server übertragen, die sich an geografisch stark unterschiedlichen Orten befinden, um geringe Latenzen bieten zu können („move data more closely to clients“). Über „Continuous Replication“ kann relativ komfortabel eine unidirektionale Replikation, welche als Backup dienen kann, faktisch aber keines darstellt, eingerichtet werden, diese kann zudem zu einer bidirektionalen Replikation erweitert werden. Die Backupserver sind hierbei nicht aktiv für Abfragen eingebunden. Um die bidirektionale Replikationen im Rahmen von Load-Balancing einsetzen zu können, müssen zusätzliche Frameworks wie „CouchDB Lounge“ verwendet werden. Für Partitionierung (bzw. Sharding) wird ebenfalls einer der genannten Forks von Apache CouchDB benötigt, um im Kontext von verteilter Einrichtung besser zu skalieren. Die dokumentweise Übertragung dient dazu, um bei Unterbrechung des Kommunikationsprozesses die Übertragung dort fortzusetzen, wo sie abgebrochen worden ist. Damit ist ein Neustart der Replikation nicht erforderlich und das System wird robuster gegenüber Fehlern. 
Über [Futon](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.Futon) kann ein entsprechender Replikationsprozess couch-entsprechend bequem initialisiert werden.

Bei der Entwicklung des Replikationsverfahrens ging man davon aus, ein CouchDB-Knoten sei im Normalfall nicht erreichbar("offline by default"). Daher wurde bei CouchDB der Fokus auf eine hohe Ausfalltoleranz (siehe [CAP-Theorem](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.CAP)) gelegt.
Ein wesentliches Augenmerk bei der Entwicklung von CouchDB lag auf dem Aspekt der Verfügbarkeit. Bei Replikationsvorgängen bleiben die Daten dennoch weiter lesbar, es findet also kein Locking statt. Die Konsistenz wird dadurch jedoch nicht ignoriert, da jedes Dokument über eine Revisions-ID verfügt, so dass eventuelle Änderungen nachverfolgt werden können.

Da bei Datenbankzugriffen während des Replikationsvorgangs Versionskonflikte auftreten können, ist eine entsprechende Konfliktbehandlung nötig, welche über das Konsistenzmodell [BASE](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.BASE) mittels der Technik [MVCC](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.MVCC) gewährleistet wird. [3]

### 7.1.3 Sicherheit

### 7.1.3 Bewertung



## 7.2 MongoDB

### 7.2.1 Beschreibung

MongoDB gehört zu den Stars am Himmel der NoSQL-Vertreter – gemessen an der Euphorie,
die dieser Datenbank in der Blogosphäre entgegen gebracht wird. Dies ist kaum verwunderlich,
kann MongoDB doch mit Features auftrumpfen, die man bei anderen Vertretern
aus dem NoSQL-Lager vermisst.
MongoDB hat das Ziel, die Lücke zwischen klassischen relationalen Datenbanken und den
Key/Value-Stores zu schließen. Dazu sollen möglichst umfangreiche Abfragemöglichkeiten
mit guter Skalierbarkeit und Performance kombiniert werden, um ernsthaft mit klassischen
RDMBS konkurrieren zu können. Darüber hinaus kann MongoDB an viele bekannte
Programmiersprachen angebunden werden.
Es sollte erwähnt werden, dass hinter MongoDB ein Team bekannter Größen aus erfolgreichen
Web-Unternehmen in den USA steht, die ihre langjährigen technischen Erfahrungen
in der Entwicklung von MongoDB bündeln. [1]







## 7.3 Couchbase







------

[1] Edlich
[2] Kindle Buch
[3] http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.CouchDB
[4] http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.MongoDB
[5] http://guide.couchdb.org/editions/1/de/why.html
[6] 

