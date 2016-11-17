---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Latest updates
{: #latest_updates}

A list of the latest updates to the service.

## November 8, 2016: Updated WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Added ability for clients to request a [Public IP](networkEnvironment.html#networkEnvironment) address for their WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} VM
* Addressed [several security vulnerabilities](http://www-01.ibm.com/support/docview.wss?uid=swg21993842){: new_window} that affect WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} including:
  * A vulnerability in IBM WebSphere Application Server that could allow remote attackers to execute arbitrary Java code with a serialized object from untrusted sources.
  * A denial of service vulnerability caused by an out-of-bounds read in the TS_OBJ_print_bio function. A remote attacker could exploit this vulnerability using a specially crafted time-stamp file to cause the application to crash.
  * A potential vulnerability in OpenSSL that could allow a remote attacker to obtain sensitive information, caused by an error in the in the Triple-DES on 64-bit block cipher, used as a part of the SSL/TLS protocol. By capturing large amounts of encrypted traffic between the SSL/TLS server and the client, a remote attacker able to conduct a man-in-the-middle attack could exploit this vulnerability to recover the plaintext data and obtain sensitive information. This vulnerability is known as the SWEET32 Birthday attack.
  * OpenSSL is vulnerable to a denial of service. By repeatedly requesting renegotiation, a remote authenticated attacker could send an overly large OCSP Status Request extension to consume all available memory resources.
  * OpenSSL is vulnerable to a denial of service, caused by an integer overflow in the MDC2_Update function. By using unknown attack vectors, a remote attacker could exploit this vulnerability to trigger an out-of-bounds write and cause the application to crash.
  * A potential vulnerability in OpenSSL that allows a remote attacker to obtain sensitive information, caused by an error in the DSA implementation that allows the following of a non-constant time codepath for certain operations. An attacker could exploit this vulnerability using a cache-timing attack to recover the private DSA key.
  * OpenSSL is vulnerable to a denial of service, caused by missing message length checks when parsing certificates. A remote authenticated attacker could exploit this vulnerability to trigger an out-of-bounds read and cause a denial of service.

## September 19, 2016: Updated WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Upgraded the WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} binaries so that new instances of WebSphere Application Server Liberty (Core and ND Plans) have fixpack 16.0.0.3 installed.
* Addressed [several security vulnerabilities](http://www-01.ibm.com/support/docview.wss?uid=swg21990236){: new_window} that affect WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} including:
  * A vulnerability in IBM WebSphere Application Server Liberty that could allow a remote attacker to conduct phishing attacks.
  * A vulnerability in IBM WebSphere Application Server Liberty to cross-site scripting in OpenID Connect clients.
  * A potential vulnerability in IBM WebSphere Application Server Liberty that could allow a remote attacker to obtain sensitive information caused by improper handling of exceptions when a default error page does not exist.
  * A vulnerability in Apache Tomcat to a denial of service, caused by an error in the Apache Commons FileUpload component.
  * A vulnerability in IBM WebSphere Application Server and IBM WebSphere Application Server Liberty that could allow a remote attacker to obtain sensitive information, caused by the improper handling of responses under certain conditions.
  * An unspecified vulnerability related to the Networking component that has no confidentiality impact, low integrity impact, and no availability.

## August 17, 2016: Updated WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Upgraded the WebSphere Application Server for Bluemix binaries from 8.5.5.9 to 8.5.5.10
* Addressed [several security vulnerabilities](http://www-01.ibm.com/support/docview.wss?uid=swg21988710){: new_window} that affect WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} including:
  * Apache Struts vulnerabilities that affect the WebSphere Application Server and WebSphere Application Server Hypervisor Edition Administration Console.
  * A potential denial of service vulnerability with IBM WebSphere Application Server when using SIP services.
  * Several vulnerabilities that may affect the IBM HTTP Server used by WebSphere Application Server.
  * A vulnerability that allows redirecting of HTTP traffic with CGI applications that may affect IBM HTTP Server (IHS). This vulnerability is known as "HTTPOXY".
  * An Information Disclosure Vulnerability in IBM WebSphere Application Server.
  * A potential bypass security restriction vulnerability in IBM WebSphere Application Server that only occurs in environments that have the webcontainer custom property HttpSessionIdReuse enabled.


## June 24, 2016: Updated WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Added ability for clients to to choose between V8.5 and V9.0 when you create a new _Traditional ND_ or _Traditional WebSphere_ instance.
* Upgraded the WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} binaries so that new instances of WebSphere Application Server Liberty (Core and ND Plans) have fixpack 16.0.0.2 installed. 16.0.0.2 is the next fixpack after 8.5.5.9. As of 16.0.0.2, all entitled Liberty optional features supported for these plans are installed by default.
* Addressed [Several security vulnerabilities](http://www-01.ibm.com/support/docview.wss?uid=swg21984977){: new_window} that affect WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} including:
  * An XML External Entity Injection (XXE) vulnerability in the Apache Standard Taglibs that affects IBM WebSphere Application Server.
  * A potential for weaker than expected security when using the WebSphere Application Server Liberty profile API Discovery feature and Swagger documents.
  * A potential information disclosure vulnerability in Admin Center for IBM WebSphere Application Server Liberty.
  * A potential HTTP response splitting vulnerability in IBM WebSphere Application Server.
  * OpenSSL vulnerabilities disclosed on May 3, 2016 by the OpenSSL Project.

## June 13, 2016: Updated WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Added ability for clients to build, provision, manage, and delete virtual machine instances through the creation of an application or script that uses WebSphere Application Server for Bluemix RESTful APIs.
* Added function that allows a client to have a fixed number of STOPPED instances with no more than 10 IP addresses or 64 GB of memory. Clients are now charged for accumulated instances in the STOPPED state at a reduced rate of 5%.

## April 26, 2016: Updated WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Addressed  [potential security vulnerabilities](http://www-01.ibm.com/support/docview.wss?uid=swg21982128){: new_window} in WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} if FIPS 140-2 is enabled and multiple vulnerabilities in Samba - including Badlock.
* Integrated miscellaneous service maintenance.

## April 15, 2016: Updated WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Upgraded the WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} binaries from 8.5.5.8 to 8.5.5.9
* Addressed a [Cross-site scripting](http://www-01.ibm.com/support/docview.wss?uid=swg21981221){: new_window} vulnerability in Liberty for Java for IBM {{site.data.keyword.Bluemix_notm}} that affects consumers using the OpenID Connect (OIDC) client.
* Integrated miscellaneous service maintenance.

## February 19, 2016: Updated WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* Added an option for clients with memory-intensive applications to "right-size" their environment with larger virtual machines. Clients can select the specific resource size of a given WebSphere Application Server component or single system up to 32 GB RAM virtual machines.
* Upgraded the WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} binaries from 8.5.5.7 to 8.5.5.8
* Addressed multiple vulnerabilities in IBM SDK Java Technology Edition that affect WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} that are commonly referred to as [SLOTH](http://www-01.ibm.com/support/docview.wss?uid=swg21977244){: new_window}.
* Addressed a [Cross-site scripting](http://www-01.ibm.com/support/docview.wss?uid=swg21976337){: new_window} vulnerability that affects consumers of the OAuth provider output.
* Integrated miscellaneous service maintenance.

## December 11, 2015: Updated WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* Changed the official product name from IBM Application Server on Cloud for {{site.data.keyword.Bluemix_notm}} to IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* Added new capabilities to the WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment plan. The plan consists of a WebSphere Application Server Network Deployment cell environment with two or more virtual machines. These new capabilities allow users to set up a clustered environment for high availability, failover, and scalability.
* Added new capabilities to the WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Liberty Core plan. The plan includes the use of a Liberty Collective, which is an administrative domain for a group of Liberty profiles (servers) and consists of two or more virtual machines
* Upgraded the WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} binaries from 8.5.5.6 to 8.5.5.7
* Addressed an [Apache Commons Collections vulnerability](https://www.us-cert.gov/ncas/current-activity/2015/11/13/Apache-Commons-Collections-Java-Library-Vulnerability){: new_window} for handling Java object deserialization.
* Addressed a vulnerability that could allow an [HTTP response splitting attack](http://www-01.ibm.com/support/docview.wss?uid=swg21972254){: new_window}.
* Integrated miscellaneous service maintenance.

## October 15, 2015: Updated Application Server on Cloud
* Added the following two new plans:
  * [WebSphere Application Server Traditional V9 Beta](https://www-01.ibm.com/marketing/iwm/iwmdocs/web/cc/earlyprograms/websphere.shtml){: new_window}
  * WebSphere Application Server ND
* Miscellaneous service maintenance
