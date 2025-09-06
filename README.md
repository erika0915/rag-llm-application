# RAG를 활용한 LLM Application 개발 (feat. LangChain)

> [pyenv 설치](https://javaexpert.tistory.com/1056) 

</br> 

## 🦜🔗 LangChain과 흐름 
### 1) Docx 로더 :  [Docx2txtLoader](https://python.langchain.com/docs/integrations/document_loaders/microsoft_word)
`.docx` 파일을 Langchain의 Document로 읽어와서 사용할 수 있도록 해준다. 

### 2) 텍스트 분할 : [RecursiveCharacterTextSplitter](https://python.langchain.com/docs/how_to/recursive_text_splitter)
긴 문서를 청크로 쪼개야 토큰 초과를 피하고 검색 적중률도 높아지기 때문에 RecursiveCharacterTextSplitter를 활용하여 문단 -> 문장 -> 단어 순으로 최대한 의미 단위를 보존하면서 자른다. 

### 3) 임베딩 : [OpenAIEmbeddings](https://python.langchain.com/api_reference/openai/embeddings/langchain_openai.embeddings.base.OpenAIEmbeddings.html)
텍스트를 벡터로 변환해 벡터 db에서 유사도 검색이 가능하게 만든다. 

### 4) 벡터 DB 
- 로컬 : [Chroma](https://www.trychroma.com)
- 클라우드 : [Pinecone](https://app.pinecone.io/)

### 5) [Retriever](https://python.langchain.com/docs/how_to/vectorstore_retriever) 설계
질문과 가장 유사한 청크 n개를 고른다. 

### 6) 프롬프트 준비 
[LangChain Hub](https://smith.langchain.com/hub/rlm/rag-prompt)에서 공개된 RAG 템플릿을 pull 해와서 사용한다. 

### 7) 체인 조립 (검색 -> 주입 -> 생성) : [RetrievalQA](https://python.langchain.com/api_reference/langchain/chains/langchain.chains.retrieval_qa.base.RetrievalQA.html) 
  
</br> 

## 🔍 질의 처리 단계  

1. 사용자의 자연어 질문 시작
2. 벡터 DB 검색 : 질문을 임베딩으로 바꿔, 벡터 DB에서 가장 유사한 상위 n개의 청크를 가져온다.
3. 프롬프트 준비 : LangChain Hub의 RAG 템플릿을 가져온다.
4. RetrievalQA 체인
   - Retrieval가 유사 청크를 찾고
   - 찾은 청크를 prompt의 {context}에 꽂고
   - LLM이 근거를 기반으로 답변을 생성한다.
  
<img width="600" height="400" alt="image" src="https://github.com/user-attachments/assets/9f246990-644e-4cd0-a737-f77edf94e486" />



</br> 

</br> 


## LLM 평가 파이프라인 (RAG + [LangSmith](https://www.langchain.com/langsmith))
LLM이 중요 질문에 제대로 답하는지 자동으로 평가하며, 단순히 답변만 보는 게 아니라 정확도, 유용성, 환각 여부까지 점검한다.  


1. 정답지 준비 : 도메인 전문가가 만든 질문-정답을 LangSmith에 저장
2. RAG 파이프라인 
3. 평가 (Evaluation) 
  - 정확도 : 기준 정답과 얼마나 일치하는가 ?
  - 도움됨 : 질문에 답변이 유용한가 ?
  - 환각 : 제공된 문서 밖의 내용을 꾸며냈는가 ?
4. 리포트 확인 : LangSmith 대시보드에서 점수와 결과 비교 가능 

</br> 

> [정리](https://erika0915.tistory.com/entry/RAG-RAG를-사용한-LLM-Application-개발)
