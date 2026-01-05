# 작업 중입니다.

# Azure SQL Database의 CDC를 이용하여 Real time intelligence 환경 구축하기

## 배경


일반적으로 Azure SQL Database와 같은 관계형 데이터베이스의 데이터를 클라우드 레이크하우스로 가져오는 방법은 **과거 지향적 접근 방법**을 사용하곤 합니다.

간단하게 설명하면, 주기적으로 정해진 시간에 쿼리를 하여 변경된 데이터들을 가져오는 방법을 의미합니다.

예를 들면, Data Factory를 이용하여 변경된 데이터의 내용을 읽어와서 레이크하우스로 복사하는 것이 이에 해당 합니다.

<img src='https://learn.microsoft.com/en-us/fabric/data-factory/media/copy-job/monitor-copy-job.png#lightbox'>

이 작업은 매일, 또는 6시간마다, 혹은 3시간마다 수행되도록 할 수 있지만, 데이터가 원본(source)에서 생성되는 순간부터 레이크하우스에 도달하기까지 많은 시간을 필요로 하게 됩니다.

데이터로부터 좀 더 의미있는 정보와 인사이트를 이끌어내기 위해서는, 가장 최신의 데이터가 유지되는 것이 필요합니다.

따라서, 데이터를 주기적으로 **가져오기(pull)** 보다는, 원본(source)에서 **실시간**으로, **upstream(여기서는 Microsoft Fabric)** 으로 **올려(push)** 주어야 합니다.

## 아키텍처
이번 hands-on lab에서는 Azure SQL Database의 CDC 기능을 이용하여 변경된 데이터를 Microsoft Fabric으로 실시간으로 가져오는 방법에 대해서 살펴보게 됩니다.

<img src='./images/batch-2-rti-azure-sql-db-flow.png'>

## 순서
1. Azure SQL Database 생성
2. Azure SQL Database 구성
    - SQL Database 서버 설정
    - CDC 활성화
    - 데이터베이스 사용자 생성
    - 테이블 생성
3. 데이터 시뮬레이터 노트북 생성 + 테스트
4. 이벤트하우스 생성
5. 이벤트스트림 생성
6. 이벤트스트림 구성
    - Azure SQL Database 연결
    - 이벤트스트림과 이벤트하우스 연결
7. KQL을 이용한 데이터 확인

## 1. Azure SQL Database 생성
[Azure Portal](https://portal.azure.com/)에 로그인하고, Create a resource 버튼을 클릭합니다.

<img src='./images/batch-2-rti-azure-sql-db-create-a-resource.png'>

검색창에 'Azure SQL Database'를 입력하여 리소스를 검색합니다.

<img src='./images/batch-2-rti-azure-sql-db-create-a-resource-sql-db.png'>

결과 화면에서 'SQL Database'의 'Create' > 'SQL Database' 버튼을 클릭합니다.

<img src='./images/batch-2-rti-azure-sql-db-create-a-resource-sql-db-create.png'>

구독과 리소스 그룹을 선택합니다.
그 다음에는 데이터베이스 이름을 입력하고, 

<img src='./images/batch-2-rti-azure-sql-db-create-a-resource-sql-db-create-basic.png'>

필요하면, Server의 'Create New' 버튼을 클릭하여 데이터베이스 서버를 생성합니다.

<img src='./images/batch-2-rti-azure-sql-db-create-a-resource-sql-db-create-dbsvr.png'>

Workload environment는 'Development'로 설정하고, 'Review + create' 버튼을 클릭하여 생성합니다.

<img src='./images/batch-2-rti-azure-sql-db-create-a-resource-sql-db-create-db.png'>

## 2. Azure SQL Database 구성

### SQL Database 서버 설정
### CDC 활성화
### 데이터베이스 사용자 생성
### 테이블 생성


