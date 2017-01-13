---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Configuration des règles de sécurité
{: #set_up_policies.md}
Dernière mise à jour : 15 novembre 2016
{: .last-updated}

Un analyste de sécurité peut configurer des règles de sécurité de connexion et des listes noires ou des listes blanches.

## Configuration des règles de connexion

Vous pouvez définir le niveau de sécurité par défaut qui est appliqué à tous les terminaux. Vous pouvez ensuite ajouter des paramètres de sécurité personnalisés pour des terminaux spécifiques.

1. Sur la page **Règles** du module complémentaire de Gestion des risques et de la sécurité, cliquez sur **Configurer** en regard de **Sécurité de connexion**.
2. Sur la page **Sécurité de connexion**, sélectionnez le niveau de sécurité de connexion par défaut dans la liste déroulante. La valeur que vous sélectionnez ici s'applique à tous les terminaux, à l'exception des terminaux dotés de paramètres de connexion personnalisés. Ces règles affectent la façon dont les terminaux se connectent au serveur - elles ne modifient aucun paramètre sur le terminal même ou n'envoient aucun message sur le terminal. Vous pouvez sélectionner l'un des niveaux de sécurité suivants par défaut :
    - TLS facultatif
    - TLS avec authentification par jeton
    - TLS avec authentification par certificat client
    - TLS avec authentification par jeton et par certificat client

En fonction du niveau de sécurité sélectionné, le tableau indique le nombre de terminaux concernés et le niveau de conformité prévu au niveau de sécurité défini.

3. Si nécessaire, cliquez sur **Ajouter une connexion personnalisée** et sélectionnez les types de terminaux et les niveaux de sécurité personnalisés. La valeur de conformité prévue est mise à jour pour refléter les modifications résultant des paramètres de sécurité personnalisés.
4. Cliquez sur **Sauvegarder**.  

## Configuration des listes noires et des listes blanches

Limitez l'accès au serveur à partir de certains terminaux en utilisant une liste noire ou utilisez une liste blanche pour accorder l'accès au serveur à des terminaux spécifiques. Vous pouvez utiliser une liste noire ou une liste blanche - elles ne peuvent pas être utilisées ensemble.

### Configuration d'une liste noire

1. Sur la page **Règles** du module complémentaire de Gestion des risques et de la sécurité, dans la section **Liste noire**, cliquez sur **Configurer**.
2. Dans la page **Liste noire**, cliquez sur **Ajouter à la liste noire**.
3. Dans la fenêtre **Ajouter à la liste noire**, effectuez l'une des opérations suivantes :
    - Dans l'onglet **Adresse IP/plage**, saisissez les adresses IP que vous souhaitez bloquer ou les plages d'adresses IP pour plusieurs terminaux consécutifs.
    - Dans l'onglet **CIDR**, entrez un bloc notéClassless Inter-Domain Routing (CIDR).
    - Dans l'onglet **Pays**, entrez ou sélectionnez les pays dont vous souhaitez bloquer tous les terminaux.
4. Dans la fenêtre **Ajouter à la liste noire**, cliquez sur **Sauvegarder**.
5. Consultez la liste des terminaux bloqués. Tous les terminaux figurant dans la liste, en fonction de l'adresse IP, du routage CIDR ou du pays, ne peuvent pas se connecter au serveur Watson IoT Platform.
6. Cliquez sur **Sauvegarder**.

### Configuration d'une liste blanche
1. Sur la page **Règles** du module complémentaire de Gestion des risques et de la sécurité, cliquez sur **Configurer** en regard de **Ligne blanche**.
2. Dans la page **Liste blanche**, cliquez sur **Ajouter à la liste blanche**.
3. Dans la fenêtre **Ajouter à la liste blanche**, effectuez l'une des opérations suivantes :
    - Dans l'onglet **Adresse IP/plage**, saisissez les adresses IP dont vous souhaitez autoriser l'accès ou les plages d'adresses IP pour plusieurs terminaux consécutifs.
    - Dans l'onglet **CIDR**, entrez un bloc notéClassless Inter-Domain Routing (CIDR).
    - Dans l'onglet **Pays**, entrez ou sélectionnez les pays dont vous souhaitez autoriser l'accès de tous les terminaux.
4. Dans la fenêtre **Ajouter à la liste blanche**, cliquez sur **Sauvegarder**.
5. Consultez la liste des terminaux autorisés. Tous les terminaux figurant dans la liste, en fonction de l'adresse IP, du routage CIDR ou du pays, sont autorisés à se connecter au serveur Watson IoTP Platform.
6. Cliquez sur **Sauvegarder**.
