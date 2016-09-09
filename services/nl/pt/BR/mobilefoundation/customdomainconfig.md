---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurando o domínio customizado do servidor {{site.data.keyword.mobilefoundation_short}}
{: #configcustomdomain}

Última atualização: 08 de agosto de 2016
{: .last-updated}

O {{site.data.keyword.mobilefoundation_short}} provisiona um {{site.data.keyword.mfserver_short_notm}}, que é<!--on {{site.data.keyword.containerlong}} as a container group. The container group will be mapped to--> acessível usando uma URL que tem os nomes de domínio baseados na {{site.data.keyword.Bluemix_notm}} **Região**. Também é possível configurar seu próprio domínio customizado.
{:shortdesc}

A URL ou rota do <!--container group is created with a--> é criada
com os nomes de domínio padrão, com base na {{site.data.keyword.Bluemix_notm}} `Região`.

*Tabela 1. Nomes de domínio de aplicativo baseados na
'Region' no {{site.data.keyword.Bluemix_notm}}*

  |Domínio |  Região  |    
  |:----- | :----- |    
  |`mybluemix.net` | Sul dos EUA |    
  |`eu-gb.mybluemix.net` | Reino Unido  |
  |`au-syd.mybluemix.net` | Sydney  |      

Para ser capaz de usar seu próprio domínio, você precisará configurar o domínio customizado executando as etapas a seguir:

1.	Crie uma instância {{site.data.keyword.mfserver_short_notm}} criando a instância de serviço {{site.data.keyword.mobilefoundation_short}} escolhendo um dos planos suportados.

+ Inclua o domínio customizado que você gostaria de usar na `Organization` do {{site.data.keyword.Bluemix_notm}}. Acesse **Gerenciar organizações > DOMÍNIOS > INCLUIR DOMÍNIO** para incluir seu próprio domínio.

+ Configure uma rota para o servidor <!--container group--> usar seu domínio customizado.

+ Acesse o provedor DNS para o seu domínio e inclua uma entrada CNAME que roteará o
tráfego do seu domínio para a rota padrão do {{site.data.keyword.Bluemix_notm}}, na
qual o servidor <!--container group--> está em execução.

+ Se quiser configurar `https` para seu domínio customizado, faça upload do certificado SSL para seu domínio no {{site.data.keyword.Bluemix_notm}}. Para fazer isso, acesse **Gerenciar organizações > DOMÍNIOS**, selecione o domínio customizado para o qual você deseja configurar o certificado SSL, clique em **Fazer upload de certificado** para fazer upload do certificado SSL para seu domínio. Consulte [Certificados SSL e Domínios customizados do Bluemix](https://developer.ibm.com/bluemix/2014/09/28/ssl-certificates-bluemix-custom-domains/), para obter mais informações.
