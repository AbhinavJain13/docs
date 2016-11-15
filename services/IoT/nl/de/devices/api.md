---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# HTTP-REST-API für Geräte
{: #api}
Letzte Aktualisierung: 11. Oktober 2016
{: .last-updated}

**Wichtig:** Die {{site.data.keyword.iot_full}}-Funktion 'HTTP-REST-API für Geräte' steht nur als Bestandteil des eingeschränkten Beta-Programms zur Verfügung. Zukünftige Aktualisierungen enthalten möglicherweise Änderungen, die mit der aktuellen Version dieser Funktion nicht kompatibel sind. Starten Sie einen Versuch und [senden Sie uns Ihren Erfahrungsbericht](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html).

## Zugriff auf HTTP-REST-API
{: #api_link}

Für den Zugriff auf die {{site.data.keyword.iot_short_notm}}-HTTP-REST-API und zum Abrufen weiterer Informationen zur Vorgehensweise bei der Integration von Geräten in Ihre Organisation rufen Sie die Webadresse 'https://docs.internetofthings.ibmcloud.com/swagger/v0002.html' auf.

Die einzige unterstützte {{site.data.keyword.iot_short_notm}}-HTTP-REST-API ist Version 2. Stellen Sie sicher, dass Ihre {{site.data.keyword.iot_short_notm}}-Lösungen Version 2 verwenden.

# HTTP-REST-Messaging-API für Geräte
{: #rest_messaging_api}

## Ereignisse publizieren
{: #event_publication}

Zusätzlich zum MQTT-Nachrichtenprotokoll können Sie Ihre Geräte auch so konfigurieren, dass Ereignisse in {{site.data.keyword.iot_short_notm}} über HTTP mithilfe von HTTP-REST-API-Befehlen publiziert werden.

Verwenden Sie eine der folgenden URLs, um eine `POST`-Anforderung von einem Gerät zu übergeben, das mit {{site.data.keyword.iot_short_notm}} verbunden ist:

### Nicht sichere POST-Anforderung
<pre class="pre">http://<var class="keyword varname">Organisations-ID</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">Typ-ID</var>/devices/<var class="keyword varname">Geräte-ID</var>/events/<var class="keyword varname">Ereignis-ID</var></pre>
{: codeblock}

### Sichere POST-Anforderung
<pre class="pre">https://<var class="keyword varname">Organisations-ID</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">Typ-ID</var>/devices/<var class="keyword varname">Geräte-ID</var>/events/<var class="keyword varname">Ereignis-ID</var></pre>
{: codeblock}

Wenn Sie eine Verbindung zwischen einem Gerät oder einer Anwendung und dem Quickstart-Service herstellen, verwenden Sie stattdessen eine der folgenden URLs:

### Nicht sichere POST-Anforderung an Quickstart
<pre class="pre">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">Typ-ID</var>/devices/<var class="keyword varname">Geräte-ID</var>/events/<var class="keyword varname">Ereignis-ID</var></pre>
{: codeblock}

### Sichere POST-Anforderung an Quickstart
<pre class="pre">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">Typ-ID</var>/devices/<var class="keyword varname">Geräte-ID</var>/events/<var class="keyword varname">Ereignis-ID</var></pre>
{: codeblock}

**Wichtige Hinweise:**
- In der aktuellen Version der HTTP-REST-API können Sie Geräteereignisse nur mithilfe der HTTP-Nachrichtenübertragung übergeben. Verwenden Sie das MQTT-Nachrichtenprotokoll, um Anforderungen nach anderen Gerätemanagement- und Steuerfunktionen zu übergeben.
- HTTP-Verbindungen können nur wiederverwendet werden, um Ereignisse für dasselbe Gerät zu publizieren, da der HTTP-Header für die Berechtigung nicht geändert werden kann.

### Authentifizierung

Alle Anforderungen müssen einen Berechtigungsheader enthalten. Die Basisauthentifizierung ist die einzige Methode, die unterstützt ist. Wenn ein Gerät eine HTTP-Anforderung über die {{site.data.keyword.iot_short_notm}}-HTTP-REST-API übergibt, sind folgende Berechtigungsnachweise erforderlich:

|Berechtigungsnachweis|Erforderliche Eingabe|
|:---|:---|
|Benutzername|`use-token-auth`
|Kennwort| Das Authentifizierungstoken, das beim Registrieren des Geräts entweder automatisch generiert oder manuell angegeben wurde.


### Anforderungsheader des Typs 'Content-Type'

Zusammen mit der Anforderung muss ein Anforderungsheader des Typs `Content-Type` ('Inhaltstyp') angegeben werden. Die folgende Tabelle zeigt die Zuordnung der unterstützten Typen zu den internen {{site.data.keyword.iot_short_notm}}-Formaten.

|Header des Typs 'Content-Type'|Format in {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

### Servicequalität

Ähnlich der Servicestufe 0 der MQTT-Servicequalität (Zustellung höchstens einmal) bietet das HTTP-REST-Messaging die Zustellung nicht persistenter Nachrichten, prüft aber, ob die Anforderung richtig ist und an den Server gesendet werden kann, bevor es die HTTP-Antwort sendet. Durch eine Antwort, die den HTTP-Statuscode 200 enthält, wird bestätigt, dass die Nachricht an den Server übermittelt wurde. Wenn Sie entweder die MQTT-Servicequalitätsstufe 'höchstens einmal' oder das HTTP-Äquivalent zum Zustellen von Ereignisnachrichten verwenden, muss das Gerät oder die Anwendung Wiederholungslogik implementieren, damit die Zustellung garantiert ist.

Weitere Informationen zum MQTT-Protokoll und den Servicequalitätsstufen für {{site.data.keyword.iot_short_notm}} finden Sie in [MQTT-Messaging](../reference/mqtt/index.html).


<--!
Wurde vom veralteten Abschnitt für die Featureentwicklung verschoben. Position muss mit Entwicklung besprochen werden.
## Cache für zuletzt gemeldete Ereignisse
{: #last-event-cache}

Durch Verwendung der {{site.data.keyword.iot_short_notm}}-API für zuletzt gemeldete Ereignisse können Sie das zuletzt von einem Gerät gesendete Ereignis abrufen. Dies funktioniert unabhängig davon, ob das Gerät online oder offline ist, wodurch Sie den Gerätestatus unabhängig vom physischen Standort des Geräts oder dem Status seiner Verwendung abrufen können. Sie können den zuletzt aufgezeichneten Wert einer Ereignis-ID für ein bestimmtes Gerät oder den zuletzt aufgezeichneten Wert für alle Ereignis-IDs abrufen, die von einem bestimmten Gerät gemeldet wurden. Daten zum letzten Ereignis eines Geräts können für jedes Ereignis abgerufen werden, das nicht später als 365 Tage zurückliegt.

Zum Abfragen des letzten aktuellen Werts für eine bestimmte Ereignis-ID verwenden Sie die folgende API-Anforderung, die den zuletzt aufgezeichneten Wert für die Ereignis-ID 'power' (Spannung) zurückgibt.

```
GET /api/v0002/device/types/<Gerätetyp>/devices/<Geräte-ID>/events/power
```

Die Antwort wird im folgenden JSON-Format zurückgegeben:

```
{
    "deviceId": "<Geräte-ID>",
    "eventId": "power",
    "format": "json",
    "payload": "eyJzdGF0ZSI6Im9uIn0=",
    "timestamp": "2016-03-14T14:12:06.527+0000",
    "typeId": "<Gerätetyp>"
}
```

**Hinweis:** Auch wenn die API-Antwort das Format JSON hat, können Ereignisnutzdaten in einem beliebigen anderen Format geschrieben werden. Nutzdaten, die von der API für zuletzt gemeldete Ereignisse zurückgegeben werden, haben die Base64-Codierung.

Zum Abfragen des letzten aktuellen Werts für die einzelnen Ereignis-IDs, die von einem Gerät gemeldet wurden, verwenden Sie folgende API-Anforderung:

```
GET /api/v0002/device/types/<Gerätetyp>/devices/<Geräte-ID>/events
```

Die Antwort enthält alle Ereignis-IDs, die vom Gerät gesendet wurden. Im folgenden Beispiel werden Werte für die Ereignisse 'power' (Spannung) und 'temperature' (Temperatur) zurückgegeben.

```
[
    {
        "deviceId": "<Geräte-ID>",
        "eventId": "power",
        "format": "json",
        "payload": "eyJzdGF0ZSI6Im9uIn0=",
        "timestamp": "2016-03-14T14:12:06.527+0000",
        "typeId": "<Gerätetyp>"
    },
    {
        "deviceId": "<Geräte-ID>",
        "eventId": "temperature",
        "format": "json",
        "payload": "eyJpbnRlcm5hbCI6MjIsICJleHRlcm5hbCI6MTZ9",
        "timestamp": "2016-03-14T14:17:44.891+0000",
        "typeId": "<Gerätetyp>"
    }
]
```
-->
