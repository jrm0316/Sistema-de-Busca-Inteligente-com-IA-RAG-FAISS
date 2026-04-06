# Sistema-de-Busca-Inteligente-com-IA-RAG-FAISS-
Este projeto consiste em um sistema backend capaz de ler documentos PDF e responder perguntas com base no conteúdo do próprio documento.  A aplicação utiliza o conceito de RAG (Retrieval-Augmented Generation), combinando busca semântica com modelos de linguagem para gerar respostas precisas e contextualizadas, reduzindo alucinações da IA.

Como funciona

O sistema segue um pipeline completo de processamento de dados:
1. Ingestão do PDF
  * Leitura página por página
  * Extração de texto
2. Pré-processamento
  * Limpeza de texto (remoção de quebras, espaços e ruídos)
  * Divisão em chunks com base em frases (melhor contexto semântico)
3. Geração de embeddings
  * Conversão dos textos em vetores numéricos usando Sentence Transformers
4. Indexação
  * Armazenamento dos vetores em um índice FAISS para busca eficiente
5. Busca semântica
  * A pergunta do usuário é transformada em embedding
  * O sistema busca os trechos mais relevantes do documento
6. Geração de resposta (LLM)
  * Um modelo de linguagem (Groq / Llama 3) responde com base no contexto recuperado
  * A resposta inclui referência às páginas do documento

Exemplo de uso
Digite sua busca: Como o sistema operacional gerencia o processador?

Resultados mais relevantes:
[Página 102] ...
[Página 721] ...
[Página 290] ...

Resposta da IA:
O sistema operacional gerencia o processador por meio de um escalonador...
(Páginas 102, 290 e 721)

Tecnologias utilizadas
  * Python
  * FAISS (busca vetorial)
  * Sentence Transformers (embeddings)
  * Groq API (LLM - Llama 3)
  * PyPDF (leitura de PDF)
  * NumPy

Como executar o projeto
  1. Clone o repositório
    git clone https://github.com/seu-usuario/seu-repo.git
    cd seu-repo
  2. Crie um ambiente virtual
    python -m venv venv
    venv\Scripts\activate  # Windows
  3. Instale as dependências
    pip install -r requirements.txt
  4. Configure a API Key
    Crie um arquivo .env:
    GROQ_API_KEY=sua_chave_aqui
  5. Execute o projeto
    python app_withFAISS.py

Estrutura do projeto
.
├── app_withFAISS.py     # Pipeline principal
├── pdf_loader2.py       # Leitura e processamento do PDF
├── llm_groq.py          # Integração com o modelo de linguagem
├── .env                 # Chave da API
└── Sistemas.pdf         # Documento utilizado

Diferenciais do projeto
  * Implementação de RAG completo (não apenas chat com IA)
  * Uso de busca vetorial com FAISS
  * Estratégia de chunking por frases (melhora contexto e relevância)
  * Redução de alucinação com controle de contexto
  * Respostas com referência às páginas do documento
  * Pipeline backend bem estruturado (ingestão → processamento → busca → resposta)
