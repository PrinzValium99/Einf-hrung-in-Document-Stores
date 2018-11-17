# Einleitung


# Entwicklung und Ursprung:

Dokumentenorientierte Datenbanken stellen die am weitesten verbreitete und beliebteste Alternative zu den klassischen relationalen Datenbanken dar. 

Sie beruhen auf keinem festen Schema, das hingegen bei relationalen Datenbanken der Fall ist und gehören somit zu deren "Gegenspieler", den NoSQL Datenbanken. - [1 onlinequelle ]

Zu beachten ist, dass der Begriff NoSQL keineswegs „No" impliziert und nicht einfach mit „kein“
gleichzusetzen ist. Für die meisten steht es für „Not only SQL“ – also nicht für ein Ende der Ab-fragesprache SQL.

NoSQL Datenbanken können sich recht stark unterscheiden, da ihnen unterschiedliche Datenbankmodelle zu Grunde liegen. Die Unterschied, der sie von relationalen Datenbanken stark abgrenzen lässt und sie zusammenfassen lässt, liegt in der Schemafreiheit begründet. 

Erstaunlicherwesie begann die Geschichte der NoSQL-Datenbank Systeme durchaus schon parallel zu der der relationalen Datenbank Systemen. Bereits 1979 entwickelte Ken Thompson eine Key/Hash-Datenbank namens DBM. Aber erst 1998 tauchte der Begriff NoSQL zum ersten Mal bei einer Datenbank von Carlo Strozzi auf. Seiner Datenbank lag zwar immer noch ein relationales Datenbankmodell zugrunde, er stellte aber keine SQL-API zur Verfügung.

Der eigentliche Schub für NoSQL kam aber erst ab 2000 mit der Einführung des Web 2.0 und dem Versuch, auch große Datenmengen zu verarbeiten. Google kann man mit seinem BigTable-Datenbanksystem (2004) als den NoSQL-Vorreiter schlechthin betrachten. Später zogen Firmen wie Yahoo, Amazon und später bald auch alle sozialen Netzwerke wie MySpace, Facebook, LinkedIn usw. nach. 

Bis 2005 entstanden einige im Vergleich kleinere hochinteressante Datenbanken, die in vielen Facetten schon NoSQL-Charakter aufwiesen. [2 whitepaper MongoDB]

Von 2006 bis 2009 entstanden dann die heutigen klassischen NoSQL-Systeme. Doch erst 2009 tauchte der heutige Begriff in einem Weblog von Eric Evans zum ersten Mal auf [3 Oska09].  

Um den Bogen zurück zu  Document Stores zu spannen, ist man allgemein der Auffassung, dass der Bereich der dokumentenorientierten Datenbanken zu den interessantesten Teilen der NoSQL-Bewegung gehört. [4 NoSQL - ein Einstieg in die …]

Jedoch muss man mit dem Begriff  “Document Stores” vorsichtig sein. Sie sind im eigentlichen Sinne keine echten Dokumentendatenbanken. Der Begriff selbst stammt noch aus der Zeit von Lotus Notes, wo tatsächlich echte Anwenderdokumente gespeichert wurden. Wahrscheinlich wurde der Begriff sogar vom ehemaligen Lotus Notes-Entwickler Damien Katz geprägt, der später für CouchDB arbeitete.

