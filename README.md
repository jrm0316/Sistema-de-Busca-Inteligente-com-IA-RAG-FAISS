# Sistema-de-Busca-Inteligente-com-IA-RAG-FAISS-
Este projeto consiste em um sistema backend capaz de ler documentos PDF e responder perguntas com base no conteúdo do próprio documento.  A aplicação utiliza o conceito de RAG (Retrieval-Augmented Generation), combinando busca semântica com modelos de linguagem para gerar respostas precisas e contextualizadas, reduzindo alucinações da IA.


### Como funciona ###
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

### Exemplo de uso ###
  Digite sua busca: Como o sistema operacional gerencia o processador?


### Resultados mais relevantes: ###

    [Página 102] ... 
    [Página 721] ...
    [Página 290] ...

### Resposta da IA:
O sistema operacional gerencia o processador por meio de um escalonador...
(Páginas 102, 290 e 721)

Tecnologias utilizadas
  * Python
  * FAISS (busca vetorial)
  * Sentence Transformers (embeddings)
  * Groq API (LLM - Llama 3)
  * PyPDF (leitura de PDF)
  * NumPy

## Como executar o projeto

### 1. Clonar o repositório

```bash
git clone https://github.com/jrm0316/Sistema-de-Busca-Inteligente-com-IA-RAG-FAISS.git
cd Sistema-de-Busca-Inteligente-com-IA-RAG-FAISS
```

### 2. Criar e ativar um ambiente virtual

No Windows (PowerShell):

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

### 3. Instalar as dependências

```bash
pip install -r requirements.txt
```

### 4. Configurar a chave da Groq

Crie um arquivo `.env` na raiz do projeto, utilizando `.env.example` como referência.

Adicione sua própria chave:

```env
GROQ_API_KEY=sua_chave_aqui
```

Nunca publique sua chave verdadeira no GitHub.

### 5. Adicionar um documento PDF

Coloque um arquivo PDF na raiz do projeto com o nome:

`Sistemas.pdf`

O programa utiliza esse arquivo como documento de entrada. Para utilizar outro nome, altere o caminho informado em `app_withFAISS.py`.

### 6. Executar a aplicação

```bash
python app_withFAISS.py
```

Após o processamento do PDF, o programa solicitará uma pergunta no terminal e apresentará os trechos recuperados e a resposta gerada pela IA.

### Estrutura do projeto ###

├── app_withFAISS.py     # Pipeline principal de RAG

├── pdf_loader2.py       # Leitura e processamento de PDFs

├── llm_groq.py          # Integração com a API Groq

├── requirements.txt     # Dependências do projeto

├── .env.example         # Exemplo de configuração da API

├── .gitignore           # Arquivos ignorados pelo Git

└── README.md            # Documentação

### Diferenciais do projeto ###
  * Implementação de RAG completo (não apenas chat com IA)
  * Uso de busca vetorial com FAISS
  * Estratégia de chunking por frases (melhora contexto e relevância)
  * Redução de alucinação com controle de contexto
  * Respostas com referência às páginas do documento
  * Pipeline backend bem estruturado (ingestão → processamento → busca → resposta)

### Autor ###
  Desenvolvido por Juliano Rodrigues Madeira
