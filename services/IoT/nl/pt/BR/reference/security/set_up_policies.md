---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Configurando as Políticas de Segurança
{: #set_up_policies.md}
Última atualização: 15 de novembro de 2016
{: .last-updated}

Um analista de segurança pode configurar políticas de segurança de conexão e listas de bloqueio ou listas de desbloqueio.

## Configurando políticas de conexão

É possível configurar o nível de segurança padrão que é aplicado a todos os dispositivos. É possível, então, incluir configurações de segurança customizadas para dispositivos específicos.

1. Na página **Polícias** do complemento Gerenciamento de Risco e Segurança, clique em **Configurar** ao lado de **Segurança de Conexão**.
2. Na página **Segurança de Conexão**, selecione o nível de segurança de conexão padrão na lista suspensa. O valor que você seleciona aqui é aplicado a todos os dispositivos, exceto aos dispositivos que tenham configurações de conexão customizadas. Essas políticas afetam como os dispositivos se conectam ao servidor -- eles não mudam nenhuma configuração no dispositivo real nem enviam nenhuma mensagem para o dispositivo. É possível selecionar um dos níveis de segurança a seguir como o padrão:
    - TLS opcional
    - TLS com Autenticação do Token
    - TLS com Autenticação por Certificado de Cliente
    - TLS com Autenticação do Token e Autenticação por Certificado de Cliente

Com base no nível de segurança selecionado, a tabela mostra o número de dispositivos que são impactados e o nível previsto de conformidade no nível de segurança configurado.

3. Se necessário, clique em **Incluir conexão customizada** e selecione os tipos de dispositivo e os níveis de segurança customizados. O valor de conformidade previsto é atualizado para refletir as mudanças resultantes das configurações de segurança customizadas.
4. Clique em **Salvar**.  

## Configurando listas de bloqueio e listas de desbloqueio

Restrinja o acesso ao servidor de determinados dispositivos usando uma lista de bloqueio ou use uma lista de desbloqueio para conceder acesso ao servidor a dispositivos específicos. Você pode usar uma lista de bloqueio ou uma lista de desbloqueio -- elas não podem ser usadas juntas.

### Configurar uma lista de bloqueio

1. Na página **Políticas** de Gerenciamento de Risco e Segurança, na seção **Lista de Bloqueio**, clique em **Configurar**.
2. Na página **Lista de Bloqueio**, clique em **Incluir na Lista de Bloqueio**.
3. Na janela **Incluir na Lista de Bloqueio**, execute uma das ações a seguir:
    - Na guia **Endereço IP/Intervalo**, insira os dispositivos de endereços IP que você deseja bloquear ou os intervalos de endereços IP para vários dispositivos consecutivos.
    - Na guia **CIDR**, insira um bloco indicado Classless Inter-Domain Routing (CIDR).
    - Na guia **País**, insira ou selecione países dos quais você deseja bloquear todos os dispositivos
4. Na janela **Incluir na Lista de Bloqueio**, clique em **Salvar**.
5. Revise a lista de dispositivos bloqueados. Todos os dispositivos que fazem parte da lista, com base no endereço IP, CIDR ou país, não são capazes de se conectar ao servidor Watson IoT Platform.
6. Clique em **Salvar**.

### Configure uma lista de desbloqueio
1. Na página **Políticas** de Gerenciamento de Risco e Segurança, clique em **Configurar** ao lado de **Lista de Desbloqueio**.
2. Na página **Lista de Desbloqueio**, clique em **Incluir na Lista de Desbloqueio**.
3. Na janela **Incluir na Lista de Desbloqueio**, execute uma das ações a seguir:
    - Na guia **Endereço IP/Intervalo**, insira os dispositivos de endereços IP aos quais você deseja permitir o acesso ou os intervalos de endereços IP para vários dispositivos consecutivos.
    - Na guia **CIDR**, insira um bloco indicado Classless Inter-Domain Routing (CIDR).
    - Na guia **País**, insira ou selecione países dos quais você deseja bloquear o acesso para todos os dispositivos.
4. Na janela **Incluir na Lista de Desbloqueio**, clique em **Salvar**.
5. Revise a lista de dispositivos permitidos. Todos os dispositivos que fazem parte da lista, com base no endereço IP, CIDR ou país, são capazes de se conectar ao servidor Watson IoTP.
6. Clique em **Salvar**.
