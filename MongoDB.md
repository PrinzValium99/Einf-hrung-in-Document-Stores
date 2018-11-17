# 7 Übersicht wichtiger dokumentorientierter Datenbanken

Im Gegensatz zu beispielsweise relationalen Datenbanken gibt es für dokumentenorientierte Datenbanken keine vergleichbare Standardisierung. Aus diesem Grund können unter den verschiedenen Systemen deutlich stärkere Unterschiede festgestellt werden. Im folgenden werden drei Document Store Datenbanksysteme näher behandelt, die laut DB-Engines Ranking zu den wichtigsten Vertretern ihrer Art gehören. [1, 7]

## 7.1 CouchDB ---> LOGO FEHLT NOCH

### 7.1.1 Beschreibung

Die Entwicklung von CouchDB wurde im Jahre 2005 vom ehemaligen Senior-Entwickler von Lotus Notes, Damien Katz zunächst auf privater Basis und später als Apache-Projekt begonnen. CouchDB orientiert sich an Google BigTable und stellt auch MapReduce über JavaScript zur Verfügung. Dieser Datenbank liegt außerdem die Apache Lizenz 2.0 zugrunde, wodurch sie als Open Source Software einzuordnen ist.

CouchDB zeichnet sich vor allem dadurch aus, dass es auch mit einfachen Grundkenntnissen im NoSQL-Bereich leicht benutzbar ist. Dieses Prinzip vermittelt auch das Logo, welches eine Couch und den Schriftzug "relax" zeigt. Nutzer, die bereits Erfahrungen im Bereich der Webentwicklung sammeln konnten, werden einen leichten Einstieg in CloudDB finden. Der Fokus wurde auf eine unkomplizierte und einfache Nutzung der Datenbank gelegt. Dieses Prinzip der Einfachheit gilt auch für die Fehlertoleranz, Fehlersuche, Skalierbarkeit und Performance von CouchDB. Entsprechend geht man z. B. auch davon aus, dass nicht immer eine Netzwerkverbindung vorhanden ist und Fehler in verteilten Systemen vorkommen können. Anders als erwartet steht das Akronym CouchDB für "Cluster of unreliable commodity hardware Data Base". Zusammenfassend lassen sich die besonderen Merkmale dieses dokumentorientieren Datenbanksystems folgendermaßen beschreiben:

- JSON-Dokumente als Datenspeicher
- HTTP (per REST) für Anfragen
- Zuverlässigkeit
- Konsistenz der Datenspeicherung. [1, 3, 5]

### 7.1.2 Architektur und Implementierung

Bei CouchDB werden alle Daten als JSON-Datenstrukturen gespeichert. Diese können über eine HTTP API (RESTful JSON API) erstellt, gelesen oder aktualisiert werden. Wie bereits erwähnt, erfolgen die Abfragen über JavaScript und das MapReduce-Verfahren. CouchDB basiert auf der Erlang OTP-Plattform, welche die Parallelisierung von Anwendungen ermöglicht. Diese Programmiersprache wurde mit einem Fokus auf Zuverlässigkeit und Verfügbarkeit entwickelt. Das Datenbanksystem ermöglicht die Replikation der Daten auf mehrere Knoten, somit können Lesevorgänge parallelisiert werden. Durch ein MVCC-Modell (Multiversion Concurrency Control) können konkurrierende Zugriffe stattfinden. Der Nutzer erhält über den gesamten Zeitraum der Leseoperation einen konsistenten Snapshot der Datenbank ohne andere Zugriffe zu blockieren. [1, 3, 5]

**Noch umschreiben?**

CouchDB ist auf der Erlang OTP Plattform aufgebaut. Das Modul für Views nutzt die JavaScript-Engine SpiderMonkey und Unicode Collation für die Kodierung von Zeichen, legt aber auch Views (genauer permanente Views) im physischen Speicher ab. Apache Lucene kann für Textsuche und Indizierung hinzugefügt werden. Ad-hoc-Abfragen sind über Virtuelle Dokumente (Temporary Views) möglich, somit kann jedes Field eines Dokuments jederzeit abgefragt werden, und der User kann eine Anfrage formulieren, „ohne ein vollständiges Programm schreiben zu müssen“. CouchDB wendet asynchrone Replikation an, des Weiteren handelt es sich um ein Disk-basierend speicherndes DBS, alle Schreibvorgänge werden direkt auf die Festplatte geschrieben, ohne länger im Arbeitsspeicher oder dergleichen temporär gespeichert zu werden. Das Modul *mod_couch* sammelt und wandelt JSON-Dokumente über URL's des Datenbankzugriffs entsprechend um, dabei ersetzt hauptsächlich dieses Modul die mittlere Software-Schicht hin zu einer 2-Schichten-Architektur. [3]

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





<hr>
[1] Edlich <br>
[2] Kindle Buch <br>
[3] http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.CouchDB <br>
[4] http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.MongoDB <br>
[5] http://guide.couchdb.org/editions/1/de/why.html <br>
[6] http://docs.couchdb.org/en/stable/ <br>
[7] https://db-engines.com/de/ranking/document+store
<hr>