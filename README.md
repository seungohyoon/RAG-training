# RAG-training
25년 8월 RAG교육

1. 프로젝트 배경
   - '24년 모 렌터카 업체 챗봇 프로젝트 참여 => 고객사 요청으로 LLM을 배재한 NLU 챗봇 구축
   - 실제 구현된 챗봇: https://www.skdirect.co.kr/ , https://www.lotterentacar.net/hp/kor/cs/faq/list.do
   - 제한적인 답변 능력과 intent 가중치 조절 실패로 인한 오답을 LLM은 극복 가능할 것이라 생각
     ex) "반려동물 이용"이라는 문의 입력시 '이용' 중심으로 intent를 이해해 오답 제공

2. 프로젝트 구조
<img width="2254" height="1869" alt="SKRC RAG구조" src="https://github.com/user-attachments/assets/26729e76-3331-4b92-a92a-d826a557f7a7" />

3. 작성 과정
   - 하나의 문서가 아닌 여러 하위 페이지로 구성된 FAQ문서 스크래핑 실패 >> 수동 copy&paste
   - Vector DB: Chroma DB 활용 (소규모 구성에 적합한 파일 구조를 가지고 있음)
   - Ensemble Retriever 가중치: 0.3:0.7(vector검색 가중치) >> 0.5:0.5로 수정 시 특정 단어에 의해 검색결과 왜곡
   - Relevance Test를 통한 필터링 & top n 채택: 본 챗봇에서는 영향 없음
   - 시스템 프롬프팅
       당신은 SK렌터카의 친절한 고객 상담원입니다.
        1) 명확한 근거가 없으면 "근거없음"으로 답변하세요
        2) 답변하기 어려운 질문은 "잘 모르겠습니다"라고 대답하세요
        3) 추측이나 일반적인 지식을 이용하지 마세요
        4) 참조 문서의 내용만을 바탕으로 답변하세요
        5) 답변은 한국어로 작성하고, 필요시 구체적인 예시를 포함하세요

4. 시연

5. 후기
   - 동작 하는 챗봇을 만들어낸 스스로가 대견함: many thanks to 강사님 & chat GPT
   - 챗봇의 품질에 가장 중요한 요소는 원본 Data의 완결성 -> 기획단계가 매우 중요
