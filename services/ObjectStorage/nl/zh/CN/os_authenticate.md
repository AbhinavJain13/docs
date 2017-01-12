---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 使用 Keystone 认证 {{site.data.keyword.objectstorageshort}} 实例

要与服务进行交互，您必须使用 Keystone 来认证 {{site.data.keyword.objectstorageshort}} 实例，以获取 URL 和不记名令牌。
{: shortdesc}


供应新的 {{site.data.keyword.objectstorageshort}} 实例将在 IBM 公共云中创建独立的 Keystone 项目。Keystone 凭证结构包含一整组属性，允许您选择最适合您的应用程序的 OpenStack 令牌请求方法或 OpenStack SDK。将新应用程序绑定到实例时，将创建具有项目访问权的新 Keystone 用户。撤销供应实例后，将删除项目和用户。

有关使用 OpenStack Swift 和 Keystone 的更多信息，请查看 [OpenStack 文档站点](http://docs.openstack.org)。

1. 建议使用的 V3 令牌请求是对 https://identity.open.softlayer.com/v1/auth/tokens 的 POST 请求，如以下 cURL 命令中所示：
  ```
  	curl -i \
	  -H "Content-Type: application/json" \
	  -d '
	{
		"auth": {
			"identity": {
				"methods": [
					"password"
				],
				"password": {
					"user": {
						"id": "ad78b2a3f843466988afd077731c61fc",
						"password": "XXXXXXXXXX"
					}
				}
  			},
			"scope": {
				"project": {
					"id": "0f47b41b06d047f9aae3b33f1db061ed"
				}
			}
  		}
  	}' \
	  https://identity.open.softlayer.com/v3/auth/tokens ; echo
```
  {: codeblock}

2. 使用 Keystone 进行认证时，将收到目录响应。请选择 `object-store` 端点并进行记录。构建完整 URL 时需要此端点。以下响应示例已经过修剪，只显示了与 {{site.data.keyword.objectstorageshort}} 相关的信息。

  ```
  	HTTP/1.1 201 Created
	Date: Mon, 29 Feb 2016 21:03:41 GMT
	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.1e-fips mod_wsgi/3.4 Python/2.7.5
	X-Subject-Token: gAAAAABW1LIubUgqKl-eInzhZUHWEnXijp7t6_5inl4DTRLxDhNbJ25ly2X7bASNvH7ocxinaJu_kdhSfnHNRwPAeYY77Ii2Cwp02-bvxUA1S9lV_knT6EyCOW2mSBl_HuuDD2cEgdiKmyZTVt-RvDxhPKYD-rHkJz-dHO4Folg8TVXotilb1uw
	Vary: X-Auth-Token
	x-openstack-request-id: req-01e096c8-5393-4f98-8ff6-029c55e42524
	Content-Length: 12051
	Content-Type: application/json

	{
	  "token" : {
	    "roles" : [
	      {
	        "id" : "f61f06a84f6443e880210fa986bd8691",
	        "name" : "ObjectStorageOperator"
	      }
	    ],
	    "catalog" : [
	      {
	        "endpoints" : [
	          {
	            "id" : "20cbfa6ff22b4a67a1484d30235bfc80",
  	            "region" : "london",
  	            "region_id" : "london",
  	            "url" : "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "admin"
  	          },
  	          {
  	            "id" : "38b8c081b11a452bb951698c334a406d",
  	            "region" : "london",
  	            "region_id" : "london",
  	            "url" : "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "internal"
  	          },
  	          {
  	            "id" : "4207049680fa4effbecd044c7448a8cb",
                "region" : "dallas",
                "region_id" : "dallas",
                "url" : "https://dal.objectstorage.open.softlayer.com/v1/AUTH_4abf7d7bac2c4eda89c03dd3afa7a0a3",
                "interface" : "public"
  	          },
  	          {
  	            "id" : "8a65a0cf38ac4211ad6a3c9c0eb337ff",
  	            "region" : "london",
  	            "region_id" : "london",
  	            "url" : "https://lon.objectstorage.open.softlayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "public"
  	          },
  	          {
  	            "id" : "a60cf32be624491d89170ef8264de5e8",
  	            "region" : "dallas",
  	            "region_id" : "dallas",
  	            "url" : "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "admin"
  	          },
  	          {
  	            "id" : "c769862200124a308d6748e418c971ba",
  	            "region" : "dallas",
  	            "region_id" : "dallas",
  	            "url" : "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "internal"
  	          }
  	        ],
	        "id" : "896e4064cbe742afbf9a543c15f27ac0",
	        "type" : "object-store",
	        "name" : "swift"
	      },
	    ],
	    "extras" : {

	    },
	    "user" : {
	      "id" : "0b8aebd924ef4cc7aa9232f07e47e874",
	      "name" : "user_87c094ce47a9feae3a137ffcbbfa098a888c12a8",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "expires_at" : "2016-02-29T22:03:42.061343Z",
	    "audit_ids" : [
	      "cbA-iL2dSheyB72PHd7q8Q"
	    ],
	    "issued_at" : "2016-02-29T21:03:42.000000Z",
	    "project" : {
	      "id" : "3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	      "name" : "object_storage_c1d8b3a1",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "methods" : [
	      "password"
	    ]
	  }
  	}
  ```
  {: screen}

  <table>
    <tr>
      <th> 响应端点</th>
      <th> 说明</th>
    </tr>
    <tr>
      <td> <code> X-Subject-Token </code></td>
      <td> 您的认证令牌。</td>
    </tr>
    <tr>
      <td> <code> id </code></td>
      <td> 您的 {{site.data.keyword.objectstorageshort}} 实例标识。</td>
    </tr>
    <tr>
      <td> <code> region </code></td>
      <td> 您的存储区域。请确保选择与凭证中所列字段相匹配的区域。</td>
    </tr>
    <tr>
      <td> <code> url </code></td>
      <td> 您的 {{site.data.keyword.objectstorageshort}} URL。用于通过 cURL 命令与服务进行交互。</td>
    </tr>
    <tr>
      <td> <code> interface </code></td>
      <td> 无法从 {{site.data.keyword.Bluemix_notm}} 访问内部接口。请使用公共接口 (<code>publicURL</code>)。</td>
    </tr>
  </table>

  表 1：POST 请求响应说明
