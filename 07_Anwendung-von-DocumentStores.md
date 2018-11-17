# 5. Anwendung von Document-Stores

Im Folgenden sind Beispiele aufgeführt, bei denen Document-Stores zur Anwendung kommen.

## 5.1 Benutzerprofile

Ein Benutzerprofil hat meist eine Reihe von Attributen, jedoch kann die Menge der vorhandenen Attribute von Benutzer zu Benutzer variieren (z.B. werden einige Benutzer das Geburtsdatum nicht zur Verfügung stellen, wo einige Benutzer möglicherweise keine politische Zugehörigkeit offenbaren, usw.).
Benutzer in Twitter werden dann z.B. in einer dokumentenorientierten Datenbank gespeichert, in der jedes Dokument das Profil und einige aktuelle Tweets der entsprechenden Benutzer enthält.  [1]



## 5.2 Produkt/Katalog Daten

Dokumentorientiere Datenbanken kommen auch dann zum Einsatz, wenn es darum geht komplizierte Produktinformationen abzubilden. Bestehen Produkte zum Beispiel wiederum aus Produkten und gibt es zusätzlich noch mehrere Hersteller, oder andere individuelle Attribute, die nicht bei jedem Produkt zu finden sind, lässt sich die gesammelte Information am besten in Document-Stores abspeichern. [1]



## 5.3 Geoinformationsdaten

Geoinformationsdaten liefern Informationen zu einem Standort in Form von Werten der Latitude und Longitude. MongoDB beispielsweise hat eigene spezifische Geoinformationsfeatures. Diese können zum Einsatz kommen, wenn z.B. die Distanz einer Bike Tour abgerufen oder gespeichert werden soll. [1]



## 5.4 Speichern von Gesprächsverläufen

In den letzten zehn Jahren werden Exabyte an sozialen Daten generiert. Document-Stores leisten gute Arbeit, wenn es darum geht, massive Datenmengen von Gesprächsverläufen auf sozialen Kanälen oder ähnlichem abzuspeichern und diese Last zu bewältigen. [1]



## 5.5 IoT

Im Bereich von IoT (Internet of Things), bezieht sich die Anwendung nicht direkt auf dokumentorientierte Datenbanken, sondern allgemeiner auf NoSQL Datenbanken, die im Bereich IoT, aufgrund von Performance und Kostengründen, hohe Beliebtheit erfahren. IoT-Applikationen sind darauf angewiesen, Prozesse mit großen Daten Volumen durchzuführen. Dies erfordert eine schnelle und kostengünstige Skalierbarkeit und ist somit nur mit neuen BigData Technologien wie MongoDB durchzuführen. [2]


## 5.6 Zusammenfassung
Das Paradigma der Document-Stores passt somit auf Anwendungsbereiche, bei denen ein relationales Schema die Flexibilität der Anwendung einschränkt. [3]
Sie kommen häufig dann zum Einsatz, wenn Objekte sich in mehrere Objekte schachteln und die Objekte wiederum nicht nach einem strengen Gerüst mit Attributen aufgebaut sind, häufigen Änderungen unterliegen und die Datenmenge enorm ist. Außerdem werden sie angewendet, wenn verteiltes Arbeiten mit großen bis sehr großen Datenmengen erforderlich ist und bieten diesem Einsatzzweck entsprechende Datenstrukturen und verzichten bewusst auf Transaktionen. [1]

------

[1] https://www.infoworld.com/article/2612785/application-development/10-common-tasks-for-mongodb.html

[2] MongoDB Paper - Why NoSQL Databases for the Internet of Things: Machina Research

[3] Edlich, S. (2011). *NoSQL: Einstieg in die Welt nichtrelationaler Web 2.0 Datenbanken*. München: Hanser.

------

[< Vergleich mit anderen Datenbankmodellen](06_Vergleich-mit-anderen Datenbankmodellen.md)		|   [Übersicht wichtiger dokumentorientierter Datenbanken >](08_Übersicht-wichtiger-dokumentorientierter-Datenbanken.md)