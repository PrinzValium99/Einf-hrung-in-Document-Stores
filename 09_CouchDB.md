## 6.1 CouchDB ---> LOGO FEHLT NOCH

### 6.1.1 Beschreibung

Die Entwicklung von CouchDB wurde im Jahre 2005 vom ehemaligen Senior-Entwickler von Lotus Notes, Damien Katz zunächst auf privater Basis und später als Apache-Projekt begonnen. CouchDB orientiert sich an Google BigTable und stellt auch MapReduce über JavaScript zur Verfügung. Dieser Datenbank liegt außerdem die Apache Lizenz 2.0 zugrunde, wodurch sie als Open Source Software einzuordnen ist.

CouchDB zeichnet sich vor allem dadurch aus, dass es auch mit einfachen Grundkenntnissen im NoSQL-Bereich leicht benutzbar ist. Dieses Prinzip vermittelt auch das Logo, welches eine Couch und den Schriftzug "relax" zeigt. Nutzer, die bereits Erfahrungen im Bereich der Webentwicklung sammeln konnten, werden einen leichten Einstieg in CouchDB finden. Der Fokus wurde auf eine unkomplizierte und einfache Nutzung der Datenbank gelegt. Dieses Prinzip der Einfachheit gilt auch für die Fehlertoleranz, Fehlersuche, Skalierbarkeit und Performance von CouchDB. Entsprechend geht man z. B. auch davon aus, dass nicht immer eine Netzwerkverbindung vorhanden ist und Fehler in verteilten Systemen vorkommen können. Anders als erwartet steht das Akronym CouchDB für "Cluster of unreliable commodity hardware Data Base". Zusammenfassend lassen sich die besonderen Merkmale dieses dokumentorientieren Datenbanksystems folgendermaßen beschreiben:

- JSON-Dokumente als Datenspeicher
- HTTP (per REST) für Anfragen
- Zuverlässigkeit
- Konsistenz der Datenspeicherung. [1, 3, 5]

### 6.1.2 Architektur

Bei CouchDB werden alle Daten als JSON-Datenstrukturen gespeichert. Diese können über eine HTTP API (RESTful JSON API) erstellt, gelesen oder aktualisiert werden. Wie bereits erwähnt, erfolgen die Abfragen über JavaScript und das MapReduce-Verfahren. CouchDB basiert auf der Erlang OTP-Plattform, welche die Parallelisierung von Anwendungen ermöglicht. Diese Programmiersprache wurde mit einem Fokus auf Zuverlässigkeit und Verfügbarkeit entwickelt. Das Datenbanksystem ermöglicht die Replikation der Daten auf mehrere Knoten, somit können Lesevorgänge parallelisiert werden. Durch ein MVCC-Modell (Multiversion Concurrency Control) können konkurrierende Zugriffe stattfinden. Der Nutzer erhält über den gesamten Zeitraum der Leseoperation einen konsistenten Snapshot der Datenbank ohne andere Zugriffe zu blockieren. [1, 3, 6]

**Noch umschreiben?**

CouchDB ist auf der Erlang OTP Plattform aufgebaut. Das Modul für Views nutzt die JavaScript-Engine SpiderMonkey und Unicode Collation für die Kodierung von Zeichen, legt aber auch Views (genauer permanente Views) im physischen Speicher ab. Apache Lucene kann für Textsuche und Indizierung hinzugefügt werden. Ad-hoc-Abfragen sind über Virtuelle Dokumente (Temporary Views) möglich, somit kann jedes Field eines Dokuments jederzeit abgefragt werden, und der User kann eine Anfrage formulieren, „ohne ein vollständiges Programm schreiben zu müssen“. CouchDB wendet asynchrone Replikation an, des Weiteren handelt es sich um ein Disk-basierend speicherndes DBS, alle Schreibvorgänge werden direkt auf die Festplatte geschrieben, ohne länger im Arbeitsspeicher oder dergleichen temporär gespeichert zu werden. Das Modul *mod_couch* sammelt und wandelt JSON-Dokumente über URL's des Datenbankzugriffs entsprechend um, dabei ersetzt hauptsächlich dieses Modul die mittlere Software-Schicht hin zu einer 2-Schichten-Architektur. [3]

