# RAG를 활용한 LLM Application 개발 (feat. LangChain)

> [pyenv 설치](https://javaexpert.tistory.com/1056) 

</br> 

## 🦜🔗 LangChain과 흐름 
### 1) Docx 로더 :  [Docx2txtLoader](https://python.langchain.com/docs/integrations/document_loaders/microsoft_word)
`.docx` 파일을 Langchain의 Document로 읽어와서 사용할 수 있도록 해줌 

### 2) 텍스트 분할 : [RecursiveCharacterTextSplitter](https://python.langchain.com/docs/how_to/recursive_text_splitter)
긴 문서를 청크로 쪼개야 토큰 초과를 피하고 검색 적중률도 높아지기 때문에 RecursiveCharacterTextSplitter를 활용하여 문단 -> 문장 -> 단어 순으로 최대한 의미 단위를 보존하면서 자른다. 

### 3) 임베딩 : [OpenAIEmbeddings](https://python.langchain.com/api_reference/openai/embeddings/langchain_openai.embeddings.base.OpenAIEmbeddings.html)
텍스트를 벡터로 변환해 벡터 db에서 유사도 검색이 가능하게 만든다. 

### 4) 벡터 DB 
- 로컬 : [Chroma](https://www.trychroma.com)
- 클라우드 : [Pinecone](https://app.pinecone.io/)

### 5) Retriever 설계 : [Retriever](https://python.langchain.com/docs/how_to/vectorstore_retriever/)
벡터 DB에 '이 질문이랑 가장 비슷한 문서 조각 몇 개를 줘' 라고 부탁하는 역할

### 6) 프롬프트 & 응답 포맷 : [Prompt Templates](https://python.langchain.com/docs/concepts/prompt_templates/)
가져온 문서 조각들을, 모델이 이해하기 쉬운 일관된 틀에 넣는 것

</br> 

> [노션](https://erika0915.tistory.com/entry/RAG-RAG를-사용한-LLM-Application-개발)
