---
title: "JDBC 드라이버를 통해 Hive 쿼리 - Azure HDInsight | Microsoft Docs"
description: "Java 응용 프로그램에서 JDBC 드라이버를 사용하여 HDInsight의 Hadoop에 Hive 쿼리를 제출합니다. 프로그래밍 방식으로 SQuirrel SQL 클라이언트에서 연결합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.translationtype: Human Translation
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.openlocfilehash: 14bfdd8554b075b0c19a75bb572f1214a45ff471
ms.contentlocale: ko-kr
ms.lasthandoff: 07/08/2017

---
# <a name="query-hive-through-the-jdbc-driver-in-hdinsight"></a>HDInsight에서 JDBC 드라이버를 통해 Hive 쿼리

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Java 응용 프로그램에서 JDBC 드라이버를 사용하여 Azure HDInsight의 Hadoop에 Hive 쿼리를 제출하는 방법을 알아봅니다. 이 문서의 정보는 프로그래밍 방식으로 SQuirrel SQL 클라이언트에서 연결하는 방법을 보여 줍니다.

Hive JDBC 인터페이스에 대한 자세한 내용은 [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

* HDInsight 클러스터의 Hadoop. Linux 또는 Windows 기반의 클러스터가 작동합니다.

  > [!IMPORTANT]
  > Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다. 자세한 내용은 [HDInsight 3.3 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

* [SQuirreL SQL](http://squirrel-sql.sourceforge.net/). SQuirreL은 JDBC 클라이언트 응용 프로그램입니다.

* [JDK(Java Developer Kit) 버전 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 이상

* [Apache Maven](https://maven.apache.org). Maven은 이 문서와 관련된 프로젝트에서 사용되는 Java 프로젝트에 대한 프로젝트 빌드 시스템입니다.

## <a name="jdbc-connection-string"></a>JDBC 연결 문자열

Azure에서 HDInsight 클러스터에 대한 JDBC가 443을 통해 연결되어 트래픽이 SSL을 사용하여 보호됩니다. 클러스터가 뒤에 있는 공용 게이트웨이는 HiveServer2에서 실제로 수신하는 포트로 트래픽을 리디렉션합니다. 다음은 예제 연결 문자열입니다.

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

`CLUSTERNAME` 을 HDInsight 클러스터 이름으로 바꿉니다.

## <a name="authentication"></a>인증

연결을 설정할 때 HDInsight 클러스터 관리자 이름 및 암호를 사용하여 클러스터 게이트웨이에 대해 인증해야 합니다. SQuirreL SQL 등의 JDBC 클라이언트에서 연결할 때 클라이언트 설정에 관리자 이름 및 암호를 입력해야 합니다.

Java 응용 프로그램에서 연결을 설정할 때 이름 및 암호를 사용해야 합니다. 예를 들어 다음 Java 코드는 연결 문자열, 관리자 이름 및 암호를 사용하여 새 연결을 엽니다.

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a>SQuirreL SQL 클라이언트를 사용하여 연결

SQuirreL SQL은 HDInsight 클러스터와 함께 Hive 쿼리를 원격으로 실행하는 데 사용할 수 있는 JDBC 클라이언트입니다. 다음 단계에서는 SQuirreL SQL을 이미 설치했다고 가정합니다.

1. HDInsight 클러스터에서 Hive JDBC 드라이버를 복사합니다.

    * **Linux 기반 HDInsight**의 경우 다음 단계에 따라 필요한 jar 파일을 다운로드합니다.

        1. 파일을 포함하는 디렉터리를 만듭니다. 예: `mkdir hivedriver`.

        2. 명령줄에서 다음 명령을 사용하여 HDInsight 클러스터에서 파일을 복사합니다.

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            `USERNAME`은 클러스터의 SSH 사용자 계정 이름으로 바꿉니다. `CLUSTERNAME`은 HDInsight 클러스터 이름으로 바꿉니다.

    * **Windows 기반 HDInsight**의 경우 다음 단계에 따라 jar 파일을 다운로드합니다.

        1. Azure Portal에서 HDInsight 클러스터를 선택한 다음 **원격 데스크톱** 아이콘을 선택합니다.

            ![원격 데스크톱 아이콘](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. [원격 데스크톱] 블레이드에서 **연결** 단추를 사용하여 클러스터에 연결합니다. 원격 데스크톱을 사용하지 않는 경우 사용자 이름 및 암호를 입력하는 양식을 사용한 다음 **사용**을 선택하여 클러스터에서 원격 데스크톱을 사용하도록 설정합니다.

            ![원격 데스크톱 블레이드](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            **연결**을 선택하면 .rdp 파일이 다운로드됩니다. 이 파일을 사용하여 원격 데스크톱 클라이언트를 시작합니다. 메시지가 표시되면 원격 데스크톱 액세스에 입력한 사용자 이름 및 암호를 사용합니다.

        3. 연결되면 원격 데스크톱 세션에서 다음 파일을 로컬 컴퓨터에 복사합니다. `hivedriver`라는 이름의 로컬 디렉터리에 넣습니다.

            * C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar

            > [!NOTE]
            > 경로 및 파일 이름에 포함된 버전 번호는 클러스터마다 다를 수 있습니다.

        4. 파일을 복사한 후 원격 데스크톱 세션의 연결을 끊습니다.

2. SQuirreL SQL 응용 프로그램을 시작합니다. 왼쪽 창에서 **드라이버**를 선택합니다.

    ![창 왼쪽의 드라이버 탭](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. **드라이버** 대화 상자 위쪽의 아이콘에서 **+** 아이콘을 선택하여 드라이버를 만듭니다.

    ![드라이버 아이콘](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. 드라이버 추가 대화 상자에 다음 정보를 추가합니다.

    * **이름**: Hive
    * **예제 URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`
    * **추가 클래스 경로**: [추가] 단추를 사용하여 이전에 다운로드한 jar 파일을 추가합니다.
    * **클래스 이름**: org.apache.hive.jdbc.HiveDriver

   ![드라이버 추가 대화 상자](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   **확인**을 클릭하여 이러한 설정을 저장합니다.

5. SQuirreL SQL 창의 왼쪽에서 **별칭**을 선택합니다. 그런 다음 **+** 아이콘을 클릭하여 연결 별칭을 만듭니다.

    ![새 별칭 추가](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. **별칭 추가** 대화 상자에서 다음 값을 사용합니다.

    * **이름**: Hive on HDInsight

    * **드라이버**: 드롭다운에서 **Hive** 드라이버를 선택합니다.

    * **URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

        **CLUSTERNAME** 을 HDInsight 클러스터의 이름으로 바꿉니다.

    * **사용자 이름**: HDInsight 클러스터의 클러스터 로그인 계정 이름입니다. 기본값은 `admin`입니다.

    * **암호**: 클러스터 로그인 계정의 암호입니다.

 ![별칭 추가 대화 상자](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    **테스트** 단추를 사용하여 연결이 작동하는지 확인합니다. **연결 대상: Hive on HDInsight** 대화 상자가 나타나면 **연결**을 선택하여 테스트를 수행합니다. 테스트가 성공하면 **연결 성공** 대화 상자가 표시됩니다.

    연결 별칭을 저장하려면 **별칭 추가** 대화 상자의 아래쪽에 있는 **확인** 단추를 사용합니다.

7. SQuirreL SQL 위쪽의 **연결 대상** 드롭다운에서 **Hive on HDInsight**를 선택합니다. 메시지가 표시되면 **연결**을 선택합니다.

    ![연결 대화 상자](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. 연결되면 SQL 쿼리 대화 상자에 다음 쿼리를 입력한 다음 **실행** 아이콘을 선택합니다. 결과 영역에 쿼리 결과가 표시됩니다.

        select * from hivesampletable limit 10;

    ![결과를 포함한 sql 쿼리 대화 상자](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a>Java 응용 프로그램 예제에서 연결

HDInsight에서 Hive를 쿼리하는 데 Java 클라이언트를 사용하는 예제를 [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc)에서 사용할 수 있습니다. 리포지토리의 지침에 따라 샘플을 빌드하고 실행합니다.

## <a name="troubleshooting"></a>문제 해결

### <a name="unexpected-error-occurred-attempting-to-open-an-sql-connection"></a>SQL 연결을 열 때 예기치 않은 오류가 발생했습니다

**증상**: 버전 3.3 또는 3.4인 HDInsight 클러스터에 연결할 때 예기치 않은 오류가 발생할 수 있습니다. 이 오류에 대한 스택 추적은 다음 줄로 시작합니다.

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

**원인**: 이 오류는 SQuirreL에서 사용하는 common-codec.jar 파일 버전과 Hive JDBC 구성 요소에 필요한 파일의 버전과 일치하지 않아 발생합니다.

**해결**: 이 오류를 해결하려면 다음 단계를 수행합니다.

1. HDInsight 클러스터에서 common-codec jar 파일을 다운로드합니다.

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. SQuirreL을 종료한 다음 시스템에서 SQuirreL이 설치된 디렉터리로 이동합니다. SquirreL 디렉터리의 `lib` 디렉터리에서 기존 common-codec.jar 파일을 HDInsight 클러스터에서 다운로드한 파일로 바꿉니다.

3. SQuirreL을 다시 시작합니다. HDInsight에서 Hive에 연결할 때 오류가 더 이상 발생하지 않아야 합니다.

## <a name="next-steps"></a>다음 단계

JDBC를 사용하여 Hive와 함께 작업하는 방법을 살펴보았으므로 이제 다음 링크를 사용하여 Azure HDInsight로 작업하는 다른 방법을 알아봅니다.

* [HDInsight에 데이터 업로드](hdinsight-upload-data.md)
* [HDInsight에서 Hive 사용](hdinsight-use-hive.md)
* [HDInsight에서 Pig 사용](hdinsight-use-pig.md)
* [HDInsight에서 MapReduce 작업 사용](hdinsight-use-mapreduce.md)