### 6.1.3 Datenspeicherung

In CouchDB werden Dokumente in Form von JSON-Datenstrukturen abgelegt. Ähnlich wie bei anderen dokumentorientierten Datenbanken geschieht dies schemafrei. Allerdings gibt das JSON Format eine gewisse Struktur durch die Syntax vor. Die Dokumente werden in Unterdatenbanken gespeichert und durch Dokument-IDs bzw. Revisions-IDs indexiert. Die eindeutige Dokument-ID legt der Nutzer selbst fest, die Revisions-ID wird wiederum von CouchDB verwaltet. Sie gibt an, in welcher Version ein Dokument vorhanden ist. Wird eine Instanz aktualisiert, dann lassen sich die Änderungen später anhand der Revisions-ID nachvollziehen. Die einzelnen Dokumente stellen das pendant zu den Tupeln der relationalen Datenbanken dar. Jedes JSON-Objekt wird durch eine Liste von Eigenschaften aufgebaut, wobei jede Eigenschaft durch ein Key/Value-Paar beschrieben wird. Jeder Value kann zusätzlich eine neue Eigenschaft darstellen. Dieses System ermöglicht die beliebige Verschachtelung von Key/Value-Paaren und Listen. [1, 3]

In JSON werden die folgenden Basistypen definiert: Objekte, Arrays, Zeichenketten, Zahlen, Boolesche Werte und null. Sowohl zum Datenaustausch als auch zur Speicherung wird das kompakte JSON-Datenformat genutzt. Damit entfällt die Umwandlung in andere Formate zur Speicherung in einer Datenbank, was sich durch erhöhte Performance bemerkbar machen kann. [1, 5]

In CouchDB findet außerdem eine Unterscheidung diverser Dokumentarten statt. Die folgenden sind von besonderer Bedeutung:

- Datendokumente

- Virtuelle (nicht persistent) Dokumente

- Design Dokumente


**Datendokumente**

Datendokumente bilden eine geschlossene Einheit von Informationen. Als zusätzliche Metadaten werden die oben angesprochenen Dokument-IDs und Revisions-IDs gespeichert. Wie bereits erwähnt wird die Dokument-ID durch den Benutzer vergeben. Es wird empfohlen dafür eine Universally Unique Identifier (UUID) zu verwenden, aber auch benutzerdefinierte IDs funktionieren. Diese UUIDs kann CouchDB auch mit Hilfe eines GET-Request selbst generieren. Im folgenden Beispiel ist ein Datendokument zusehen, welches die Dokument-ID bzw. Revisions-ID als Value zu den Keys   `"_id"` und `"_rev"` zuordnet. [3]


```
{
	"_id"       :	"00a271787f89c0ef2e10e88a0c00048b", 
	"_rev"      :	"1-60e25d93dc12884676d037400a6fa189", 
	"tutor"     :	"Hans Maier", 
	"lecture"   : 
		{
			"Quantencomputer"   : "Raum 102", 
			"Mathematik 1" 		: "Raum 220", 
			"Web Development"	: "Raum 138",
            "Softwaretechnik"	: "Raum 68" 
		} 
}
```

**Virtuelle Dokumente**

Grundsätzlich werden zwar alle Informationen in einem Dokument gespeichert, da dies aber auch Nachteile mit sich bringen kann, ist es manchmal notwendig diese in mehrere logische Dokument-Typen aufzuteilen. Als Beispiel werden oft Blogposts und die dazugehörenden Kommentare genannt. Virtuelle Dokumente werden dazu verwendet, um diese verteilten Informationen als zusammengehörendes Dokument darzustellen. Mit Hilfe einer Anfrage lassen diese temporären Views anzeigen, welche auch als Ad-Hoc-Abfragen bezeichnet werden können. [3]

**Design Dokumente**

