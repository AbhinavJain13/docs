---

copyright:
  years: 2016
lastupdated: "2016-09-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 概説 (ベータ)


{{site.data.keyword.openwhisk}} は、サーバーレス・コンピューティングまたは Function as a Service (FaaS) とも呼ばれる分散イベント・ドリブン計算サービスです。{{site.data.keyword.openwhisk_short}} は、イベントに応えて、または、Web アプリやモバイル・アプリからの HTTP を介した直接起動に応えて、アプリケーション・ロジックを実行します。イベントは、Bluemix サービス (Cloudant など) および外部ソースから提供できます。開発者は、アプリケーション・ロジックの開発と、オンデマンドで実行されるアクションの作成に専念できます。アクションの実行率は常にイベント率に一致するため、本来の拡張性と回復力に応じたものになり、最適な使用効率をもたらします。使用した分のみ支払えばよく、サーバーを管理する必要はありません。[ソース・コード](https://github.com/openwhisk/openwhisk)を入手し、システムを自身で実行することもできます。
{: shortdesc}

{{site.data.keyword.openwhisk_short}} の動作について詳しくは、『[{{site.data.keyword.openwhisk_short}} 概要](./openwhisk_about.html)』を参照してください。

ブラウザーおよび CLI を使用して、{{site.data.keyword.openwhisk_short}} アプリケーションを開発できます。
この 2 つには、類似したアプリケーション開発機能がありますが、CLI では、デプロイメントおよび操作をより詳細に制御できます。


## ブラウザーで開発
{: #openwhisk_start_editor}

[ブラウザー](https://console.{DomainName}/openwhisk/editor){: new_window}で {{site.data.keyword.openwhisk_short}} を試して、アクションの作成、トリガーを使用したアクションの自動化、パブリック・パッケージの探索を行ってください。
OpenWhisk ユーザー・インターフェースのクイック・ツアーについては、[詳細](https://console.{DomainName}/openwhisk/learn){: new_window}ページを参照してください。

## {{site.data.keyword.openwhisk_short}} CLI のセットアップ
{: #openwhisk_start_configure_cli}

{{site.data.keyword.openwhisk_short}} コマンド・ライン・インターフェース (CLI) を使用して、名前空間および許可鍵をセットアップできます。[「CLI の構成」](https://new-console.{DomainName}/openwhisk/cli){: new_window}に移動し、手順に従ってインストールしてください。

### HTTPS プロキシーを使用するための CLI の構成
{: #openwhisk_configure_https_proxy_cli}

HTTPS プロキシーを使用するように CLI をセットアップできます。HTTPS プロキシーをセットアップするには、`HTTPS_PROXY` という名前の環境変数を作成する必要があります。この変数をフォーマット `{PROXY IP}:{PROXY PORT}` を使用して HTTPS プロキシーのアドレスとそのポートに設定する必要があります。

{{site.data.keyword.openwhisk_short}} を CLI と共にセットアップした後、コマンド・ラインから使用を開始できます。

## {{site.data.keyword.openwhisk_short}} CLI の使用 
{: #openwhisk_start_using_cli}

[環境を構成](https://new-console.{DomainName}/openwhisk/cli){: new_window}した後、{{site.data.keyword.openwhisk_short}} CLI の使用を開始して以下を実行することができます。

* 自身のコード・スニペット (アクション) を {{site.data.keyword.openwhisk_short}} で実行します。『[アクションの作成と起動](./openwhisk_actions.html)』を参照してください。
* トリガーおよびルールを使用して、アクションがイベントに対応できるようにします。『[トリガーおよびルールの作成](./openwhisk_triggers_rules.html)』を参照してください。
* パッケージがアクションをどのようにバンドルし、外部イベント・ソースを構成するのかを学習します。『[パッケージの使用と作成](./openwhisk_packages.html)』を参照してください。
* パッケージ・カタログを検討し、[Cloudant イベント・ソース](./openwhisk_catalog.html#openwhisk_catalog_cloudant)などの外部サービスでアプリケーションを強化します。『[{{site.data.keyword.openwhisk_short}} 対応サービスの使用](./openwhisk_catalog.html)』を参照してください。


## iOS アプリからの {{site.data.keyword.openwhisk_short}} の使用
{: #openwhisk_start_using_ios}

{{site.data.keyword.openwhisk_short}} iOS SDK を使用することによって、{{site.data.keyword.openwhisk_short}} を iOS モバイル・アプリまたは Apple Watch から使用できます。詳しくは、[iOS 資料](./openwhisk_mobile_sdk.html)を参照してください。

## {{site.data.keyword.openwhisk_short}} と REST API の使用
{: #openwhisk_start_using_restapi}

{{site.data.keyword.openwhisk_short}} 環境が有効になった後、{{site.data.keyword.openwhisk_short}} を、REST API 呼び出しを使用して Web アプリまたはモバイル・アプリと共に使用できます。アクション、アクティベーション、パッケージ、ルール、およびトリガー用の API について詳しくは、[{{site.data.keyword.openwhisk_short}} API 資料](https://new-console.{DomainName}/apidocs/98)を参照してください。

## {{site.data.keyword.openwhisk_short}} Hello World 例
{: #openwhisk_start_hello_world}
{{site.data.keyword.openwhisk_short}} の入門として、まず次の JavaScript コード例を試してみてください。

```
/**
 * Hello world as an OpenWhisk action.
 */
function main(params) {
    var name = params.name || 'World';
    return {payload:  'Hello, ' + name + '!'};
}
```
{: codeblock}

この例を使用するには、以下の手順を実行してください。

1. コードをファイルに保存します。例えば、*hello.js* などです。

2. {{site.data.keyword.openwhisk_short}} CLI コマンド・ラインから、次のコマンドを入力してアクションを作成します。

    ```
    wsk action create hello hello.js
    ```
    {: pre}

3. 次に、以下のコマンドを入力することによって、アクションを起動します。

    ```
    wsk action invoke hello --blocking --result
    ```
    {: pre}  

    このコマンドの出力は以下のとおりです。

    ```
    {
        "payload": "Hello, World!"
    }
    ```
    {: screen}

    ```
    wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    このコマンドの出力は以下のとおりです。

    ```
    {
        "payload": "Hello, Fred!"
    }
    ```
    {: screen}

{{site.data.keyword.openwhisk_short}} のイベント・ドリブン機能を使用して、イベントに応えてこのアクションを起動することもできます。[アラーム・サービス例](./openwhisk_packages.html#openwhisk_packages_trigger)に従って、周期的イベントが生成されるたびに `hello` アクションを起動するイベント・ソースを構成します。


## システムの詳細
{: #openwhisk_system_details}

{{site.data.keyword.openwhisk_short}} に関する追加情報が以下のトピックに記載されています。

* [エンティティー名](./openwhisk_reference.html#openwhisk_entities)
* [アクションの意味](./openwhisk_reference.html#openwhisk_semantics)
* [制限](./openwhisk_reference.html#openwhisk_syslimits)
* [REST API](https://new-console.{DomainName}/apidocs/98)

# 関連リンク
{: #rellinks}

## API リファレンス
{: #api}
* [REST API の資料](./openwhisk_reference.html#openwhisk_ref_restapi)
* [REST API](https://new-console.{DomainName}/apidocs/98){:new_window}

## 関連リンク
{: #general}
* [ディスカバー: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [IBM developerWorks の {{site.data.keyword.openwhisk_short}}](https://developer.ibm.com/openwhisk/){:new_window}
