---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API REST HTTP para dispositivos
{: #api}

**Importante:** o recurso API (interface de programação de aplicativos) REST HTTP (Protocolo de Transporte de Hipertexto) do {{site.data.keyword.iot_full}} para dispositivos está disponível apenas como parte de um programa beta limitado. Atualizações futuras podem incluir mudanças incompatíveis com a versão atual desse recurso. Experimente e [informe-nos o que acha](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html).

## Acessando a API REST HTTP
{: #api_link}

Para acessar a API (interface de programação de aplicativos) REST HTTP (Protocolo de Transporte de Hipertexto) do {{site.data.keyword.iot_short_notm}} e obter mais informações sobre como integrar dispositivos à sua organização, acesse https://docs.internetofthings.ibmcloud.com/swagger/v0002.html.

A única versão da API (interface de programação de aplicativos) REST HTTP (Protocolo de Transporte de Hipertexto) do {{site.data.keyword.iot_short_notm}} suportada é a versão 2. Assegure que suas soluções {{site.data.keyword.iot_short_notm}} estejam usando a versão 2.

# API (interface de programação de aplicativos) do sistema de mensagens REST HTTP (Protocolo de Transporte de Hipertexto) para dispositivos
{: #rest_messaging_api}

## Publicando eventos
{: #event_publication}

Além de usar o protocolo de sistema de mensagens MQTT, também é possível configurar seus dispositivos para publicar eventos no {{site.data.keyword.iot_short_notm}} por HTTP (Protocolo de Transporte de Hipertexto) usando comandos da API (interface de programação de aplicativos) REST HTTP (Protocolo de Transporte de Hipertexto).

Use uma das URLs (Localizadores Uniformes de Recursos) a seguir para enviar uma solicitação de `POST` de um dispositivo que está conectado ao {{site.data.keyword.iot_short_notm}}:

### Solicitação de POST não segura
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Solicitação de POST segura
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

Se você estiver conectando um dispositivo ou um aplicativo ao serviço de iniciação rápida, use uma das URLs (Localizadores Uniformes de Recursos) a seguir em seu lugar:

### Solicitação de POST não segura para iniciação rápida
<pre class="pre">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Solicitação de POST segura para iniciação rápida
<pre class="pre">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**Notas importantes:**
- Na versão atual da API (interface de programação de aplicativos) REST HTTP (Protocolo de Transporte de Hipertexto), é possível enviar eventos de dispositivos apenas usando o sistema de mensagens HTTP. Use o protocolo de sistema de mensagens MQTT para enviar solicitações para outros recursos de gerenciamento de dispositivo e controle.
- Conexões HTTP (Protocolo de Transporte de Hipertexto) podem ser reutilizadas para publicar eventos para o mesmo dispositivo apenas, pois o cabeçalho HTTP de autorização não pode ser mudado.

### Authentication

Todas as solicitações devem incluir um cabeçalho de autorização. Autenticação Básica é o único método suportado. Quando um dispositivo faz qualquer solicitação de HTTP (Protocolo de Transporte de Hipertexto) por meio da API (interface de programação de aplicativos) REST HTTP (Protocolo de Transporte de Hipertexto) do {{site.data.keyword.iot_short_notm}}, as credenciais a seguir são necessárias:

|Credencial|Entrada requerida|
|:---|:---|
|User name|`use-token-auth`
|Password| O token de autenticação que foi gerado automaticamente ou manualmente especificado quando você registrou o dispositivo.


### Cabeçalhos de solicitação Content-Type

Um cabeçalho de solicitação `Content-Type` deve ser fornecido com a solicitação. A tabela a seguir mostra como os tipos suportados são mapeados para os formatos internos do{{site.data.keyword.iot_short_notm}}.

|cabeçalho Content-Type|Formato no {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|texto/simples|"texto"
|aplicativo/json| "json"
|aplicativo/xml | "xml"
|application/octet-stream|"bin"

### Qualidade de Serviço

Semelhante ao nível 0 de serviço de entrega de qualidade de serviço MQTT "no máximo uma vez", o sistema de mensagens REST HTTP (Protocolo de Transporte de Hipertexto) fornece entrega de mensagem não persistente, mas valida se a solicitação está correta e se pode ser entregue ao servidor antes de enviar a resposta HTTP. Uma resposta que contém um código de status HTTP (Protocolo de Transporte de Hipertexto) 200 confirma que a mensagem foi entregue ao servidor. Ao usar o nível de qualidade de serviço MQTT "no máximo uma vez" ou o equivalente de HTTP (Protocolo de Transporte de Hipertexto) para entregar mensagens de eventos, o dispositivo ou o aplicativo deve implementar a lógica de nova tentativa para garantir a entrega.

Para obter mais informações sobre o protocolo MQTT e os níveis de qualidade de serviço para o {{site.data.keyword.iot_short_notm}}, consulte [Sistema de mensagens MQTT](../reference/mqtt/index.html).


<--!
Movido do tópico de desenvolvedor Recursos obsoletos. Local a ser discutido com o desenvolvedor.
## Último cache de eventos
{: #last-event-cache}

Usando a API (interface de programação de aplicativos) de cache do último evento do {{site.data.keyword.iot_short_notm}}, é possível recuperar o último evento que foi enviado por um dispositivo. Isso funciona estando o dispositivo on-line ou off-line, o que permite recuperar o status do dispositivo independentemente da localização física do dispositivo ou do status de uso. É possível recuperar o último valor registrado de um ID de evento para um dispositivo específico ou o último valor registrado para cada ID do evento que foi relatado por um dispositivo específico. Os dados do último evento de um dispositivo podem ser recuperados para qualquer evento específico que tenha ocorrido há até 365 dias.

Para solicitar o valor mais recente para um ID de evento específico, use a solicitação de API a seguir, que retorna o último valor registrado para o ID do evento “energia”.

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events/power
```

A resposta é retornada no formato JSON a seguir:

```
{
    "deviceId": "<device-id>",
    "eventId": "power",
    "format": "json",
    "payload": "eyJzdGF0ZSI6Im9uIn0=",
    "timestamp": "2016-03-14T14:12:06.527+0000",
    "typeId": "<device-type>"
}
```

**Observação:** enquanto a resposta da API está no formato JSON, cargas úteis do evento podem ser gravadas em qualquer formato. Cargas úteis retornadas pela API Last Event Cache são codificadas em base64.

Para solicitar o valor mais recente para cada ID do evento que foi relatado por um dispositivo, use a solicitação de API a seguir:

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events
```

A resposta incluirá todos os IDs de evento que foram enviados pelo dispositivo. No exemplo a seguir, os valores são retornados para os eventos “energia” e “temperatura”.

```
[
    {
        "deviceId": "<device-id>",
        "eventId": "power",
        "format": "json",
        "payload": "eyJzdGF0ZSI6Im9uIn0=",
        "timestamp": "2016-03-14T14:12:06.527+0000",
        "typeId": "<device-type>"
    },
    {
        "deviceId": "<device-id>",
        "eventId": "temperature",
        "format": "json",
        "payload": "eyJpbnRlcm5hbCI6MjIsICJleHRlcm5hbCI6MTZ9",
        "timestamp": "2016-03-14T14:17:44.891+0000",
        "typeId": "<device-type>"
    }
]
```
-->