Design Dokumente werden von CouchDB genau wie Datendokumente gespeichert und behandelt. Bei einer Replikation werden sie beispielsweise genauso auf die Zieldatenbank kopiert. Der entscheidende Unterschied ist jedoch, dass sie Quellcode enthalten, der mit Hilfe des eingebauten JavaScript-Query-Servers ausgeführt werden kann. Um ein Design-Dokument zu kennzeichnen muss dessen ID mit dem Präfix „_design/“ beginnen. Dieser Dokumenttyp kann aus folgenden Komponenten bestehen :

- View-Funktionen
- Show-Funktionen
- List-Funktionen
- Update-Funktionen
- Validierungs-Funktionen [3, 6]

### 6.1.4 Kommunikation

CouchDB greift zur Kommunikation auf das HTTP Protokoll zurück, da dieses bereits standardisiert und vergleichsweise leicht zu verwenden ist. Zur Übermittlung, Abfragung und Manipulation aller relevanten Daten wird das Architekturprinzip REST verwendet. Jede Ressource wird durch eine URI (Uniform Resource Identifier) beschrieben. Auf diese kann jeweils durch die HTTP-Aufrufe GET, POST, PUT, DELETE zugegriffen werden. Durch die Nutzung dieser etablierten Internettechnik gibt es zahlreiche Möglichkeiten dieses Datenbanksystem anzusteuern. [1, 3]

### 6.1.5 Views

In CouchDB werden zur Aggregation und Darstellung der Daten Views verwendet. Diese greifen nur lesend auf die jeweiligen Dokumente zu und werden dynamisch erzeugt, sobald sie benötigt werden. Außerdem können verschiedene Views erstellt werden, die auf den gleichen Daten basieren. Views werden in den bereits bekannten Design Dokumenten definiert. Zur Erstellung werden MapReduce-Funktionen in der JavaScript-Programmiersprache verwendet. Diese aggregieren die gewünschten Daten, um sie anschließend in der View anzeigen zu können. Weitere Nutzungsmöglichkeiten sind beispielsweise die Filterung von Dokumenten oder die Extraktion und Aufbereitung von Informationen aus Dokumenten. Ebenso kann damit nach Informationen oder Strukturen gesucht und Berechnungen durchgeführt werden. [1, 3]

**MapReduce-Funktion**

Die Views werden automatisch von CouchDB erzeugt, wenn diese vom Anwender abgerufen werden. In diesem Fall wendet das Datenbanksystem die Map-Funktion auf alle Dokumente an. Das Resultat dieser Funktion bezeichnet man als View-Ergebnismenge bzw. View-Rows. Die View-Ergebnismenge kann beliebig viele Einträge in Form von Key/Value-Paaren enthalten. Das folgende Beispiel zeigt eine Map-Funktion.

```
function(doc) {
	if (doc.tutor && doc.lecture) {
		emit([ doc.tutor, doc.lecture ], 1);
	}
}
```

Die Map-Funktion bekommt ein Dokument als Parameter "doc" übergeben. Da die Map-Funktion auf alle Dokumente angewendet wird, muss anschließend geprüft werden, ob das übergebene Dokument die Schlüssel "tutor" und "lecture" enthält, um die entsprechenden Dokumente herauszufiltern. Im Anschluss trägt die emit-Funktion ein Key/Value-Paar in die Ergebnismenge ein. Sind mehrere Einträge gewünscht, dann kann die emit-Funktion auch mehrere Male aufgerufen werden. Im Beispiel wird eine Kombination aus den beiden Eigenschaften "tutor" bzw. "lecture" in einem Array als Schlüssel zurückgegeben.

Das folgende Beispiel zeigt eine einfache Reduce-Funktion .
```
function(keys, values, rereduce) {
   return sum(values);
}
```

