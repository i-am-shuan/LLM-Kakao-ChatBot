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
  - ⚠️ 유의사항: 소스에서 사용한 DALL·E 모델은 한국어를 학습하지 않습니다. 정확한 답변을 받으려면 영어로 질문해 주세요 🙏

---
### 서비스 흐름도
- 사용자가 kakao 채팅방에 질문을 입력
- 텔레그램 서버 > ngrok > 로컬PC 서버 > OpenAI API > ChatGPT / DALL.E2
- AWS API GW로 전송된 대화는 lambda로 전달하여 내용을 분석한다
- ChatGPT 또는 DALL.E2 에게 질문하는건지 판단하여 OpenAI API를 호출한다. 
- 요청 정보의 답변을 받은 lambda는 kakao API를 활용하여 kakao 채팅방으로 전송한다.

<p align="center">
	<img alt="image" src="https://github.com/i-am-shuan/LLM-Kakao-ChatBot/assets/161431602/cedbf6fe-cfb2-4190-a3e7-fb8128ebbf2a" width="70%" height="70%">
</p>

---

### Welcome Message
000에 오신 걸 환영해요! 🎉

1. 무엇을 도와드릴까요? 🤔
- 여러분이 궁금한 것이 있으면, ChatGPT 3.5 터보가 대답해 드려요. 💬 그리고 멋진 그림이 필요하다면, DALLE.2라는 마법의 그림 친구가 그려줄 거예요. 🎨

2. 어떻게 사용하나요?
- 질문하기: /ask
/ask 오늘 서울 날씨 어때?

- 그림 그려달라고 부탁하기: /img
/img Draw a delicious hamburger.

⚠️ 그림 친구 DALL·E는 한국어를 몰라요. 영어로 말해 줘야 정확하게 알아들어요 :)

