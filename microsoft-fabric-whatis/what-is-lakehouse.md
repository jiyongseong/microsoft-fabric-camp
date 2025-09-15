## WHAT IS - 레이크하우스

레이크하우스는 비교적 최근에 등장한 개념으로, 데이터 웨어하우스와 데이터 레이크의 장점을 결합한 구조입니다.

이 개념은 스토리지와 컴퓨팅의 분리에서 시작됐습니다. 예전 Hadoop, Hive 시절에는 파일 시스템에 데이터를 저장하고 그 위에서 쿼리를 실행했죠. 이후 테이블과 데이터베이스를 만들고, 스냅샷을 저장하거나 덮어쓰고 추가하는 기능이 발전했습니다.

최근에는 ACID 트랜잭션 같은 관계형 DB 수준의 기능을 데이터 레이크에서도 제공하는 도구들이 등장했습니다. 즉, 스토리지와 컴퓨팅을 분리하면서도 트랜잭션 일관성을 유지하고, 여러 사용자가 동시에 읽고 쓸 수 있는 환경을 제공합니다.

Fabric에서의 레이크하우스는 파일, 폴더, 테이블을 포함하는 아티팩트로, 데이터 엔지니어링 환경에서 관리됩니다.

이때 Delta Lake라는 오픈소스 테이블 포맷을 표준으로 사용하며, Spark 엔진이나 Dataflow Gen2를 통해 데이터를 작성합니다.

### ✅ 웨어하우스와의 차이점
Fabric의 웨어하우스는 T-SQL 기반으로 관리되며, 풍부한 SQL 기능을 제공합니다.

반면 레이크하우스는 Spark나 Dataflow를 통해 관리되고, 파일 기반 스토리지 위에 Delta 테이블을 얹는 구조입니다.

두 아티팩트 모두 OneLake를 기반으로 하지만, 관리 방식과 쿼리 언어가 다릅니다.

### ✅ 레이크하우스 구조
- Files 영역: 원본 파일, 참조 파일 등 비정형 데이터를 저장.
- Tables 영역: 데이터를 Delta 테이블에 저장. Spark Notebook, Job, Dataflow Gen2를 이용하여 생성.

<img src="https://learn.microsoft.com/en-us/fabric/data-engineering/media/lakehouse-overview/lakehouse-overview.gif" style="width:80%;">

