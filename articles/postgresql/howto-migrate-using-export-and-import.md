---
title: "PostgreSQL용 Azure Database에서 가져오기 및 내보내기를 사용한 데이터베이스 마이그레이션 | Microsoft Docs"
description: "PostgreSQL 데이터베이스를 스크립트 파일로 추출하고 데이터를 해당 파일에서 대상 데이터베이스로 가져오는 방법을 설명합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/14/2017
ms.translationtype: Human Translation
ms.sourcegitcommit: ef1e603ea7759af76db595d95171cdbe1c995598
ms.openlocfilehash: e05e61ea05afc2866a618c663cb437540ab54c9b
ms.contentlocale: ko-kr
ms.lasthandoff: 06/16/2017

---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a>내보내기 및 가져오기를 사용하여 PostgreSQL 데이터베이스 마이그레이션
[pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html)를 사용하여 PostgreSQL 데이터베이스를 스크립트 파일로 추출하고, [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html)을 사용하여 데이터를 해당 파일에서 대상 데이터베이스로 가져올 수 있습니다.

## <a name="prerequisites"></a>필수 조건
이 방법 가이드를 단계별로 실행하려면 다음이 필요합니다.
- 액세스를 허용하기 위한 방화벽 규칙을 사용하는 [PostgreSQL용 Azure Database 서버](quickstart-create-server-database-portal.md) 및 이에 속한 데이터베이스
- [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) 명령줄 유틸리티 설치
- [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) 명령줄 유틸리티 설치

이러한 단계를 수행하여 PostgreSQL 데이터베이스를 내보내고 가져옵니다.

## <a name="create-a-script-file-using-pgdump-that-contains-the-data-to-be-loaded"></a>로드할 데이터를 포함하는 pg_dump를 사용하여 스크립트 파일 만들기
온-프레미스 또는 VM의 기존 PostgreSQL 데이터베이스를 sql 스크립트 파일로 내보내려면 기존 환경에서 다음 명령을 실행합니다.
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
예를 들어, 로컬 서버와 **testdb**라는 데이터베이스가 있는 경우
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-the-data-on-target-azure-database-for-postrgesql"></a>PostrgeSQL용 대상 Azure Database에서 데이터 가져오기
psql 명령줄 및 -d, --dbname 매개 변수를 사용하여 sqp 파일에서 데이터를 만들고 로드한 PostrgeSQL용 Azure Database에 데이터를 가져올 수 있습니다.
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
이 예제에서는 psql 유틸리티 및 이전 단계의 **testdb.sql**이라는 스크립트 파일을 사용하여 데이터를 대상 서버 **mypgserver-20170401.postgres.database.azure.com**의 데이터베이스 **mypgsqldb**로 가져옵니다.
```bash
psql --file=testdb.sql --host=mypgserver-20170401.database.windows.net --port=5432 --username=mylogin@mypgserver-20170401 --dbname=mypgsqldb
```

## <a name="next-steps"></a>다음 단계
- 덤프 및 복원을 사용하여 PostgreSQL 데이터베이스를 마이그레이션하려면 [덤프 및 복원을 사용하여 PostgreSQL 데이터베이스 마이그레이션](howto-migrate-using-dump-and-restore.md)을 참조하세요.
