# Power BI의 Copilot 기능 

## TL;DR
* Power BI의 Copilot이란?
    Microsoft Fabric의 Power BI에 내장된 AI 기반 데이터 분석 도우미입니다. 자연어로 질문하거나 요청하면, 데이터를 자동으로 분석하고 적절한 보고서나 시각화를 생성해줍니다.

* 핵심 기능
    주요 기능은 자연어 보고서 생성, 보고서 요약(내러티브) 작성, 데이터 Q&A 등입니다. 초보자도 손쉽게 데이터에서 통찰을 얻고 시각화할 수 있도록 도와줍니다.

* Hands-on 예제
    [Lab2 Lakehouse 환경](/microsoft-fabric-in-a-day/Lab2%20Microsoft%20Fabric%20Lakehouse/Lab2%20Microsoft%20Fabric%20Lakehouse1.md)의 샘플 데이터를 활용하여, Copilot에 자연어 명령을 입력해 자동 리포트 생성 및 요약 생성을 실습합니다. 몇 단계만 거치면 차트가 포함된 보고서와 요약 결과를 얻을 수 있습니다.

## Microsoft Fabric Power BI Copilot 개요
Microsoft Fabric Power BI의 Copilot은 **생성형 AI(Generative AI) 기술** 을 기반으로 하는 데이터 분석 보조 도구입니다. 마치 팀원의 협업자(Copilot)처럼, 자연어 채팅 인터페이스를 통해 사용자의 질문이나 요청을 이해하고, 데이터 준비부터 분석, 보고서 작성까지 다양한 업무를 도와줍니다. 복잡한 코딩이나 수식을 일일이 쓰지 않아도, 일상 언어로 묻고 답하며 원하는 정보를 얻을 수 있습니다.

Copilot은 **Power BI 서비스 및 Desktop에 통합되어 동작**하며, 데이터 분석 경험을 크게 향상시키도록 설계되었습니다. **대규모 언어 모델(LLM)** 을 활용하여 사용자가 입력한 자연어 질문을 이해하고 적절한 응답(차트, 요약, 분석 등)을 생성합니다. 이를 통해 비기술자도 데이터에 쉽게 접근할 수 있고, 데이터 전문가도 반복 작업을 자동화하여 분석 업무를 효율화할 수 있습니다.

**주요 기능**으로는 크게 세 가지를 들 수 있습니다: 

* **자연어를 통한 보고서 페이지 생성**: 원하는 분석 내용을 문장으로 설명하면 Copilot이 알맞은 차트와 시각요소들로 구성된 리포트 페이지를 자동 생성해줍니다. 

* **자동 요약 및 내러티브 생성**: Copilot이 보고서 페이지 또는 특정 시각화의 핵심 인사이트를 자연어로 요약해주며, **내러티브(설명문)** 를 생성합니다.

* **데이터 Q&A(질의 응답) 지원**: 사용자는 평소 말하듯이 궁금한 점을 질문하면 Copilot이 데이터를 조회하여 답변하거나 관련 차트를 보여줍니다. 또한 데이터 모델에 동의어(synonym)를 추가해 사용자의 질문을 더 잘 이해하도록 도와줍니다.

아래에서는 이러한 기능들을 초보자도 따라할 수 있는 실습 예제와 함께 하나씩 살펴보겠습니다. 

예제는 [Lab 2: Lakehouse 환경](https://github.com/jiyongseong/microsoft-fabric-camp/blob/main/microsoft-fabric-in-a-day/Lab2%20Microsoft%20Fabric%20Lakehouse/Lab2%20Microsoft%20Fabric%20Lakehouse1.md)에서 제공된 샘플 판매 데이터셋을 활용합니다. 이 Lab을 통해 이미 OneLake의 Lakehouse에 판매 데이터를 적재하고 시맨틱 모델까지 구성했다고 가정하고, Copilot으로 이 데이터를 바로 분석해보겠습니다. 

## Power BI의 Copilot 기능 Hands-on
[Hands-on 바로가기](copilot-pbi-create-report.md)

✍️ 2026년 2월 27일 씀.