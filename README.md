# Sistema de Busca Inteligente em PDFs com IA - RAG + FAISS

Tecnologias: Python | FAISS | Sentence Transformers | PyPDF | Groq API | Llama 3

Sistema desenvolvido em Python para realizar consultas inteligentes a documentos PDF utilizando a arquitetura RAG (Retrieval-Augmented Generation).

A aplicação extrai e processa textos de documentos, gera embeddings com Sentence Transformers e utiliza o FAISS para recuperar trechos relevantes por similaridade vetorial. Esses trechos são enviados a um modelo de linguagem pela API Groq, permitindo gerar respostas contextualizadas com referências às páginas dos documentos.

O projeto demonstra a implementação prática de um pipeline de recuperação e geração de respostas com Inteligência Artificial, desde o processamento do PDF até a interação com o modelo de linguagem.


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

```text
├── app_withFAISS.py   # Pipeline principal de RAG

├── pdf_loader2.py     # Leitura e processamento de PDFs

├── llm_groq.py        # Integração com a API Groq

├── requirements.txt   # Dependências do projeto

├── .env.example       # Exemplo de configuração da API

├── .gitignore         # Arquivos ignorados pelo Git

└── README.md          # Documentação
```

**Arquivos necessários para execução local:**
```text
.env                   # Chave de API pessoal (não versionar)
Sistemas.pdf           # PDF fornecido pelo usuário
```

### Diferenciais do projeto ###

- Implementação de um pipeline RAG completo, integrando processamento de PDFs, embeddings, busca vetorial e geração de respostas com LLM.
- Utilização do FAISS com índice `IndexFlatL2` para recuperação de trechos por similaridade vetorial.
- Segmentação de textos em chunks baseada em frases, com tamanho aproximado de 800 caracteres.
- Utilização do modelo `all-MiniLM-L6-v2` da biblioteca Sentence Transformers para geração de embeddings.
- Recuperação dos 15 trechos mais próximos da pergunta para composição do contexto enviado ao LLM.
- Preservação dos números das páginas dos documentos para identificação da origem dos trechos recuperados.
- Prompt orientado a responder com base no contexto fornecido e informar quando não houver informações suficientes.
- Organização do processamento em módulos Python separados para leitura de PDFs, busca semântica e integração com a API Groq.

### Autor ###
  Desenvolvido por Juliano Rodrigues Madeira
