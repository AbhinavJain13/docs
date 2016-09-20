---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Benutzerdefinierte Domäne für {{site.data.keyword.mobilefoundation_short}}-Server konfigurieren
{: #configcustomdomain}

Letzte Aktualisierung: 08. August 2016
{: .last-updated}

{{site.data.keyword.mobilefoundation_short}} stellt einen {{site.data.keyword.mfserver_short_notm}} bereit, auf den über eine <!--on {{site.data.keyword.containerlong}} as a container group. The container group will be mapped to--> URL zugegriffen werden kann, bei der die Domänennamen auf der {{site.data.keyword.Bluemix_notm}}-**Region** basieren. Sie können auch eine eigene benutzerdefinierte Domäne erstellen.
{:shortdesc}

Bei der Erstellung der <!--container group is created with a--> URL oder Route basieren die Standarddomänennamen auf der {{site.data.keyword.Bluemix_notm}}-`Region`.

*Tabelle 1. Anwendungsdomänennamen auf der Basis der `Region` in  {{site.data.keyword.Bluemix_notm}}*

  |Domäne |  Region  |    
  |:----- | :----- |    
  |`mybluemix.net` | US - Süden |    
  |`eu-gb.mybluemix.net` | Vereinigtes Königreich  |
  |`au-syd.mybluemix.net` | Sydney  |      

Zur Verwendung einer eigenen Domäne müssen Sie eine benutzerdefinierte Domäne konfigurieren, indem Sie die folgenden Schritte ausführen:

1.	Erstellen Sie eine {{site.data.keyword.mfserver_short_notm}}-Instanz, indem Sie die {{site.data.keyword.mobilefoundation_short}}-Serviceinstanz durch die Auswahl eines unterstützten Plans erstellen.

+ Fügen Sie die benutzerdefinierte Domäne, die Sie verwenden möchten, zu Ihrer {{site.data.keyword.Bluemix_notm}}-`Organisation` hinzu. Rufen Sie **Organisationen verwalten > Domänen > Domäne hinzufügen** auf, um eine eigene Domäne hinzuzufügen.

+ Legen Sie eine Route für die Verwendung der benutzerdefinierten Domäne durch den <!--container group--> Server fest.

+ Rufen Sie den DNS-Provider für Ihre Domäne auf und fügen Sie einen CNAME-Eintrag hinzu, der den Datenverkehr von Ihrer Domäne zur {{site.data.keyword.Bluemix_notm}}-Standardroute weiterleitet, unter der der <!--container group--> Server ausgeführt wird.

+ Wenn Sie für Ihre benutzerdefinierte Domäne `https` konfigurieren möchten, laden Sie das SSL-Zertifikat für Ihre Domäne in {{site.data.keyword.Bluemix_notm}} hoch. Rufen Sie hierzu **Organisationen verwalten > Domänen** auf, wählen Sie die benutzerdefinierte Domäne aus, für die das SSL-Zertifikat konfiguriert werden soll, und klicken Sie auf **Zertifikat hochladen**, um das SSL-Zertifikat für Ihre Domäne hochzuladen. Weitere Informationen finden Sie in [SSL-Zertifikate und benutzerdefinierte Bluemix-Domänen](https://developer.ibm.com/bluemix/2014/09/28/ssl-certificates-bluemix-custom-domains/).