Zur Betrachtung der Reduce-Funktion ist es wichtig zu wissen, dass die Ergebnismenge der Map-Funktion als B+-Baum verwaltet wird. Die Reduce-Funktion durchläuft jeden Knoten des Baums, sofern keine Filterung stattfindet. In den ersten beiden Parametern werden Keys und Values übergeben, diese werden zwischengespeichert. Der dritte Parameter bestimmt, ob ein Blätter-Knoten oder ein innerer Knoten durchlaufen wird. Da bei B+-Bäumen die Nutzdaten nur in den Blättern gespeichert werden ist eine derartige Unterscheidung notwendig. Auf einzelne Einträge aus der Ergebnismenge der Map-Funktion können bei den Blättern Operationen ausgeführt werden. Bei den inneren Knoten wiederum kann mit den gespeicherten Zwischenergebnissen weitergearbeitet werden. [3]

### 6.1.6 Replikation

Die [Replikation](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.Replikation), d.h. die Übertragung der Daten auf andere Knoten, ist bei Apache CouchDB ein inkrementeller Prozess per Push und Pull. Wie die Client-Server Kommunikationsvorgänge wird auch die Replikation über HTTP-Requests abgewickelt. Die Daten werden dokumentweise auf Server übertragen, die sich an geografisch stark unterschiedlichen Orten befinden, um geringe Latenzen bieten zu können („move data more closely to clients“). Über „Continuous Replication“ kann relativ komfortabel eine unidirektionale Replikation, welche als Backup dienen kann, faktisch aber keines darstellt, eingerichtet werden, diese kann zudem zu einer bidirektionalen Replikation erweitert werden. Die Backupserver sind hierbei nicht aktiv für Abfragen eingebunden. Um die bidirektionale Replikationen im Rahmen von Load-Balancing einsetzen zu können, müssen zusätzliche Frameworks wie „CouchDB Lounge“ verwendet werden. Für Partitionierung (bzw. Sharding) wird ebenfalls einer der genannten Forks von Apache CouchDB benötigt, um im Kontext von verteilter Einrichtung besser zu skalieren. Die dokumentweise Übertragung dient dazu, um bei Unterbrechung des Kommunikationsprozesses die Übertragung dort fortzusetzen, wo sie abgebrochen worden ist. Damit ist ein Neustart der Replikation nicht erforderlich und das System wird robuster gegenüber Fehlern. 
Über [Futon](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.Futon) kann ein entsprechender Replikationsprozess couch-entsprechend bequem initialisiert werden.

Bei der Entwicklung des Replikationsverfahrens ging man davon aus, ein CouchDB-Knoten sei im Normalfall nicht erreichbar("offline by default"). Daher wurde bei CouchDB der Fokus auf eine hohe Ausfalltoleranz (siehe [CAP-Theorem](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.CAP)) gelegt.
Ein wesentliches Augenmerk bei der Entwicklung von CouchDB lag auf dem Aspekt der Verfügbarkeit. Bei Replikationsvorgängen bleiben die Daten dennoch weiter lesbar, es findet also kein Locking statt. Die Konsistenz wird dadurch jedoch nicht ignoriert, da jedes Dokument über eine Revisions-ID verfügt, so dass eventuelle Änderungen nachverfolgt werden können.

Da bei Datenbankzugriffen während des Replikationsvorgangs Versionskonflikte auftreten können, ist eine entsprechende Konfliktbehandlung nötig, welche über das Konsistenzmodell [BASE](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.BASE) mittels der Technik [MVCC](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.MVCC) gewährleistet wird. [3]

