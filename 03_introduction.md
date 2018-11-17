# Einleitung


# Entwicklung und Ursprung:

Dokumentenorientierte Datenbanken stellen die am weitesten verbreitete und beliebteste Alternative zu den klassischen relationalen Datenbanken dar. 



Sie beruhen auf keinem festen Schema, wie das bei relationalen Datenbanken der Fall ist und gehören zu der Familie der NoSQL Datenbanken. - [1 onlinequelle ]

NoSQL Datenbanken können sich jedoch recht stark unterscheiden, da ihnen unterschiedliche Datenbankmodelle zu Grunde liegen. Die Unterschied, der sich von relationene Datenbanken stark abgrenzen lässt und sie zusammenfassen lässt, liegt in der Schemafreiheit begründet. 

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

Wie bereits erwähnt sind dokumentenorientierte Datenbanken schemafrei, wobei das Schema als dynamisch angesehen werden kann: Jedes Dokument kann verschiedene Felder enthalten. Diese Flexibilität kann besonders bei der Modellierung unstrukturierter und polymorpher Daten hilfreich sein. Es erleichtert auch die Entwicklung einer Anwendung während ihres Lebenszyklus, z.B. das Hinzufügen neuer Felder. Darüber hinaus bieten einige dokumentenorientierte Datenbanken Query-Ausdrücke, die Entwickler von relationalen Datenbanken gewohnt sind. Insbesondere können Daten basierend auf einer beliebigen Kombination von Feldern in einem Dokument abgefragt werden, wobei umfangreiche Sekundärindizes effiziente Zugriffspfade bieten, die nahezu jedes Abfragemuster unterstützen.



## Anwendung von Document Stores



## Quellen

[1 onlinequelle ]

[2 whitepaper MongoDB]

[3 Oska09 http://blog.sym-link.com/2009/05/12nosql_2009.html] 

[4 NoSQL - ein Einstieg in die …]

[5 Online Quelle: https://db-engines.com/en/ranking/document+store]