Jedoch ist die Anzahl der wirklich relevanten dokumentenorientierten Datenbanken relativ gering. Neben MongoDB haben noch Couchbase und CouchDB eine große Bedeutung [5 Online Quelle: https://db-engines.com/en/ranking/document+store]



## Datenmodell

Bei dokumentenorientierten Datenbanken werden Daten in Form von Dokumenten gespeichert. Gemeint sind hier aber nicht Word- oder Textdateien, sondern strukturierte Datensammlungen wie JSON oder XML-Dokumente, beides bei Entwicklern beliebtes Format. Document Stores legen z.B. JSON-Dateien zusammen mit einer ID ab. Meist legt die Datenbank nur fest, auf welches Format die ID weist. Mehr aber auch nicht. [Oska09]

Die Strukturierung in Dokumenten bieten eine intuitive und natürliche Möglichkeit, Daten zu modellieren, die eng mit der objektorientierten Programmierung verbunden sind - jedes Dokument ist praktisch ein Objekt. Dokumente enthalten ein oder mehrere Felder, wobei jedes Feld einen typisierten Wert enthält, wie z.B. Zeichenkette, Datum, Binärwert, Dezimalwert oder Array. Anstatt einen Datensatz über mehrere Spalten und Tabellen zu verteilen, die mit Fremdschlüsseln verbunden sind, werden jeder Datensatz und seine zugehörigen (d.h. verwandten) Daten typischerweise zusammen in einem einzigen, hierarchischen Dokument gespeichert. Dieses Modell beschleunigt die Produktivität der Entwickler, vereinfacht den Datenzugriff und erübrigt in vielen Fällen aufwendige JOIN-Operationen und komplexe Transaktionen mit mehreren Datensätzen.

Wie bereits erwähnt sind dokumentenorientierte Datenbanken schemafrei, wobei das Schema als dynamisch angesehen werden kann: Jedes Dokument kann verschiedene Felder enthalten. Diese Flexibilität kann besonders bei der Modellierung unstrukturierter und polymorpher Daten hilfreich sein. *Das Schema wird in diesem Sinne mit Einfügen eines Dokuments zur Laufzeit erzeugt.*  Dies erleichtert die Entwicklung einer Anwendung während ihres Lebenszyklus, z.B. das Hinzufügen neuer Felder. Darüber hinaus bieten einige dokumentenorientierte Datenbanken Query-Ausdrücke, die Entwickler von relationalen Datenbanken gewohnt sind. Insbesondere können Daten basierend auf einer beliebigen Kombination von Feldern in einem Dokument abgefragt werden, wobei umfangreiche Sekundärindizes effiziente Zugriffspfade bieten, die nahezu jedes Abfragemuster unterstützen.

## Geschwister von Doument stores

Document stores gehören zweifelsohne zu den wichtigsten NoSQL Datenbanken. Andere wichtige No-SQL Datenbanken sind

-  **Schlüssel/Wert-orientiert (engl. Key/Value):** 

  Abgefragt wird auf den Schlüssel, der einen beliebigen String (z. B. XML oder ein serialisiertes Objekt) zurückliefert.

-  **Spaltenorientiert:** 

   Dieser Speichertyp greift über einen Schlüssel gezielt auf Einzelwerte einer Struktur (Spaltenfamilie) zu.

-  **Graphenorientiert:** 

  Entscheidender Anwendungsfall ist das Traversieren der Objekte, wie z. B. bei Verbindungen in Social Networks oder Produktempfehlungen. Die Daten werden in Knoten (Entitäten) und Kanten (Beziehungen) aufgeteilt, welche mit Attributen versehen werden können.

## Anwendung von Document Stores

CouchDB wird von seinen Entwicklern als Local-Web-Plattform gesehen und setzt auf be- währte Web-Techniken „build of the web“ auf. Das macht den ersten Einstieg und Umgang mit CouchDB einfach und rüstet die Datenbank für zukünftige Entwicklungen im Internet. CouchDB rechnet mit dem Auftreten von Fehlern in verteilten Systemen „offline by default“ und bietet Möglichkeiten zur Konflikterkennung und zum Konfliktmanagement. Anwen- dungen mit dieser Datenbank lassen sich auch ohne Netzzugang nutzen. CouchDB schlägt eine Brücke zwischen Anwendungen im Internet bzw. in einer Cloud und lokalen Anwen- dungen. Das Paradigma der Document Stores passt auf Anwendungsbereiche, bei denen ein relationales Schema die Flexibilität der Anwendung einschränkt. [edlich]



Häufig sind sie explizit für ein verteiltes Arbeiten mit großen bis sehr großen Datenmengen ausgelegt, bieten diesem Einsatzzweck entsprechende Datenstrukturen und verzichten bewusst auf Transaktionen. [https://www.innoq.com/en/articles/2011/01/nosql-einsatzgebiete/]

IoT

NoSQL Datenbanken erfahren Beliebheit im Bereich von IoT. Aufrung von Performance und Kostengründen. IoT Applikationen sind darauf angewiesen Prozesse mit großen Daten Volumen durchzuführen. Dies erfordert eine schnelle und kostengünstige Skalierbarkeit und ist somit nur mit neuen BigData Technologien wie MongoDB durchzuführen. [https://www.mongodb.com/scale/internet-of-things-applications]

[MongoDB Paper - Why NoSQL Databases for the Internet of Things: Machina Research]





Aus Quelle:

[https://www.infoworld.com/article/2612785/application-development/10-common-tasks-for-mongodb.html]

 **1. Profiles of people**

In User-Profilen gibt es immer wieder Daten, die zusätzlich nachgetragen werden und  von den gewöhnlichen top-Level Attributen wie Telefonnummer, Adresse, Email abweichen. Anderen Datenbanken können auch nicht auflösen, wie Profile

There's always new data to add to the user's profile, from the usual  top-level stuff (phone, address, email, and so on) to information a  layer below (such as phone type). Other database types haven't evolved  fast enough to capture the hundred ways we contact each other or the  dozens of ways we pay for things.







 **2. Product/catalog data**

Dokumentorientiere DAtenbanken komen auch dann zum Einssatz, wenn es darum geht komplizierte Produkinformatioen abzubnilden. Bestehen Produkte zum Beispiel aus anderen Produkten oder gibt es mehrere Hersteller. Informationen, die Informationen enthalten usw lassen sich optimal mit Document Stores abbilden.

"Way back when, I  worked for a cellphone manufacturer (or two) and later a chemical  company. Each had a weird version of the same problem: Products were  composed of other products, and which products those were composed of  changed over time and tended to have more than one brand or identifier.  Capturing the thing that contains the thing that contains the thing is  much simpler in a document database than in some other database types."

 **3. Geospatial data**

MongoDB beispielsweise hat eigene spezifische peospatial Features. Diese können zum Einsatz kommen, wenn man die Distanz einer Bike Tour oder geospezifische Information über den Kunden benötigt.

This isn't necessarily because MongoDB is a great document database, but because it has [specific geospatial features](http://www.infoworld.com/d/application-development/use-mongodb-make-your-app-location-aware-229403).  Either way, MongoDB is your friend, whether you're calculating your  bike ride distance or figuring out geospecific information about your  customers.

**4. Talk**

Domentsores leisten gute Arbeit, wenn es darum geht massive Mengen an Daten über Gesprächsverlaufe auf sozialen Kanälen abzuspeichern

People are social creatures, and over  the last decade or so we've generated exabytes of social data. Mongo is a  fine choice to handle the load. Often, people talk topically, with a  lot of associated metadata. MongoDB is good for storing that too.



 **8. Games**

In Spielen ermglicht es, mutilleel data zu speichern. Zum bsiepiel verscheidene Arten von Währungen, Ziele, die aus multiplen Objekten bestehen

You have to water those flowers or  serve those restaurant patrons or grow your vegetables or kill zombies  or whatever. Games have goals, which consist of multiple objectives  obtained through achievement or paying your way out. Whether it's a  titanium rake or a BFG 9000, MongoDB can handle the concurrency and save  the (often multilevel) data.



Zusammenfassend lässt sich sagen, kommen Document Stores häufig dann zum Einsatz, wenn Objekte sich in mehrere Objekte schachteln und die Objekte wiederum nicht nach einem strengen Gerüst mit Attributen aufgebaut sind, oder häufigen Änderungen unterliegen.

## Quellen

[1 onlinequelle ]

[2 whitepaper MongoDB - Top 5 Considerations When Evaluating NoSQL Databases]

[3 Oska09 http://blog.sym-link.com/2009/05/12nosql_2009.html] 

[4 Edlich - NoSQL - ein Einstieg in die …]

[5 Online Quelle: https://db-engines.com/en/ranking/document+store]

[https://www.innoq.com/en/articles/2011/01/nosql-einsatzgebiete/]

[https://www.mongodb.com/scale/internet-of-things-applications]

[https://www.infoworld.com/article/2612785/application-development/10-common-tasks-for-mongodb.html]


