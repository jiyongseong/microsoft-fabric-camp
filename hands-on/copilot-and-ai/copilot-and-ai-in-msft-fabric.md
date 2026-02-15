# Microsoft Fabric의 Copilot과 AI 기능
Microsoft Fabric은 데이터 플랫폼이지만, 단순히 데이터를 저장하고 처리하는 역할을 넘어서, "데이터로 일하는 사람들의 업무 방식" 자체를 바꾸려는 방향으로 끊임없이 진화하고 있습니다. 

그 변화의 한가운데 서 있는 것이 바로 **Copilot과 AI 지원(AI assistance) 기능들** 입니다.

이번 글에서는, 앞으로 이어질 hands-on 시리즈(데이터 엔지니어링/데이터 사이언스/데이터 팩토리/웨어하우스/SQL DB/Power BI/Real-Time Intelligence)를 시작하는 글로, Fabric에서 Copilot과 AI 기능이 무엇이고, 어디에 있고, 어떤 식으로 도움을 주는지를 살펴보도록 하겠습니다.

## Fabric의 Copilot
쉽게 말하면, Fabric의 Copilot은 Fabric 안에서 데이터 작업을 할 때 옆에서 도와주는 생성형 AI 비서라고 할 수 있습니다. "자연어로 말하면 코드/쿼리/변환/리포트 초안을 만들어주고, 설명도 해주고, 막힌 부분을 풀어주는" 역할을 합니다.

중요한 포인트는 "Copilot이 Fabric의 모든 화면에서 똑같이 동작한다"가 아니라, **워크로드(workload)별로 '잘하는 일이 조금씩 다르다'** 는 점입니다. Fabric에는 여러 워크로드가 있고, Copilot은 그 흐름(수집→변환→분석/ML→시각화→실시간)에 맞춰 각자 다른 방식으로 기능이 제공됩니다. 

예를 들면,

- 데이터 엔지니어링/데이터 사이언스에서는 노트북에서 코드를 만들어주거나, 디버깅/문서화/시각화를 도와줍니다.
- Data Factory에서는 Dataflow Gen2나 파이프라인에서 변환 단계(M 코드) 만들기/설명/요약/오류 해결 같은 "ETL 작업"을 자연어로 끌어갈 수 있게 해줍니다
- Power BI에서는 "보고서 페이지를 한 번에 초안으로 만들어주고", "내러티브(요약)를(을) 만들고", "Q&A 동의어도 생성"해줍니다. 
- Real-Time Intelligence에서는 질문을 KQL 쿼리로 바꿔주는 식으로, 실시간/이벤트 데이터 탐색을 도와줍니다.
- SQL database/웨어하우스에서는 SQL 편집기에서 자연어→SQL, 코드 자동완성, Explain/Fix 같은 빠른 액션으로 쿼리를 더 빨리/안전하게 만들수 있도록 도와줍니다.

요약하면, **"Copilot은 Fabric의 분석 여정(Analytics Journey) 전체를 더 빠르게 굴리게 해주는 생산성 엔진"** 이라고 보면 됩니다.

## Copilot의 가치
초보자 관점에서 Copilot의 가장 큰 가치는, 뭘 어떻게 해야할지 모를 때 일을 시작할 수 있게 해준다는 겁니다.

예를 들어 Data Factory에서 "이 데이터에서 국가가 'KR'인 것만 남겨줘", "도시별 직원 수 세어줘" 같은 문장을 던지면, Copilot이 그걸 실제 변환 단계로 만들어주고(그리고 필요하면 되돌리기도) 작업 흐름을 이어갈 수 있게 해줍니다.

노트북에서도 비슷합니다. 데이터프레임을 불러왔는데 "이 데이터 뭐가 문제인지?", "아웃라이어 제거하고 싶어", "이 컬럼들로 히트맵 그려줘" 같은 요청을 하면, Copilot이 코드를 써주고 왜 그렇게 했는지 설명까지 붙여줍니다. 데이터프레임 생성부터 EDA, 시각화, 이상치 제거, 저장까지 흐름이 '대화'로 이어집니다.

Power BI에서는 더 직관적입니다. "이 데이터로 고객 분석 페이지 만들어줘" 같은 한 문장으로 보고서 페이지 초안을 뽑아주고, 리포트를 읽는 사람을 위해 내러티브 요약도 만들어줍니다. 그리고 Q&A 동의어까지 자동으로 제안해주니, 모델/리포트 완성도를 끌어올릴 때 꽤 유용합니다.

## Copilot은 어디에 있나?
Fabric에서 Copilot이 지원되는 기능은 다음과 같습니다.

<img src="https://learn.microsoft.com/ko-kr/fabric/fundamentals/media/copilot-fabric-overview/fabric-items-copilot-support.svg" alt="Copilot in Fabric 개요 다이어그램">

그림에서 볼 수 있는 것처럼, Copilot은 Fabric의 여기저기에 심어져 있습니다.
각 항목별로 지원되는 Copilot의 기능도 다음과 같이 정리되어 있습니다.

[Where to find the AI and Copilot experiences in Fabric](https://learn.microsoft.com/en-us/fabric/fundamentals/copilot-fabric-overview#where-to-find-the-ai-and-copilot-experiences-in-fabric)

## AI 기능
Fabric에는 Copilot 외에도 Data agent, AI Functions, Operations Agent와 같은 AI 기능들을 추가적으로 제공합니다.

- **Fabric data agent**는 Lakehouse/Warehouse/Power BI semantic model/KQL DB 같은 데이터 자산을 바탕으로, "자연어 질문→답"을 더 구조적으로 제공하도록 설계된 기능입니다. 그리고 Microsoft 365 Copilot이나 Copilot Studio에서 "연결된 에이전트" 형태로 소비할 수 있습니다.

- AI functions는 데이터프레임을 요약/분류/텍스트 생성 같은 방식으로 "한 줄" 호출로 처리하는 방향의 기능입니다.

- IQ 쪽에서는 Operations Agent처럼 실시간 데이터 기반으로 상태를 모니터링하고 권장 조치를 제안하는 "운영형 에이전트" 기능도 제공됩니다.

이런 것들을 한데 묶어 보면, Fabric이 가려는 방향은 꽤 명확합니다.

    데이터 플랫폼(OneLake) 위에서, 사람은 자연어로 의도를 말하고, AI는 코드/쿼리/리포트/액션 초안을 만들어준다.

✍️ 2026년 2월 13일 씀.