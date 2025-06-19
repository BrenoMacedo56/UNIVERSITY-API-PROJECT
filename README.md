# 📘 Documentação do Projeto de Aplicação Financeira

Este repositório contém a documentação técnica e funcional de uma aplicação financeira desenvolvida como **trabalho final da disciplina _Linguagem de Programação para Internet_** do curso de **Sistemas de Informação** da **Universidade de Uberaba (UNIUBE)**.

A aplicação inclui:
- Endpoints da API
- Instruções de instalação e deploy
- Exemplos de uso
- Funcionalidades principais

> ⚠️ **Atenção:** Este projeto foi desenvolvido em colaboração com outros membros de equipe. A autoria não é exclusiva.

## 👥 Equipe de Desenvolvimento

### 🔧 Back-End
- [@daviisp](https://github.com/daviisp)<br>Lógica do back-end extraida de um de seus projetos. [ACESSE AQUI](https://github.com/daviisp/finance-app-backend)

### 🎨 Front-End
- [@Yanlucca0205](https://github.com/YANLUCCA0205/YanLucca0205)

---

Sinta-se à vontade para explorar os arquivos e contribuir!
## 1. Endpoints da API


A API do projeto é construída com Node.js e Express, fornecendo uma interface RESTful para a gestão de usuários e transações financeiras. Os endpoints são categorizados da seguinte forma:

### 1.1. Endpoints de Usuários

| Método HTTP | Endpoint           | Descrição                                   | Autenticação Necessária |
|-------------|--------------------|---------------------------------------------|-------------------------|
| `POST`      | `/users`           | Cria um novo usuário.                       | Não                     |
| `PATCH`     | `/me`              | Atualiza os dados do usuário autenticado.   | Sim                     |
| `GET`       | `/me`              | Retorna os dados do usuário autenticado.    | Sim                     |
| `GET`       | `/me/balance`      | Retorna o saldo do usuário autenticado.     | Sim                     |
| `DELETE`    | `/me`              | Exclui o usuário autenticado.               | Sim                     |
| `POST`      | `/auth/login`      | Realiza o login do usuário e retorna um token de autenticação. | Não                     |
| `POST`      | `/refresh-token`   | Renova o token de autenticação.             | Não                     |

### 1.2. Endpoints de Transações

| Método HTTP | Endpoint                  | Descrição                                   | Autenticação Necessária |
|-------------|---------------------------|---------------------------------------------|-------------------------|
| `POST`      | `/transactions`           | Cria uma nova transação para o usuário autenticado. | Sim                     |
| `PATCH`     | `/transactions/:id`       | Atualiza uma transação específica do usuário autenticado. | Sim                     |
| `DELETE`    | `/transactions/:id`       | Exclui uma transação específica do usuário autenticado. | Sim                     |
| `GET`       | `/transactions`           | Retorna todas as transações do usuário autenticado. | Sim                     |




## 2. Instalação / Deploy

Esta seção descreve os passos necessários para configurar e executar o projeto, tanto o frontend quanto o backend.

### 2.1. Pré-requisitos

Certifique-se de ter as seguintes ferramentas instaladas em seu ambiente:

*   **Node.js** (versão 18 ou superior)
*   **npm** (gerenciador de pacotes do Node.js)
*   **PostgreSQL** (servidor de banco de dados)
*   **Git** (para clonar o repositório)

### 2.2. Configuração do Banco de Dados (PostgreSQL)

1.  Crie um novo banco de dados PostgreSQL para a aplicação (ex: `finance_app_db`).
2.  Crie um arquivo `.env` na raiz do diretório `finance-app-backend` com as seguintes variáveis de ambiente, substituindo os valores pelos seus dados de conexão:

    ```
    DATABASE_URL="postgresql://USER:PASSWORD@HOST:PORT/DATABASE?schema=public"
    JWT_SECRET="sua_chave_secreta_jwt"
    ```

    *   `USER`: Seu usuário do PostgreSQL.
    *   `PASSWORD`: Sua senha do PostgreSQL.
    *   `HOST`: O host do seu servidor PostgreSQL (geralmente `localhost`).
    *   `PORT`: A porta do seu servidor PostgreSQL (geralmente `5432`).
    *   `DATABASE`: O nome do banco de dados que você criou (ex: `finance_app_db`).
    *   `JWT_SECRET`: Uma string secreta para assinar os tokens JWT. Gere uma string longa e aleatória.

3.  No diretório `finance-app-backend`, execute os comandos para aplicar as migrações do Prisma e gerar o cliente Prisma:

    ```bash
    cd finance-app-backend
    npm install
    npx prisma migrate dev --name init
    npx prisma generate
    ```

### 2.3. Instalação e Execução do Backend

1.  Navegue até o diretório `finance-app-backend`:

    ```bash
    cd finance-app-backend
    ```

2.  Instale as dependências do projeto:

    ```bash
    npm install
    ```

3.  Inicie o servidor de desenvolvimento:

    ```bash
    npm run dev
    ```

    O backend estará disponível em `http://localhost:3000` (ou outra porta configurada).

### 2.4. Instalação e Execução do Frontend

1.  Navegue até o diretório `API-Project` (frontend):

    ```bash
    cd API-Project
    ```

2.  Instale as dependências do projeto:

    ```bash
    npm install
    ```

3.  Crie um arquivo `.env` na raiz do diretório `API-Project` com a seguinte variável de ambiente, apontando para a URL do seu backend:

    ```
    VITE_API_URL=http://localhost:3000
    ```

4.  Inicie o servidor de desenvolvimento:

    ```bash
    npm run dev
    ```

    O frontend estará disponível em `http://localhost:5173` (ou outra porta configurada).

### 2.5. Deploy (Considerações Gerais)

Para deploy em ambiente de produção, recomenda-se:

*   **Backend:** Utilizar serviços de hospedagem de Node.js (ex: Heroku, AWS EC2, DigitalOcean) e configurar um processo de CI/CD. O comando `npm start` deve ser usado para iniciar a aplicação em produção.
*   **Frontend:** Gerar a build de produção (`npm run build`) e servir os arquivos estáticos através de um servidor web (ex: Nginx, Apache) ou serviços de hospedagem de frontend (ex: Netlify, Vercel, AWS S3 com CloudFront).



## 3. Exemplo de Uso

Este exemplo demonstra um fluxo básico de interação com a aplicação, desde o registro de um novo usuário até o registro de uma transação financeira.

### 3.1. Registro de Usuário

Para começar a usar a aplicação, um novo usuário precisa se registrar. Isso pode ser feito através da interface de usuário do frontend, que enviará uma requisição `POST` para o endpoint `/users` do backend com os dados do novo usuário (ex: nome, email, senha).

**Exemplo de Requisição (via Postman ou similar):**

```http
POST /users HTTP/1.1
Host: localhost:3000
Content-Type: application/json

{
    "name": "Novo Usuário",
    "email": "novo.usuario@example.com",
    "password": "senhaSegura123"
}
```

**Exemplo de Resposta de Sucesso:**

```json
HTTP/1.1 201 Created
Content-Type: application/json

{
    "id": "uuid-do-usuario",
    "name": "Novo Usuário",
    "email": "novo.usuario@example.com",
    "createdAt": "2025-06-19T10:00:00.000Z",
    "updatedAt": "2025-06-19T10:00:00.000Z"
}
```

### 3.2. Login de Usuário

Após o registro, o usuário pode fazer login para obter um token de autenticação, que será usado para acessar os endpoints protegidos da API.

**Exemplo de Requisição:**

```http
POST /auth/login HTTP/1.1
Host: localhost:3000
Content-Type: application/json

{
    "email": "novo.usuario@example.com",
    "password": "senhaSegura123"
}
```

**Exemplo de Resposta de Sucesso:**

```json
HTTP/1.1 200 OK
Content-Type: application/json

{
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

### 3.3. Registro de Transação

Com o token de acesso em mãos, o usuário pode registrar uma nova transação (ex: despesa ou receita).

**Exemplo de Requisição:**

```http
POST /transactions HTTP/1.1
Host: localhost:3000
Content-Type: application/json
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

{
    "title": "Compra de Supermercado",
    "amount": 150.75,
    "type": "EXPENSE",
    "date": "2025-06-18T15:30:00.000Z"
}
```

**Exemplo de Resposta de Sucesso:**

```json
HTTP/1.1 201 Created
Content-Type: application/json

{
    "id": "uuid-da-transacao",
    "title": "Compra de Supermercado",
    "amount": 150.75,
    "type": "EXPENSE",
    "date": "2025-06-18T15:30:00.000Z",
    "userId": "uuid-do-usuario",
    "createdAt": "2025-06-19T10:05:00.000Z",
    "updatedAt": "2025-06-19T10:05:00.000Z"
}
```

### 3.4. Visualização do Saldo

O usuário pode consultar seu saldo atual a qualquer momento.

**Exemplo de Requisição:**

```http
GET /me/balance HTTP/1.1
Host: localhost:3000
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

**Exemplo de Resposta de Sucesso:**

```json
HTTP/1.1 200 OK
Content-Type: application/json

{
    "balance": 850.25
}
```




## 4. Funcionalidades

A aplicação financeira oferece um conjunto de funcionalidades essenciais para a gestão de finanças pessoais ou empresariais, divididas entre as capacidades do frontend e do backend:

### 4.1. Funcionalidades do Backend (API)

O backend, construído com Node.js e Express.js, é responsável por gerenciar a lógica de negócios e a persistência dos dados. Suas principais funcionalidades incluem:

*   **Autenticação e Autorização de Usuários:**
    *   Registro de novos usuários com validação de dados.
    *   Login de usuários existentes, gerando tokens de acesso (JWT) para sessões seguras.
    *   Mecanismo de refresh token para renovação de sessões sem a necessidade de novo login.
    *   Proteção de rotas através de middleware de autenticação, garantindo que apenas usuários autorizados possam acessar determinadas funcionalidades.
*   **Gestão de Usuários:**
    *   Criação e armazenamento de perfis de usuário.
    *   Atualização de informações de perfil (nome, email, senha).
    *   Recuperação de dados do perfil do usuário autenticado.
    *   Exclusão de contas de usuário.
*   **Gestão de Transações Financeiras:**
    *   Registro de novas transações, incluindo título, valor, tipo (receita/despesa) e data.
    *   Atualização de transações existentes.
    *   Exclusão de transações.
    *   Listagem de todas as transações associadas a um usuário específico.
*   **Cálculo de Saldo:**
    *   Cálculo dinâmico do saldo total do usuário com base em suas transações de receita e despesa.
*   **Persistência de Dados:**
    *   Utilização do PostgreSQL como banco de dados relacional para garantir a integridade, consistência e durabilidade dos dados financeiros.
    *   Uso do Prisma ORM para facilitar a interação com o banco de dados, abstraindo a complexidade das consultas SQL e garantindo a segurança das operações.

### 4.2. Funcionalidades do Frontend (React)

O frontend, desenvolvido com React, oferece uma interface de usuário interativa e responsiva para que os usuários possam interagir com as funcionalidades do backend. As principais funcionalidades incluem:

*   **Interface de Usuário Intuitiva:**
    *   Design limpo e moderno, facilitando a navegação e a compreensão das informações financeiras.
    *   Componentes reutilizáveis para uma experiência de usuário consistente e eficiente.
*   **Registro e Login:**
    *   Formulários para registro de novos usuários e login de usuários existentes.
    *   Feedback visual para validação de formulários e status de autenticação.
*   **Dashboard Financeiro:**
    *   Visualização clara do saldo atual do usuário.
    *   Apresentação de um resumo das transações, categorizadas por tipo (receitas e despesas).
*   **Gestão de Transações:**
    *   Formulários para adicionar novas transações (receitas e despesas).
    *   Listagem detalhada de todas as transações, com opções de filtragem e ordenação.
    *   Funcionalidades para editar e excluir transações existentes.
*   **Navegação e Rotas:**
    *   Gerenciamento de rotas na aplicação para uma navegação fluida entre diferentes seções (ex: dashboard, transações, perfil).
*   **Comunicação com a API:**
    *   Integração com a API do backend para enviar e receber dados de forma assíncrona, garantindo que a interface do usuário esteja sempre atualizada com as informações mais recentes.
*   **Responsividade:**
    *   Layout adaptável a diferentes tamanhos de tela, proporcionando uma experiência de uso otimizada em dispositivos desktop, tablets e móveis.


