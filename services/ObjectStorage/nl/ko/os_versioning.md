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


# 오브젝트 버전화 설정 {: #setting-up-versioning}

오브젝트 버전화를 사용하면 이전 버전의 오브젝트를 자동으로 백업 컨테이너에 저장하여 보관할 수 있습니다. 그러면 각 오브젝트의 히스토리를 보고 변경이 이루어진 경우를 계속 추적할 수 있습니다.
{: shortdesc}

기본 컨테이너에 새 파일 버전을 업로드하는 경우 이전 버전이 자동으로 백업 컨테이너로 이동합니다. 기본 컨테이너에서 파일을 삭제하면 백업 컨테이너에 있는 최신 버전 파일이 자동으로 기본 컨테이너로 이동하여 삭제된 파일을 대체합니다. 

1. 컨테이너를 작성하고 이름을 지정합니다. *container_name* 변수를 컨테이너에 지정할 이름으로 대체합니다. 

    ```
swift post <container_name>
```
    {: pre}

2. 백업 스토리지 역할을 할 두 번째 컨테이너를 작성하고 이름을 지정합니다. 

    ```
    swift post <backup_container_name>
    ```
    {: pre}

3. 버전화를 설정하십시오. 

    Swift 명령:

    ```
    swift post <container_name> -H "X-Versions-Location:<backup_container_name>"
    ```
    {: pre}

      cURL 명령: 

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<backup_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}

4. 처음으로 기본 컨테이너에 오브젝트를 업로드하십시오. 

    ```
    swift upload <container_name> <object>
    ```
    {: pre}

5. 오브젝트를 변경합니다. 

6. 새 오브젝트 버전을 기본 컨테이너에 업로드합니다. 

    ```
    swift upload <container_name> <object>
    ```
    {: pre}

7.  백업 컨테이너의 오브젝트는 `<Length><Object_name>/<Timestamp>` 형식으로 이름이 자동 지정됩니다.
  <table>
    <tr>
      <th> 속성 </th>
      <th> 설명 </th>
    </tr>
    <tr>
      <td> <i>Length</i> </td>
      <td> 오브젝트 이름의 길이입니다. 3자의 영(0)으로 채워진 16진수입니다. </td>
    </tr>
    <tr>
      <td> <i>Object_name</i> </td>
      <td> 오브젝트 이름입니다. </td>
    </tr>
    <tr>
      <td> <i>Timestamp</i> </td>
      <td> 오브젝트의 버전이 처음 업로드된 때를 나타내는 시간소인입니다. </td>
    </tr>
  </table>

  표 1: 이름 지정 속성 설명

6. 기본 컨테이너의 오브젝트를 나열하여 파일의 새 버전을 확인합니다. 

    ```
    swift list --lh <container_name>
    ```
    {: pre}

7. 백업 컨테이너의 오브젝트를 나열합니다. 파일의 이전 버전이 이 컨테이너에 저장되어 있는 것을 확인할 수 있습니다. 시간소인도 파일에 추가되어 있습니다. 

    ```
    swift list --lh <backup_container_name>
    ```
    {: pre}

8. 기본 컨테이너의 오브젝트를 삭제합니다. 오브젝트를 삭제하면 백업 컨테이너에 있는 최신 버전이 자동으로 기본 컨테이너로 이동합니다. 

    ```
    swift delete <container_name>
    <object>
    ```
    {: pre}

9. 선택사항: 오브젝트 버전화의 사용을 해제합니다. 

    Swift 명령:

    ```
    swift post <container_name> -H "X-Remove-Versions-Location:"
    ```
    {: pre}

      cURL 명령: 

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/<container_name>
    ```
    {: pre}
