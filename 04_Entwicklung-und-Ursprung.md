# 2. Entwicklung und Ursprung

Erstaunlicherwesie begann die Geschichte der NoSQL-Datenbank Systeme durchaus schon parallel zu der der relationalen Datenbank Systemen. Bereits 1979 entwickelte Ken Thompson eine Key/Hash-Datenbank namens DBM. Aber erst 1998 tauchte der Begriff NoSQL zum ersten Mal bei einer Datenbank von Carlo Strozzi auf. Seiner Datenbank lag zwar immer noch ein relationales Datenbankmodell zugrunde, er stellte aber keine SQL-API zur Verfügung.

Der eigentliche Schub für NoSQL kam aber erst ab 2000 mit der Einführung des Web 2.0 und dem Versuch, auch große Datenmengen zu verarbeiten. Google kann man mit seinem BigTable-Datenbanksystem (2004) als den NoSQL-Vorreiter schlechthin betrachten. Später zogen Firmen wie Yahoo, Amazon und später bald auch alle sozialen Netzwerke wie MySpace, Facebook, LinkedIn usw. nach. 

Bis 2005 entstanden einige im Vergleich kleinere hochinteressante Datenbanken, die in vielen Facetten schon NoSQL-Charakter aufwiesen. (wie zB. Graphendatenbanken, objektorientierte Datenbanken) [2 whitepaper MongoDB]

Von 2006 bis 2009 entstanden dann die heutigen klassischen NoSQL-Systeme. Doch erst 2009 tauchte der heutige Begriff "NoSQL" in einem Weblog von Eric Evans zum ersten Mal auf [3 Oska09].  

Um den Bogen zurück zu  Document Stores zu spannen, ist man allgemein der Auffassung, dass der Bereich der dokumentenorientierten Datenbanken zu den interessantesten Teilen der NoSQL-Bewegung gehört. [4 NoSQL - ein Einstieg in die …]

Jedoch muss man mit dem Begriff  “Document Stores” vorsichtig sein. Sie sind im eigentlichen Sinne keine echten Dokumentendatenbanken. Der Begriff selbst stammt noch aus der Zeit von Lotus Notes, wo tatsächlich echte Anwenderdokumente gespeichert wurden. Wahrscheinlich wurde der Begriff sogar vom ehemaligen Lotus Notes-Entwickler Damien Katz geprägt, der später für CouchDB arbeitete.

Jedoch ist die Anzahl der wirklich relevanten dokumentenorientierten Datenbanken relativ gering. Neben MongoDB haben noch Couchbase und CouchDB eine große Bedeutung [5 Online Quelle: https://db-engines.com/en/ranking/document+store]

## 2.1 Geschwister von Document Stores

Document Stores gehören zweifelsohne zu den wichtigsten NoSQL Datenbanken. Andere wichtige No-SQL Datenbanken sind

-  **Schlüssel/Wert-orientiert (engl. Key/Value):** 

  Abgefragt wird auf den Schlüssel, der einen beliebigen String (z. B. XML oder ein serialisiertes Objekt) zurückliefert.

-  **Spaltenorientiert:** 

   Dieser Speichertyp greift über einen Schlüssel gezielt auf Einzelwerte einer Struktur (Spaltenfamilie) zu.

-  **Graphenorientiert:** 

  Entscheidender Anwendungsfall ist das Traversieren der Objekte, wie z. B. bei Verbindungen in Social Networks oder Produktempfehlungen. Die Daten werden in Knoten (Entitäten) und Kanten (Beziehungen) aufgeteilt, welche mit Attributen versehen werden können.


<hr>
[< Einleitung](03_introduction.md)		|   [Datenmodell >](05_Datenmodell.md)