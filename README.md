---
### 서비스 설명
ChatGPT로 질의응답 및 DALLE.2 모델기반 그림을 그려주는 AI 챗봇

<p align="center">
	<img alt="image" src="https://github.com/i-am-shuan/LLM-Kakao-ChatBot/assets/161431602/25894ccf-c504-4905-a10f-41ec91c3f557" width="35%" height="35%">
</p>

<p align="center">
	<img alt="image" src="https://github.com/i-am-shuan/LLM-Kakao-ChatBot/assets/161431602/cf42b778-e8f2-4d97-a282-639f49825b0e" width="35%" height="35%">
</p>


✅ service spec
- aws lambda, aws api gateway, kakao api
- langchain, gpt-3.5-turbo, gpt-DALL.E 2

---
### 서비스 사용방법
- GPT에게 질문하기
  - 명령어: /ask
  - 예시: /ask 오늘 서울의 날씨를 알려줘.
- DALL-E에게 이미지 작성 요청하기
  - 명령어: /img
  - 예시: /img Draw a delicious hamburger.
  - ⚠️ 유의사항
    - 이미지 생성
      - 소스에서 사용한 DALL·E 모델은 한국어를 학습하지 않습니다. 정확한 답변을 받으려면 영어로 질문해 주세요 🙏
    - 휴식 안내 문구
      - 카카오의 정책에 따라 잠시 휴식을 취하겠습니다. 조금 후에 아래의 말풍선을 클릭해 주세요 :)
      - kakao 정책으로 응답시간이 5초 이상 걸리는 통신에 대해서는 차단하고, 이외의 정책사항으로 프로그램 내에서 답변 생성시간을 3.5초로 설정하고 있습니다.
      - 이에 3.5초 이내에 받아오지 못한 응답에 대해서는, 먼저 사용자에게 [휴식을 취하고 있어요] 라는 메세지를 노출하고, 이후에 GPT로 응답받은 결과를 AWS 서버(/tmp/botlog.txt)에 저장하고
      - 일정 시간 이후, 사용자로부터 [답변해주세요] 메세지를 입력받으면 AWST 서버(/tmp/botlog.txt)을 확인하여 결과를 response 합니다. (이미지의 경우, DALLE로부터 이미지 URL 링크받아 botlog.txt에 저장합니다.)
 
---
### 서비스 흐름도
- 사용자가 kakao 채팅방에 질문 입력
- AWS API GW > AWS Lambda 잘문 전송
- AWS Lambda로 전달하여 내용을 분석
- ChatGPT 또는 DALL.E2 에게 질문하는건지 판단하여 OpenAI API 호출
- 요청 정보의 답변을 받은 lambda는 kakao API를 활용하여 kakao 채팅방으로 전송

<p align="center">
	<img alt="image" src="https://github.com/i-am-shuan/LLM-Kakao-ChatBot/assets/161431602/cedbf6fe-cfb2-4190-a3e7-fb8128ebbf2a" width="70%" height="70%">
</p>

---
### Sample Welcome Message
000에 오신 걸 환영해요! 🎉

1. 무엇을 도와드릴까요? 🤔
- 여러분이 궁금한 것이 있으면, ChatGPT 3.5 터보가 대답해 드려요. 💬 그리고 멋진 그림이 필요하다면, DALLE.2라는 마법의 그림 친구가 그려줄 거예요. 🎨

2. 어떻게 사용하나요?
- 질문하기: /ask
/ask 오늘 서울 날씨 어때?

- 그림 그려달라고 부탁하기: /img
/img Draw a delicious hamburger.

⚠️ 그림 친구 DALL·E는 한국어를 몰라요. 영어로 말해 줘야 정확하게 알아들어요 :)

---
### p.s. 서비스 확대
Kakao 비즈니스(https://business.kakao.com) 서비스를 활용하여 서비스를 고도화할 수 있다.
- 지식베이스: 자주 묻는 질문, 답변 효율적으로 관리
- 지식 업로드: RAG
  - RAG(Retrieval-Augmented Generation)는 대규모 언어 모델(LLM)에서 사용되는 기술로, 특정 질문에 대한 답변을 생성하기 위해 외부 문서나 데이터베이스에서 관련 정보를 검색(retrieve)하여 그 결과를 활용해 답변을 생성(generate)하는 과정을 말합니다. 이 방식을 문서 기반 RAG 서비스로 활용하는 경우, 사용자는 자신이 가진 문서를 시스템에 업로드합니다. 그러면 시스템이 이 문서들을 데이터베이스화하여, 사용자의 질문이 들어올 때 관련된 문서를 검색하여 그 내용을 바탕으로 정확하고 상세한 답변을 생성할 수 있게 됩니다.
  - 간단히 말해서, 문서 기반의 RAG 서비스는 사용자가 제공한 문서를 기반으로 질문에 대한 답변을 더 잘 찾아내고 생성할 수 있게 해주는 스마트한 방법입니다. 이를 통해, 사용자는 자신의 데이터를 활용하여 보다 정확하고 맞춤화된 정보를 얻을 수 있습니다.


