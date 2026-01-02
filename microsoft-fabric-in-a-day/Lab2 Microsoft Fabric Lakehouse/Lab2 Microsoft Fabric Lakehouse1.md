# 목차
Lab 2에서는 다음과 같은 내용들을 살펴봅니다.

- [2.0 Microsoft Fabric의 Lakehouse란?](#20-microsoft-fabric의-lakehouse란)
- [2.1 메달리온 아키텍처](#21-메달리온-아키텍처)
- [2.2 예제 데이터 개요](#22-예제-데이터-개요)
- [2.3 브론즈(Bronze) 단계](Lab2%20Microsoft%20Fabric%20Lakehouse2.md#23-브론즈bronze-단계) 
    - [2.3.1 브론즈 레이크하우스 만들기](Lab2%20Microsoft%20Fabric%20Lakehouse2.md#231-브론즈-레이크하우스-만들기)
    - [2.3.2 데이터 파이프 라인 만들기](Lab2%20Microsoft%20Fabric%20Lakehouse2.md#232-데이터-파이프-라인-만들기)
    - [2.3.3 데이터 파이프 라인 실행하기](Lab2%20Microsoft%20Fabric%20Lakehouse2.md#233-데이터-파이프-라인-실행하기)
- [2.4 실버(Silver) 단계](Lab2%20Microsoft%20Fabric%20Lakehouse3.md#24-실버silver-단계)
    - [2.4.1 실버 레이크하우스 만들기](Lab2%20Microsoft%20Fabric%20Lakehouse3.md#241-실버-레이크하우스-만들기)
    - [2.4.2 바로 가기(Shortcut) 만들기](Lab2%20Microsoft%20Fabric%20Lakehouse3.md#242-바로-가기shortcut-만들기)
    - [2.4.3 노트북(notebook) 만들기](Lab2%20Microsoft%20Fabric%20Lakehouse3.md#243-노트북notebook-만들기)
    - [2.4.4 데이터 변환 - 차원(dimension) 테이블](Lab2%20Microsoft%20Fabric%20Lakehouse3.md#244-데이터-변환---차원dimension-테이블)
    - [2.4.5 데이터 변환 - 팩트(fact) 테이블](Lab2%20Microsoft%20Fabric%20Lakehouse3.md#245-데이터-변환---팩트fact-테이블)
- [2.5 골드(Gold) 단계](Lab2%20Microsoft%20Fabric%20Lakehouse4.md#25-골드gold-단계)
    - [2.5.1 골드 레이크하우스 만들기](Lab2%20Microsoft%20Fabric%20Lakehouse4.md#251-골드-레이크하우스-만들기)
    - [2.5.2 바로 가기(Shortcut) 만들기](Lab2%20Microsoft%20Fabric%20Lakehouse4.md#252-바로-가기shortcut-만들기)
    - [2.5.3 노트북(notebook) 만들기](Lab2%20Microsoft%20Fabric%20Lakehouse4.md#253-노트북notebook-만들기)
    - [2.5.4 비지니스 집계 테이블 생성](Lab2%20Microsoft%20Fabric%20Lakehouse4.md#254-비지니스-집계-테이블-생성)
        - [2.5.4.1 PySpark를 이용한 집계 테이블 생성](Lab2%20Microsoft%20Fabric%20Lakehouse4.md#2541-pyspark를-이용한-집계-테이블-생성)
        - [2.5.4.2 SparkSQL을 이용한 집계 테이블 생성](Lab2%20Microsoft%20Fabric%20Lakehouse4.md#2542-sparksql을-이용한-집계-테이블-생성)
- [2.6 분석 단계](Lab2%20Microsoft%20Fabric%20Lakehouse5.md#26-분석-단계)
    - [2.6.1 SQL analytics endpoint](Lab2%20Microsoft%20Fabric%20Lakehouse5.md#261-sql-analytics-endpoint)
    - [2.6.2 Power BI](Lab2%20Microsoft%20Fabric%20Lakehouse5.md#262-power-bi)
    - [2.7 요약](Lab2%20Microsoft%20Fabric%20Lakehouse5.md#27-요약)

⚠️ 해당 lab은 [Lakehouse end-to-end scenario: overview and architecture](https://learn.microsoft.com/en-us/fabric/data-engineering/tutorial-lakehouse-introduction)의 내용을 기반으로 하였습니다.

# 2.0 Microsoft Fabric의 Lakehouse란?
Microsoft Fabric의 [레이크하우스(lakehouse)](../../microsoft-fabric-whatis/what-is-lakehouse.md)는 조직이 정형 데이터(structured data), 반정형 데이터(semi-structured data), 비정형 데이터(unstructured data) 등 사실상 모든 유형의 데이터를 단일 위치에 저장하고 관리할 수 있도록 하는 데이터 저장 계층(data storage layer)입니다.

이를 통해 다양한 도구와 프레임워크가 조직의 요구 사항 또는 개인의 선호에 따라 이러한 데이터를 처리하고 분석할 수 있습니다.

레이크하우스(lakehouse)는 데이터 레이크와 데이터 웨어하우스의 장점을 결합하여, 기업 데이터의 중복성(duplicity)과 데이터 수집(ingesting), 변환(transforming), 공유(sharing) 과정에서 발생하는 문제를 해결할 수 있습니다.

수집된 데이터는 기본적으로 델타 레이크(Delta Lake) 형식([https://delta.io/](https://delta.io/))으로 레이크하우스에 저장되며, 테이블은 사용자 대신 메타스토어(metastore)에 자동으로 검색 및 등록되어 Microsoft Fabric 내 모든 엔진에서 원활하게 작업할 수 있도록 제공합니다.

# 2.1 메달리온 아키텍처

레이크하우스 기반의 데이터 분석 시스템(data analytics system)은 일반적으로 메달리온 아키텍처(Medallion architecture)([https://learn.microsoft.com/en-us/azure/databricks/lakehouse/medallion](https://learn.microsoft.com/en-us/azure/databricks/lakehouse/medallion), [WHAT IS - 메달리온 아키텍쳐 소개](../../microsoft-fabric-whatis/What-is-medallion-architecture.md))를 따릅니다. 

이 아키텍처는 브론즈(Bronze), 실버(Silver), 골드(Gold)라는 일련의 데이터 영역(data zones)을 정의하여, 각 단계에서 레이크하우스에 저장된 데이터의 품질을 나타내며, 엔터프라이즈 데이터 제품을 위한 단일 진실 공급원(single source of truth)을 구축하기 위해 다계층 접근 방식을 권장합니다.

예를 들어, 브론즈(Bronze), 실버(Silver), 골드(Gold)라는 용어는 각각 원시(raw), 검증(validated), 강화(enriched) 데이터로 불리기도 하며, 각 계층에서 데이터의 품질을 설명합니다.

<img src="./images/onelake-medallion-lakehouse-architecture-example.png" style="width:80%;" alt="onelake-medallion-lakehouse-architecture-example">

*이미지 소스 : [https://learn.microsoft.com/ko-kr/fabric/onelake/onelake-medallion-lakehouse-architecture#medallion-architecture-in-fabric](https://learn.microsoft.com/ko-kr/fabric/onelake/onelake-medallion-lakehouse-architecture#medallion-architecture-in-fabric)*

브론즈 레이크하우스를 생성하여 데이터를 적재하는 작업부터 시작해보겠습니다.

# 2.2 예제 데이터 개요
Microsoft Fabric in a Day hands-on labs에서는 Microsoft에서 제공하는 Wide World Importers(WWI) 예제 데이터베이스를 사용하게 됩니다.

예제 데이터에 대한 자세한 내용은 다음의 링크를 참고하시기 바랍니다.

[Wide World Importers sample databases for Microsoft SQL](https://learn.microsoft.com/en-us/sql/samples/wide-world-importers-what-is?view=sql-server-ver17)

예제 데이터베이스은 여러 개의 팩트 테이블(fact tables)과 관련된 차원 테이블(dimension tables)이 포함되어 있습니다.

이번 hands-on lab에서는 다음과 같이 단순화된 스타 스키마(Star schema)를 사용하게 됩니다.

- 팩트(Fact): Sale
- 차원(Dimension): Customer
- 차원(Dimension): Employee
- 차원(Dimension): City
- 차원(Dimension): Date
- 차원(Dimension): Stock Item

원본 데이터는 쉼표로 구분된 값(CSV, comma-separated values) 파일 형식으로, 파티션 되지 않은(un-partitioned) 구조를 가지고 있습니다.

## 다음

[Lab1 Microsoft Fabric Getting Started](../Lab1%20Microsoft%20Fabric%20Getting%20Started/Lab1%20Microsoft%20Fabric%20Getting%20Started.md) << Lab2 Microsoft Fabric Lakehouse - Overview >> [Lab2 Microsoft Fabric Lakehouse - 브론즈(Bronze) 단계](../Lab2%20Microsoft%20Fabric%20Lakehouse/Lab2%20Microsoft%20Fabric%20Lakehouse2.md)