CouchDB unterstützt das Replizieren der Daten auf mehrere Knoten inkrementell mit bidirektionaler
Konflikterkennung und bidirektionalem Konfliktmanagement und kann so
Lesevorgänge parallelisieren. Das Replizieren kann von der Anwendung ausgelöst werden
oder auch kontinuierlich erfolgen. CouchDB erlangt seine Verteiltheit über Replikation
zwischen einzelnen CouchDB-Knoten und kann somit als peer-based distributed bezeichnet
werden. CouchDB rechnet damit, dass nicht immer eine permanente Verbindung zwischen
den einzelnen CouchDB-Knoten vorhanden ist. Man kann sagen, eine CouchDB-Instanz ist
offline by default. Sobald die Knoten nach einer Unterbrechung wieder Netzzugang besitzen,
erfolgt die Synchronisation auf eine vorher definierte Weise. Die bei einer Synchronisation
üblicherweise auftretenden Konflikte werden durch die CouchDB-Konflikterkennung markiert.
CouchDB wählt deterministisch eine gewinnende Version des konfliktbehafteten
Datensatzes aus. Ist man mit der Auswahl nicht zufrieden, so kann man manuell oder
durch eine Anwendung die gewünschte Revision über die Markierung auswählen und den
Konflikt lösen. Es ist auch möglich, über Filter partielle Replikationen von Dokumenten
vorzunehmen. CouchDB ermöglicht den Austausch aller Dokumente über Replikationen,
sodass vollständige Datenbankanwendungen, einschließlich Anwendungsdesign, Logik
und Daten, repliziert werden können.
Auch einfache getriggerte Replizierungen lassen sich über das Web-Interface Futon durch
Auswahl des Links Replicator im Tool-Menü erstellen. [1]

### 6.1.7 Sicherheit

Für den Schutz vor unberechtigten Zugriffen bietet CouchDB ein einfaches Modell der Zugriffskontrolle. Hier wird zwischen den folgenden Bereichen unterschieden:



- Administratorzugriff

- Lesende Zugriffe

- Update Validierung

Neue Accounts können von Administratoren angelegt werden. Diese haben ebenfalls den Zugriff auf die sogenannten *design documents*, in denen sich neue Views auf Basis von [MapReduce-Funktionen](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.MapReduce) in Form von JavaScript abbilden lassen. Mit Hilfe von erstellbaren Nutzerlisten kann die Leseberechtigung von Dokumenten eingeschränkt werden. Die Validierung der Schreibrechte erfolgt hier ebenfalls im Hintergrund durch entsprechende JavaScript-Funktionen. [3]



Für die Zugriffskontrolle und damit zum Schutz der Daten bietet CouchDB ein einfaches
Modell für den lesenden Zugriff und zur Validierung von Updates. Dieses kann, je nach
gestellter Anforderung, in den folgenden Bereichen angepasst werden:
 Administrator Access
 Reader Access
 Update Validation
Administratoren können neue Accounts anlegen und haben unter anderem Zugriff auf die
design documents, in denen die View-Funktionen enthalten sind. Für die Dokumente lassen
sich Nutzerlisten festlegen, über die geregelt wird, welche Nutzer das Dokument oder
Teile davon sehen dürfen. Wenn die Daten auf die Festplatte geschrieben werden, können
sie dynamisch durch JavaScript-Funktionen validiert und auf Schreibrechte überprüft
werden. [1]

### 6.1.8 Bewertung

**Vorteile**

- Schemafreiheit
- Integrierter Webserver
- Kommunikation mit HTTP
- Einfache Anbindung an Web-Anwendungen
- Keine separaten Schnittstellen nötig
- Unter Apache Lizenz 2.0 verfügbar
- Nachträgliche Änderung von Dokumentenformaten möglich
- Verteilte Datenbank, allerdings fragwürdiges Prädikat "verteilt" (auch im Sinne des Akronyms *"Cluster of ..."*) nur über Replikation [vgl. 39] [vgl. 42] [vgl. 43]
- Sehr hohe Verfügbarkeit
- Wird weiterentwickelt
- Views um Join-Funktionalität zu bieten
- gut bei Fokus auf Versionierung [vgl. 40]
- PHP unterstützt [Apache CouchDB](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.CouchDB) als Speichermedium (Clustering des PHP App Servers) [vgl. 44]

**Nachteile**

