# 3. Datenmodell

Bei dokumentenorientierten Datenbanken werden Daten in Form von Dokumenten gespeichert. Gemeint sind hier aber nicht Word- oder Textdateien, sondern strukturierte Datensammlungen wie JSON oder XML-Dokumente, beides bei Entwicklern beliebtes Format. Document Stores legen z.B. JSON-Dateien zusammen mit einer ID ab. Meist legt die Datenbank nur fest, auf welches Format die ID weist. Mehr aber auch nicht. [1]

Die Strukturierung in Dokumenten bieten eine intuitive und natürliche Möglichkeit, Daten zu modellieren, die eng mit der objektorientierten Programmierung verbunden sind - jedes Dokument ist praktisch ein Objekt. Dokumente enthalten ein oder mehrere Felder, wobei jedes Feld einen typisierten Wert enthält, wie z.B. Zeichenkette, Datum, Binärwert, Dezimalwert oder Array. Anstatt einen Datensatz über mehrere Spalten und Tabellen zu verteilen, die mit Fremdschlüsseln verbunden sind, werden jeder Datensatz und seine zugehörigen (d.h. verwandten) Daten typischerweise zusammen in einem einzigen, hierarchischen Dokument gespeichert. Dieses Modell beschleunigt die Produktivität der Entwickler, vereinfacht den Datenzugriff und erübrigt in vielen Fällen aufwendige JOIN-Operationen und komplexe Transaktionen mit mehreren Datensätzen. [2]

Wie bereits erwähnt sind dokumentenorientierte Datenbanken schemafrei, wobei das Schema als dynamisch angesehen werden kann: Jedes Dokument kann verschiedene Felder enthalten. Diese Flexibilität kann besonders bei der Modellierung unstrukturierter und polymorpher Daten hilfreich sein. Das Schema wird in diesem Sinne mit Einfügen eines Dokuments zur Laufzeit erzeugt. Dies erleichtert die Entwicklung einer Anwendung während ihres Lebenszyklus, beispielsweise das Hinzufügen neuer Felder. Darüber hinaus bieten einige dokumentenorientierte Datenbanken Query-Ausdrücke, die Entwickler von relationalen Datenbanken gewohnt sind. Insbesondere können Daten, basierend auf einer beliebigen Kombination von Feldern, in einem Dokument abgefragt werden, wobei umfangreiche Sekundärindizes effiziente Zugriffspfade bieten, die nahezu jedes Abfragemuster unterstützen. [2]

------

[1] Edlich, S. (2011). *NoSQL: Einstieg in die Welt nichtrelationaler Web 2.0 Datenbanken*. München: Hanser.

[2] whitepaper MongoDB - Top 5 Considerations When Evaluating NoSQL Databases



------

[< Entwicklung und Ursprung](04_Entwicklung-und-Ursprung.md)		|   [Vergleich mit anderen Datenbankmodellen >](06_Vergleich-mit-anderen-Datenbankmodellen.md)