---

 

copyright:

  years: 2016, 2017
lastupdated: "2017-01-04"
 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 透過 API 閘道公開動作（實驗性）
{: #openwhisk_apigateway}

在 {{site.data.keyword.openwhisk}} 中，您只能透過 **POST** 方法，使用「HTTP 要求」來呼叫使用 [REST API](./openwhisk_reference.html#openwhisk_ref_restapi) 的動作。
這需要 HTTP 用戶端使用 OpenWhisk 授權 API 金鑰來提出要求，而此金鑰是容許呼叫動作並容許刪除及建立更多動作的主要金鑰。
{: shortdesc}

此實驗性特性將可讓您使用 POST 以外的 HTTP 方法來呼叫動作，且未使用動作的授權 API 金鑰。

使用 CLI，透過「OpenWhisk API 閘道」來公開 OpenWhisk 動作。 

## OpenWhisk CLI 配置
{: #openwhisk_apigateway_cli}
此實驗性特性只能與新的 OpenWhisk 鑑別模型搭配運作，在這個模型中，每一個名稱空間現在都會有相關聯的唯一鑑別金鑰。
請遵循[配置 CLI](https://console.ng.bluemix.net/openwhisk/cli) 中有關如何設定您特定名稱空間之鑑別金鑰的指示。

## 公開 OpenWhisk 動作
{: #openwhisk_apigateway_hello}

讓我們公開已與 OpenWhisk 一起預先安裝的簡式動作

```
wsk api-experimental create /hello /echo get /whisk.system/utils/echo
```
{: pre}
```
ok: created api /echo GET for action /whisk.system/utils/echo
https://21ef035.api-gw.mybluemix.net/hello/echo
```
{: screen}
透過 **GET** HTTP 方法，產生可公開 `echo` 動作的新 URL。

將 HTTP 要求傳送至 URL，來開始嘗試。
```
curl https://21ef035.api-gw.mybluemix.net/hello/echo?marco=polo
```
{: pre}
這將呼叫 `echo` 動作，以傳回含有已傳送參數的 JSON 字串。
```
{
  "marco":"polo"
}
```
{: screen}

您可以透過簡式查詢參數或透過要求內文，將參數傳遞至動作。

### 公開多個動作
{: #openwhisk_apigateway_actions}

假設您要公開好友讀書會的一組動作。
您有一系列的動作，以實作您的讀書會後端：

| 動作 (action) | HTTP 方法 | 說明 |
| ----------- | ----------- | ------------ |
| getBooks    | GET | 取得書籍詳細資料  |
| postBooks   | POST | 新增書籍 |
| putBooks    | PUT | 更新書籍詳細資料 |
| deleteBooks | DELETE | 刪除書籍 |

請使用 `/club` 作為其 HTTP URL 基本路徑及 `books` 作為其資源，來建立讀書會的 API（名為 `Book Club`）。
```
wsk api-experimental create -n "Book Club" /club /books get getBooks
wsk api-experimental create /club /books post postBooks
wsk api-experimental create /club /books put putBooks
wsk api-experimental create /club /books delete deleteBooks
```
{: pre}

請注意，公開基本路徑 `/club` 的第一個動作會取得名稱為 `Book Club` 的 API 標籤。在 `/club` 下公開的任何其他動作都會與 `Book Club` 相關聯。

讓我們列出所有剛剛公開的動作。

```
wsk api-experimental list
```
{: pre}
```
ok: apis
Action                   Verb          API Name        URL
getBooks                   get         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

現在，讓我們試試使用 HTTP **POST** 來新增 `JavaScript: The Good Parts` 書籍。
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": "success"
}
```
{: screen}

讓我們透過 HTTP **GET**，使用我們的動作 `getBooks` 來取得書籍清單。
```
curl -X GET https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### 匯出配置
讓我們將名為 `Book Club` 的 API 匯出至檔案，以用作使用檔案作為輸入來重建 API 的基礎。 
```
wsk api get "Book Club" > club-swagger.json
```
{: pre}

讓我們先刪除一般基本路徑下的所有已公開 URL，來測試 Swagger 檔案。
您可以刪除所有使用基本路徑 `/club` 或 API 名稱標籤 `"Book Club"` 的已公開 URL：
```
wsk api-experimental delete /club
```
{: pre}
```
ok: deleted API /club
```
{: screen}

現在，讓我們使用檔案 `club-swagger.json` 來還原名為 `Book Club` 的 API。
```
wsk api create --config-file club-swagger.json
```
{: pre}
```
ok: created api /books delete for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books get for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books post for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books put for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

我們可以驗證已重建 API
```
wsk api list /club
```
{: pre}
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

- **附註**：此特性目前是實驗性供應項目，可讓使用者早期試用並提供意見。下列是已收到的意見：
  - 無法自訂「跨原點資源共用 (CORS)」的 HTTP 存取控制；目前，產生的 API 回應標頭配置成容許任何 HTTP 動詞或來源（即 *）。一律會傳回下列標頭：
    - Access-Control-Allow-Origin：*
    - Access-Control-Allow-Headers：Authorization、Content-Type
    - Access-Control-Allow-Methods：GET、POST、PUT、DELETE、PATCH、HEAD、OPTIONS
  - 要求及回應僅支援內容類型 `application/json`。
  - 無法透過程式設計方式控制來自 OpenWhisk 動作的回應。
  - 所有 OpenWhisk 動作都是透過公用存取來公開，無法配置自訂 API 金鑰。
  - 不支援路徑參數，僅支援查詢參數及要求內文。
  - 如果建立的 API 沒有 API 名稱，則名稱將是基本路徑，無法進行變更。
  - 透過輸入檔重建 API 時，需要先刪除 API。
  - 匯出包含 OpenWhisk API 金鑰的 API 時，這是機密資訊，沒有可用的範本。