- ~~Noch nicht völlig ausgereift~~
- Einige Features verteilter Datenbanken werden noch nicht unterstützt
- MapReduce bei aufwendigen Abfragen ggf. komplizierter als [SQL](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.SQL)
- ~~Bietet nicht die Abfragemöglichkeiten relationaler DBMS~~
- ~~Struktur der Dokumente erfordert Disziplin des Anwenders~~
- Umdenken vom relationalen Konzept nötig
- ~~Sehr spezifisch auf Webanwendungen zugeschnitten~~
- Bug in Version 1.0 konnte zu Datenverlust führen, seit 1.0.1 behoben
- Im Zusammenhang mit den Map/Reduce-Funktionen sind JavaScript-Kenntnisse erforderlich
- kein Caching, alle Schreibvorgänge direkt auf Disk [vgl. 39]
- [DB's](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.Datenbank) können sehr groß werden, manuelle Datenkomprimierung nötig [vgl. 39] [vgl. 40] [vgl. 41] [vgl. 42] [vgl. 43]
- Erstellung von Views im Vergleich zu [SQL](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.SQL) -Queries zeitaufwändig [vgl. 41]
- vergleichsweise hohe Latenz aufgrund HTTP Document API [vgl. 42] [vgl. 43]
- keine offizielle Unterstützung partieller Updates von Dokumenten [vgl. 39], zukünftig allerdings geplant
- an sich nur für gelegentliche Veränderung von Daten [vgl. 40]



Für das spezifische Anwendungsfeld der Webanwendungen scheint CouchDB durchaus gut geeignet zu sein. Sollte es sich hauptsächlich ein System zur Eingabe und Speicherung von Daten handeln, eignet sich CouchDB bzw. allgemein eine dokumentenorientierte Datenbank. Ist häufiges Bearbeiten der Daten, etwa in Form von Berechnungen nötig, oder werden oft komplexe Anfragen durchgeführt, empfiehlt sich eher ein relationales System, da durch [SQL](http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.SQL) ein entsprechend mächtiges Werkzeug geboten wird und in CouchDB die meisten Funktionen selbst programmiert werden müssen.
CouchDB ist kein Konkurrent für herkömmliche relationale DBMS und versucht auch nicht als ein solcher aufzutreten. Die Anwendungsbereiche der Systeme sind schlicht und einfach völlig verschieden. Durch seinen webanwendungsnahen Aufbau bringt CouchDB für Anwender in diesem Bereich eine Menge Komfort mit, so dass die Erwägung, CouchDB zu nutzen, durchaus berechtigt erscheint. [3]

Das Motto der CouchDB ist „relax“, und dieses Motto sollte man
ernst nehmen. Die hier vorgestellten Tools für die Verwendung
von CouchDB vereinfachen in erster Linie die Kommunikation
per GET/PUT. Angenehm wird es, wenn ein Wrapper beim
Speichern eines Dokuments dieses auf Updates prüft, oder wenn
– wie im Fall von PHPillow – View-Dokumente in PHP definiert
werden können. Der Vorteil von CouchDB besteht darin, so wenig
Funktionen wie nötig bereitzustellen und dem
Anwendungsprogrammierer freie Hand zu lassen. Ob ein
Wrapper, der den Programmierer dann wieder auf vorgegebene
Funktionen festlegt, da der richtige Weg ist, muss jeder für sich
entscheiden. Die eigentliche Kraft der CouchDB steckt in den
Views und in den hier nicht angesprochenen weiteren
Möglichkeiten, Ergebnisse zu Transformieren (Lists, Shows).
Die hier gezeigten Wrapper sind leicht zu verstehen, und auf der
Heft-CD finden Sie eine Menge Beispiele zum Nachvollziehen.
Ihre Energie sollten Sie auf das Entwickeln in der CouchDB
stecken. JavaScript ist als Standard implementiert, allerdings
kann jede Sprache, die auf dem Server läuft und über die
Standardkonsole kommuniziert, eingebunden werden. So ist es
möglich, alle Map/Reduce-Funktionen in PHP zu programmieren.
CouchDB sollte man nicht nur als Datenbankmanagementsystem
sehen, sondern als Ökosystem von Servern, Daten und
Anwendungen. So ist es möglich, gänzlich ohne weitere
serverseitige Sprachen komplette Anwendungen in einer
CouchDB zu entwickeln. Ob Datendokumente, Designdokumente,
HTML-Templates oder JPG-Attachments, alles kann in einer
CouchDB gespeichert und damit auch auf andere Datenbanken
repliziert werden. So erreicht man eine schnelle und sichere
Verteilung der Anwendung auf viele Server. [2]

CouchDB wird von seinen Entwicklern als Local-Web-Plattform gesehen und setzt auf bewährte
Web-Techniken „build of the web“ auf. Das macht den ersten Einstieg und Umgang
mit CouchDB einfach und rüstet die Datenbank für zukünftige Entwicklungen im Internet.
CouchDB rechnet mit dem Auftreten von Fehlern in verteilten Systemen „offline by default“
und bietet Möglichkeiten zur Konflikterkennung und zum Konfliktmanagement. Anwendungen
mit dieser Datenbank lassen sich auch ohne Netzzugang nutzen. CouchDB schlägt
eine Brücke zwischen Anwendungen im Internet bzw. in einer Cloud und lokalen Anwendungen.
Das Paradigma der Document Stores passt auf Anwendungsbereiche, bei denen
ein relationales Schema die Flexibilität der Anwendung einschränkt.
Vorteile
 Setzt auf bewährte Web-Techniken und Erlang als Entwicklungsumgebung
 Robust und fehlertolerant
 Flexible und vielseitige Replizierungsmechanismen
 Bietet Konflikterkennung und Konfliktmanagement
 Erfordert keine Schemaerstellung
 Lässt sich auf vielen Betriebssystemen installieren
 Liefert eigenes Web-Interface Futon mit intuitiver Bedienung
 Bietet APIs für viele Programmiersprachen über Plug-in-Architektur

Nachteile
 Views-Aktualisierung und Erzeugung der Indizes erfolgt erst beim Datenzugriff, der
dadurch nach vielen Änderungen zeitlich verzögert wird.
 Keine partiellen Updates. Fehlermeldungen sind nicht immer hilfreich.
 Bietet keine eigenen Skalierungsmechanismus außer über Replizierung. Eine Skalierung
ist aber über CouchDB-Lounge der Firma Meebo möglich.
 Bisher nur inoffizielle Unterstützung für Windows über einen binary installer im Betastadium.
 Realisierung erweiterter Abfragen über Map/Reduce könnten aufwendiger sein als mit
SQL und bedürfen etwas Einarbeitungszeit.
Typische Einsatzbereiche für CouchDB sind daher mobile oder Offline-Anwendungen im
Web. Es werden gerade nicht extrem hochskalierbare Anwendungen adressiert. Eine Auflistung
der Einsatzbereiche ist unter anderem auch über das CouchDB-Wiki zu finden:
http://wiki.apache.org/couchdb/CouchDB_in_the_wild.
Apache CouchDB wird derzeit unter anderem von der BBC, Meebo, Assay Depot und
Engine Yard eingesetzt und ist mittlerweile ein integraler Bestandteil des Ubuntu-Betriebssystems
geworden. Der File-Hosting-Dienst Ubuntu-One der Firma Canonical Ltd.
nutzt CouchDB zur Synchronisierung von Profildaten. Einige Fallstudien zum Einsatz von

CouchDB sind auch auf der Website http://www.couchbase.com/customers/case-studies
zu finden.
Die Apache CouchDB Version 1.0 ist im Verlauf der Bucherstellung, nämlich am 14. Juli
2010 fertiggestellt worden. Damit hat die Datenbank einen weiteren Meilenstein in ihrer
Entwicklung zum vollwertigen, produktiv einsetzbaren Datenbankmanagementsystem erreicht. [1]





<hr>
[1] Edlich <br>
[2] Kindle Buch <br>
[3] http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.CouchDB <br>
[4] http://wikis.gm.fh-koeln.de/wiki_db/index.php?n=Datenbanken.MongoDB <br>
[5] http://guide.couchdb.org/editions/1/en/index.html <br>
[6] http://docs.couchdb.org/en/stable/ <br>
<hr>