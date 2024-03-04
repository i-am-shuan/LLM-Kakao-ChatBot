
---

### 서비스 설명
ChatGPT로 질의응답 및 DALLE.2 모델기반 그림을 그려주는 AI 챗봇
 
<p align="center">
	<img alt="image" src="https://github.com/i-am-shuan/LLM-Kakao-ChatBot/assets/161431602/25894ccf-c504-4905-a10f-41ec91c3f557" width="35%" height="75%">
</p>

<p align="center">
	<img alt="image" src="https://github.com/i-am-shuan/LLM-Kakao-ChatBot/assets/161431602/cf42b778-e8f2-4d97-a282-639f49825b0e" width="35%" height="75%">
</p>

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

- skill set:
  - aws lambda, aws api gateway, kakao api
  - langchain, gpt-3.5-turbo, gpt-DALL.E 2


---
