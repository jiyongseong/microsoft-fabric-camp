Lab 3에서는 다음과 같은 내용들을 살펴봅니다.

# 3.0 Microsoft Fabric의 Data Warehouse란?
데이터 분석은 lab2에서 살펴본 레이크 중심의 접근 방식으로 전환되고 있지만. 여전히 전통적인 데이터 웨어하우스(Data Warehouse)가 적합한 시나리오가 여전히 다수 존재합니다.

오래 기간 축적된 SQL 기술을 보유하고 있다면, 데이터 웨어하우스 개발에 쉽게 적용될 수 있으며,
기업용의 데이터 레이크나 레이크하우스가 다양한 부서에서 구축한 다운스트림 데이터 웨어하우스로 데이터를 제공하기도 합니다. 
이 웨어하우스들은 메달리온 아키텍처에서 **골드 레이어** 역할을 합니다.

반면, 일부 소규모 조직에서는 데이터가 대부분 관계형 데이터 소스에서 중앙 집중화되기 때문에, 레이크하우스를 도입하는 추가적인 복잡성이 필요하지 않을 때도 있습니다.

# 3.1 데이터 흐름
이번 lab3에서는 **데이터 수집(Ingestion)**, **변환(Transformation)**, **보고(Reporting)**를 포함하는 솔루션을 구축하면서 **Fabric 데이터 웨어하우스의 핵심 기능**에 대해서 살펴봅니다.

이번 lab에서는 Wide World Importers(WWI) 예제 데이터베이스를 사용합니다. 데이터 모델에 대한 자세한 설명은 [여기](../Lab2%20Microosft%20Fabric%20Lakehouse/Lab2%20Microosft%20Fabric%20Lakehouse1.md#22-예제-데이터-개요)를 참고하시기 바랍니다.

데이터의 흐름은 다음과 같습니다.

<img src="./images/onelake-medallion-datawarehouse-architecture-example.png" style="width:80%;" alt="create-silver-lakehouse">


## Ingestion
해당 단계에서는 데이터 원본에 있는 3개의 테이블의 데이터를 가져오기 하게 됩니다. 
- 하나는 Data Factory에서 제공하는 예제 데이터셋을
- 나머지 두 개는 다른 Azure Data Lake Storage(ADLS) 계정에 저장되어 있는 Parquet 파일로부터 데이터셋을 
가져오기 하게 됩니다.

Data Factory copy activity와 T-SQL을 이용하여 데이터를 가져오기 하게 됩니다.

실제 환경에서는 데이터가 다양한 소스에서 공통 데이터 레이크로 들어온 후, T-SQL을 사용하여 웨어하우스로 로드되는 경우가 일반적입니다. 그러나 일부 소규모 솔루션이나 부서별 웨어하우스 솔루션의 경우에는, Data Factory 복사 작업(copy activity)을 이용하여 웨어하우스로 직접 가져오는 경우도 있습니다.

## Transform
데이터 웨어하우스에서 데이터를 변환하는 작업은 변환 시점에 따라서 나눌 수 있습니다.

- 수집 후 : 이미 메달리온 아키텍처의 절차를 통해서 데이터가 정리되어 있다면, 일반적으로 **T-SQL Copy 명령이나 저장 프로시저** 등을 활용하여 추가 데이터 변환을 수행
- 수집 시 : 데이터 레이크가 없이 데이터가 바로 데이터 웨어하우스로 들어오면서 일부 변환이 필요한 경우에는 **Dataflow Gen2**를 이용하여 데이터 변환을 수행

## Analyze
Lab3에서도 분석 단계는 Power BI와 SQL endpoint를 이용하게 됩니다.
Power BI에서는 Direct Lake 모드(Direct Lake mode)를 이용하여 **데이터 모델 새로 고침** 방법에 대해서 살펴봅니다.

# 3.2 데이터 웨어하우스 만들기
Microsoft Fabric 포털에서 좌측 메뉴에서 **작업 영역**을 클릭하고, 화면에서 앞서 생성한 **Hands on workspace**를 선택합니다.

<img src="../Lab2 Microosft Fabric Lakehouse/images/handson-workspace.png" style="width:50%;" alt="handson-workspace">

작업 영역 화면에서, 좌측 상단에 있는 **+ 새 항목** 버튼을 클릭하여, **새 항목 > 데이터 저장 > 레이크하우스**를 클릭합니다.

<img src="./images/create-warehouse.png" style="width:80%;" alt="create-warehouse">

**새 웨어하우스** 화면에서는 웨어하우스 이름을 "wwi_dw"라고 입력하고, **만들기** 버튼을 클릭하여 새로운 웨어하우스를 생성합니다.

<img src="./images/new-warehouse.png" style="width:60%;" alt="new-warehouse">

생성이 완료되면, 웨어하우스 랜딩 페이지가 보여지게 됩니다.

<img src="./images/warehouse-landing-page.png" style="width:80%;" alt="warehouse-landing-page">