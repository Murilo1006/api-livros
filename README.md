# 📚 API de Livros — FastAPI + MySQL

> Uma API REST para gerenciamento de um acervo de livros, construída com **FastAPI** e **MySQL**, com um Front End em **HTML, CSS e JavaScript puro** consumindo o CRUD completo.

![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat&logo=fastapi&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat&logo=mysql&logoColor=white)
![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-D71F00?style=flat&logo=python&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)

---

## 📖 Sobre o projeto

Este projeto implementa uma **API de gerenciamento de livros**, permitindo cadastrar, listar, consultar, atualizar e excluir registros de um acervo — o famoso **CRUD** completo. A API foi construída com **FastAPI** e persiste os dados em um banco **MySQL**, usando **SQLAlchemy** como camada de acesso ao banco.

Além da API, o projeto conta com um **Front End simples e funcional**, feito sem frameworks (apenas HTML, CSS e JavaScript), que consome as rotas da API diretamente pelo navegador.

Cada livro possui os seguintes dados:

| Campo | Tipo | Descrição |
| --- | --- | --- |
| `id` | inteiro | Identificador único (gerado pelo banco) |
| `titulo` | texto | Título do livro |
| `autor` | texto | Nome do autor |
| `ano_publicacao` | inteiro | Ano de publicação |
| `disponivel` | booleano | Indica se o livro está disponível |

---

## 🚀 Funcionalidades

- ✅ Cadastrar um novo livro
- ✅ Listar todos os livros
- ✅ Consultar um livro específico pelo `id`
- ✅ Atualizar os dados de um livro
- ✅ Excluir um livro
- ✅ Validação automática dos dados enviados (Pydantic)
- ✅ Documentação interativa gerada automaticamente (Swagger / ReDoc)
- ✅ Interface web para gerenciar o acervo sem precisar usar o Swagger

---

## 🛠️ Tecnologias utilizadas

**Back End**
- [Python](https://www.python.org/) 3.11+
- [FastAPI](https://fastapi.tiangolo.com/) — framework para criação da API
- [Uvicorn](https://www.uvicorn.org/) — servidor ASGI
- [SQLAlchemy](https://www.sqlalchemy.org/) — ORM para comunicação com o banco
- [PyMySQL](https://pypi.org/project/PyMySQL/) — driver de conexão com o MySQL
- [Pydantic Settings](https://docs.pydantic.dev/latest/concepts/pydantic_settings/) — leitura das variáveis de ambiente
- [MySQL](https://www.mysql.com/) — banco de dados relacional

**Front End**
- HTML5
- CSS3
- JavaScript (Fetch API, sem frameworks)

---

## 📂 Estrutura do projeto

```text
api-livros/
├── .env                    # variáveis locais (NÃO versionado)
├── .gitignore
├── requirements.txt
├── database/
│   └── biblioteca_db.sql   # estrutura e dados do banco
├── app/
│   ├── __init__.py
│   ├── database.py         # configuração da conexão e da sessão
│   ├── models.py           # modelo SQLAlchemy da tabela `livros`
│   ├── schemas.py          # schemas Pydantic de entrada e saída
│   └── main.py             # rotas da API (CRUD)
└── frontend/
    ├── index.html
    ├── styles.css
    └── app.js
```

---

## 📡 Rotas da API

| Método | Rota | Descrição | Corpo esperado |
| --- | --- | --- | --- |
| `POST` | `/livros` | Cadastra um novo livro | `titulo`, `autor`, `ano_publicacao`, `disponivel` |
| `GET` | `/livros` | Lista todos os livros | — |
| `GET` | `/livros/{id_livro}` | Consulta um livro pelo `id` | — |
| `PUT` | `/livros/{id_livro}` | Atualiza um livro existente | `titulo`, `autor`, `ano_publicacao`, `disponivel` |
| `DELETE` | `/livros/{id_livro}` | Exclui um livro | — |
| `GET` | `/health` | Verifica se a API e o banco estão respondendo | — |

Exemplo de corpo para `POST` e `PUT`:

```json
{
  "titulo": "O Hobbit",
  "autor": "J. R. R. Tolkien",
  "ano_publicacao": 1937,
  "disponivel": true
}
```

---

## ⚙️ Como rodar o projeto localmente

### Pré-requisitos

- [Python 3.11+](https://www.python.org/downloads/)
- [MySQL](https://www.mysql.com/) (recomendado via [XAMPP](https://www.apachefriends.org/))
- [phpMyAdmin](https://www.phpmyadmin.net/) (incluso no XAMPP)
- [VS Code](https://code.visualstudio.com/) (opcional, mas recomendado)

### 1. Clone o repositório

```bash
git clone https://github.com/seu-usuario/api-livros.git
cd api-livros
```

### 2. Crie e ative o ambiente virtual

```bash
python -m venv .venv
.venv\Scripts\activate.bat
```

### 3. Instale as dependências

```bash
pip install -r requirements.txt
```

### 4. Configure as variáveis de ambiente

Crie um arquivo `.env` na raiz do projeto:

```dotenv
DB_USER=root
DB_PASSWORD=sua_senha_aqui
DB_HOST=localhost
DB_PORT=3306
DB_NAME=biblioteca_db
```

> ⚠️ O `.env` **nunca** deve ser enviado ao GitHub — ele já está no `.gitignore`.

### 5. Crie o banco de dados

Com o Apache e o MySQL ativos no XAMPP, acesse o phpMyAdmin e importe o arquivo `database/biblioteca_db.sql`, ou crie o banco manualmente:

```sql
CREATE DATABASE biblioteca_db
  CHARACTER SET utf8mb4
  COLLATE utf8mb4_unicode_ci;
```

### 6. Execute a API

```bash
uvicorn app.main:app --reload
```

A API estará disponível em `http://127.0.0.1:8000`, com a documentação interativa em:

- Swagger: `http://127.0.0.1:8000/docs`
- ReDoc: `http://127.0.0.1:8000/redoc`

### 7. Execute o Front End

Em um segundo terminal, na raiz do projeto:

```bash
python -m http.server 5500 --directory frontend
```

Acesse `http://127.0.0.1:5500` no navegador.

> Mantenha os dois servidores rodando ao mesmo tempo — a API na porta `8000` e o Front End na porta `5500`.

---

## 🧪 Testando a aplicação

Você pode testar as rotas de duas formas:

1. **Pelo Swagger** (`/docs`), enviando as requisições diretamente pela documentação interativa.
2. **Pelo Front End**, cadastrando, editando e excluindo livros pela interface web.

A API valida automaticamente os dados enviados e retorna:

- `201` ao criar um livro com sucesso;
- `404` quando o `id` não existe;
- `422` quando os dados enviados são inválidos (ex.: título vazio, ano fora do intervalo permitido).

---

## 👤 Autor

Desenvolvido como projeto de estudo de back end com FastAPI, MySQL e integração com um front end simples em HTML, CSS e JavaScript.

---

<p align="center">Feito com 💻 e ☕</p>
