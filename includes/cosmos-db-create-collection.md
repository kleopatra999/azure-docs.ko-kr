이제 Azure Portal에서 데이터 탐색기 도구를 사용하여 데이터베이스 및 컬렉션을 만들 수 있습니다. 

1. Azure Portal의 왼쪽 탐색 메뉴에서 **데이터 탐색기(미리 보기)**를 클릭합니다. 

2. **데이터 탐색기(미리 보기)** 블레이드에서 **새 컬렉션**을 클릭한 후 다음 정보를 제공합니다.

    ![Azure Portal 데이터 탐색기 블레이드](./media/cosmos-db-create-collection/azure-cosmosdb-data-explorer.png)

    설정|제안 값|설명
    ---|---|---
    데이터베이스 ID|작업|새 데이터베이스에 대한 이름입니다. 데이터베이스 이름은 1-255자여야 하며, /, \\, #,? 또는 후행 공백은 포함할 수 없습니다.
    컬렉션 ID|항목|새 컬렉션에 대한 이름입니다. 컬렉션 이름에는 데이터베이스 ID와 동일한 문자 요구 사항이 적용됩니다.
    저장소 용량| 고정(10GB)|기본값을 사용합니다. 이 값은 데이터베이스의 저장소 용량입니다.
    처리량|400RU|기본값을 사용합니다. 대기 시간을 줄이면 나중에 처리량을 늘릴 수 있습니다.
    파티션 키|/category|각 파티션에 데이터를 균등하게 배포하는 파티션 키입니다. 올바른 파티션 키를 선택하는 것은 성능이 뛰어난 컬렉션을 만드는 데 중요합니다. 자세한 내용은 [분할 디자인](../articles/cosmos-db/partition-data.md#designing-for-partitioning)를 참조하세요.    
3. 양식을 완성한 후 **확인**을 클릭합니다.

데이터 탐색기는 새 데이터베이스 및 컬렉션을 보여줍니다. 