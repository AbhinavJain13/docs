---

copyright:
  years: 2016
lastupdated: "2016-09-16"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Archivierungsfunktion mithilfe von {{site.data.keyword.cloudant_short_notm}} verbinden und konfigurieren  
{: #cloudant_main}

Durch Herstellen einer Verbindung zwischen einem {{site.data.keyword.cloudantfull}}-Service und Ihrer Instanz von {{site.data.keyword.iot_full}} können Sie Ihre Gerätedaten speichern und auf sie zugreifen. Gerätedaten werden je nach dem von Ihnen gewählten Bucketintervall in Datenbanken gespeichert, die auf der Grundlage 'Tag', 'Woche' oder 'Monat' arbeiten.

Wenn Sie beginnen, {{site.data.keyword.cloudant_short_notm}} zum Speichern von Gerätedaten zu verwenden, werden automatisch drei Datenbanken erstellt: eine Datenbank für das aktuelle Bucketintervall, eine Datenbank für das kommende Intervall und eine Konfigurationsdatenbank. Der Konfigurationsdatenbank können Designdokumente hinzugefügt werden, die beim Erstellen von neuen Datenbanken in diese kopiert werden. Bei Erreichen des Intervallendes werden in der Bucketdatenbank Gerätedaten für das neue Intervall gespeichert und für das folgende Intervall wird eine neue Datenbank erstellt.

Für die Speicherung von Gerätedaten, die an eine Datenbank gesendet werden, gibt es zwei Möglichkeiten. Wenn die Daten ein gültiges JSON-Format aufweisen und als Format des Geräteereignisses `JSON` eingestellt ist, werden die Gerätedaten im folgenden Format gespeichert:

```json

{
  "_id": "78bf4380-3311-11e6-a747-d7b140d1a70a",
  "_rev": "2-d13912b7c089f060a4ba7369fa86e46f",
  "typeId": "t",
  "deviceType": "0",
  "eventType": "json_payload",
  "format": "json",
  "timestamp": "2016-06-15T16:54:41.464+01",
  "data": {
    "a": 22
  }
}

```

Wenn die Gerätedaten kein gültiges JSON-Format aufweisen oder als Format nicht `JSON` festgelegt ist, werden die Gerätedaten im Feld `payload` als Zeichenfolge mit Base64-Codierung im folgenden Format gespeichert:

```json

{
  "_id": "80f1ce10-3311-11e6-a747-d7b140d1a70a",
  "_rev": "1-bfcbf1e74389fe4188a9425c0cd2575a",
  "payload": "eHh4eHg=",
  "typeId": "t",
  "deviceType": "0",
  "eventType": "non_json_payload",
  "format": "notjson",
  "timestamp": "2016-06-15T16:54:55.217+01"
}

```

## Vorbereitende Schritte  
{: #byb}

Bitte führen Sie vor dem Herstellen einer Verbindung von {{site.data.keyword.cloudant_short_notm}} zu Ihrem {{site.data.keyword.iot_short}}-Service folgende Tasks aus:

- Richten Sie in dem Bluemix-Bereich, in dem auch {{site.data.keyword.iot_short_notm}} vorhanden ist, mithilfe des Bluemix-Katalogs eine {{site.data.keyword.cloudant_short_notm}}-Datenbank ein.

Stellen Sie sicher, dass Sie innerhalb der Bluemix-Organisation über Entwicklerberechtigungen verfügen und dass Sie über Bluemix angemeldet sind. Wenn Sie nicht über Bluemix angemeldet sind oder innerhalb dieser Bluemix-Organisation nicht über Entwicklerberechtigungen verfügen, können Sie die Bindung zwischen der {{site.data.keyword.cloudant_short_notm}}-Datenbank und der {{site.data.keyword.iot_short_notm}}-Instanz nicht berechtigen.

Führen Sie folgende Schritte aus, um für eine {{site.data.keyword.cloudant_short_notm}}-Datenbank eine Verbindung herzustellen:

1. Klicken Sie in Ihrem {{site.data.keyword.iot_short}}-Dashboard in der Navigationsleiste auf **Erweiterungen**.
2. Klicken Sie auf der Kachel 'Speicherung archivierter Daten' auf **Einrichtung**.
2. Alle verfügbaren {{site.data.keyword.cloudant_short_notm}}-Services, die sich innerhalb desselben Bluemix-Bereichs wie Ihr {{site.data.keyword.iot_short}}-Service befinden, werden im Abschnitt 'Speicherung archivierter Daten konfigurieren' aufgelistet.
3. Wählen Sie den {{site.data.keyword.cloudant_short_notm}}-Service aus, für den Sie eine Verbindung herstellen wollen.
4. Wählen Sie die Konfigurationsoptionen für {{site.data.keyword.cloudant_short_notm}} aus:

  a. Wählen Sie ein Bucketintervall aus. Mit dem Bucketintervall wird gesteuert, wie häufig neue Datenbanken für die Gerätedatenspeicherung erstellt werden. Auf der Basis des von Ihnen gewählten Bucketintervalls werden in der gewählten Zeitzone um Mitternacht neue Buckets erstellt.

  b. Wählen Sie eine Zeitzone aus. Um zu bestimmen, in welchen Bucket Gerätedaten platziert werden, wird die Zeit der ausgewählten Zeitzone verwendet, nicht die für das Gerät geltende Ortszeit. Zeitmarken für Gerätedaten, die an die {{site.data.keyword.cloudant_short_notm}}-Datenbank gesendet werden, werden bei der Entscheidung, in welche Datenbank die Daten einzugeben sind, in die ausgewählte Zeitzone konvertiert.

  c. Wählen Sie Optionen aus, mit denen der Datenbankname festgelegt wird. Der Datenbankname lautet `iotp_<Organisations-ID>_<Datenbankname>_<Bucketname>`, wobei Folgendes gilt:

 +  * `<Organisations-ID>` ist die ID Ihrer Organisation.
 +  * `<Datenbankname>` ist Ihre Auswahl für diesen Teil des Datenbanknamens, der durch das Feld für den Datenbanknamen (`Database Name`) gesteuert wird.
 +  * `<Bucketname>` ist eine Zeichenfolge, die durch Ihre Auswahl für das Feld für das Bucketintervall (`Bucket Interval`) festgelegt ist:
 +    * Für ein tägliches Bucketintervall (`day`) nimmt `<Bucketname>` den Wert `jjjj-mm-tt` an.  Beispielsweise `2016-07-06` für Ereignisse am 6. Juli 2016.
 +    * Für ein wöchentliches Bucketintervall (`week`) nimmt `<Bucketname>` den Wert `jjjj-'w'ww` an, wobei `'w'ww` die Nummer einer Woche angibt.  Beispielsweise `2016-w03` für Ereignisse in der dritten Kalenderwoche in 2016.
 +    * Für ein monatliches Bucketintervall (`month`) nimmt `<Bucketname>` den Wert `jjjj-mm` an.  Beispielsweise `2016-07` für Ereignisse im Juli 2016.

5. Klicken Sie auf **Berechtigen**.
6. Klicken Sie im Dialogfeld 'Berechtigung' auf **Bestätigen**.

Ihre Gerätedaten werden nun in Ihrer {{site.data.keyword.cloudant}}-Datenbank gespeichert.

## Neue Designdokumente erstellen  
{: #design_docs}

Neue Designdokumente, die in der Konfigurationsdatenbank enthalten sind, werden in jede erstellte Datenbank kopiert. Der Name der Konfigurationsdatenbank lautet 'iotp_<Organisations-ID>_<Auswahl>_configuration', wobei dieselben Parameter wie für die in Schritt 3b des Abschnitts 'Vorbereitende Schritte' beschriebenen Datenbanknamen verwendet werden.

Die standardmäßig in {{site.data.keyword.iot_short_notm}} enthaltenen Designdokumente implementieren neben der Zusammenfassungsfunktion Abfragen, die in der aktuellen Archivierungsfunktion zur Verfügung stehen.

Der Konfigurationsdatenbank können zusätzliche Designdokumente hinzugefügt werden, die im Zuge ihrer Erstellung in neue Datenbanken für Bucketintervalle kopiert werden. Informationen zum Hinzufügen von Designdokumenten zur Konfigurationsdatenbank finden Sie in der [Dokumentation zur Cloudant-API](https://docs.cloudant.com/document.html).

<!--  # Related links
{: #rellinks}
* [Querying your {{site.data.keyword.cloudant_short_notm}}](link) -->
