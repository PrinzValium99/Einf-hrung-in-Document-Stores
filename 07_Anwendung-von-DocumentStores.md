# 5.Anwendung von Document Stores

*CouchDB wird von seinen Entwicklern als Local-Web-Plattform gesehen und setzt auf bewährte Web-Techniken „build of the web“ auf. Das macht den ersten Einstieg und Umgang mit CouchDB einfach und rüstet die Datenbank für zukünftige Entwicklungen im Internet. CouchDB rechnet mit dem Auftreten von Fehlern in verteilten Systemen „offline by default“ und bietet Möglichkeiten zur Konflikterkennung und zum Konfliktmanagement. Anwendungen mit dieser Datenbank lassen sich auch ohne Netzzugang nutzen. CouchDB schlägt eine Brücke zwischen Anwendungen im Internet bzw. in einer Cloud und lokalen Anwendungen. Das Paradigma der Document Stores passt auf Anwendungsbereiche, bei denen ein relationales Schema die Flexibilität der Anwendung einschränkt. [edlich]*



*Häufig sind sie explizit für ein verteiltes Arbeiten mit großen bis sehr großen Datenmengen ausgelegt, bieten diesem Einsatzzweck entsprechende Datenstrukturen und verzichten bewusst auf Transaktionen.*[https://www.innoq.com/en/articles/2011/01/nosql-einsatzgebiete/]

## 5.1 IoT

NoSQL Datenbanken erfahren Beliebtheit im Bereich von IoT, aufgrund von Performance und Kostengründen. IoT Applikationen sind darauf angewiesen Prozesse mit großen Daten Volumen durchzuführen. Dies erfordert eine schnelle und kostengünstige Skalierbarkeit und ist somit nur mit neuen BigData Technologien wie MongoDB durchzuführen. [https://www.mongodb.com/scale/internet-of-things-applications]

[MongoDB Paper - Why NoSQL Databases for the Internet of Things: Machina Research]





Aus Quelle:

[https://www.infoworld.com/article/2612785/application-development/10-common-tasks-for-mongodb.html]

## 5.2 Profiles of people

In User-Profilen gibt es immer wieder Daten, die zusätzlich nachgetragen werden und  von den gewöhnlichen top-Level Attributen wie Telefonnummer, Adresse, Email abweichen. Anderen Datenbanken können auch nicht auflösen, wie Profile

There's always new data to add to the user's profile, from the usual  top-level stuff (phone, address, email, and so on) to information a  layer below (such as phone type). Other database types haven't evolved  fast enough to capture the hundred ways we contact each other or the  dozens of ways we pay for things.

## 5.3 Product/catalog data

Dokumentorientiere DAtenbanken komen auch dann zum Einssatz, wenn es darum geht komplizierte Produkinformatioen abzubnilden. Bestehen Produkte zum Beispiel aus anderen Produkten oder gibt es mehrere Hersteller. Informationen, die Informationen enthalten usw lassen sich optimal mit Document Stores abbilden.

"Way back when, I  worked for a cellphone manufacturer (or two) and later a chemical  company. Each had a weird version of the same problem: Products were  composed of other products, and which products those were composed of  changed over time and tended to have more than one brand or identifier.  Capturing the thing that contains the thing that contains the thing is  much simpler in a document database than in some other database types."

## 5.4 Geospatial data

MongoDB beispielsweise hat eigene spezifische geospatial Features. Diese können zum Einsatz kommen, wenn man die Distanz einer Bike Tour oder andere geospezifische Information über den Kunden benötigt.

This isn't necessarily because MongoDB is a great document database, but because it has [specific geospatial features](http://www.infoworld.com/d/application-development/use-mongodb-make-your-app-location-aware-229403).  Either way, MongoDB is your friend, whether you're calculating your  bike ride distance or figuring out geospecific information about your  customers.

## 5.5 Gesprächsprotkollierung

Domentsores leisten gute Arbeit, wenn es darum geht massive Mengen an Daten über Gesprächsverlaufe auf sozialen Kanälen abzuspeichern

People are social creatures, and over  the last decade or so we've generated exabytes of social data. Mongo is a  fine choice to handle the load. Often, people talk topically, with a  lot of associated metadata. MongoDB is good for storing that too.



## 5.6 Spiele
In Spielen ermglicht es, mutilleel data zu speichern. Zum bsiepiel verscheidene Arten von Währungen, Ziele, die aus multiplen Objekten bestehen.

You have to water those flowers or  serve those restaurant patrons or grow your vegetables or kill zombies  or whatever. Games have goals, which consist of multiple objectives  obtained through achievement or paying your way out. Whether it's a  titanium rake or a BFG 9000, MongoDB can handle the concurrency and save  the (often multilevel) data.


## 5.7 Zusammenfassung
Zusammenfassend lässt sich sagen, kommen Document Stores häufig dann zum Einsatz, wenn Objekte sich in mehrere Objekte schachteln und die Objekte wiederum nicht nach einem strengen Gerüst mit Attributen aufgebaut sind, oder häufigen Änderungen unterliegen.

<hr>
[< Vergleich mit anderen Datenbankmodellen](06_Vergleich-mit-anderen Datenbankmodellen.md)		|   [DAS NÄCHSTE >](07_Anwendung-von-DocumentStores.md)