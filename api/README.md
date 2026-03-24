# TECTECA API 📚

A API do projeto TECTECA é o motor que gerencia usuários, livros, perfis, e integrações com diversos serviços (IUGU, AWS, Apple IAP, Hub Educacional). Construída seguindo princípios de Clean Architecture e SOLID para garantir escalabilidade e manutenibilidade.

---

## 🚀 Tecnologias e Ferramentas

O projeto utiliza um stack moderno focado em performance e produtividade:

- **Linguagem:** [TypeScript](https://www.typescriptlang.org/)
- **Runtime:** [Node.js](https://nodejs.org/)
- **Framework Web:** [Express](https://expressjs.com/)
- **ORM:** [TypeORM](https://typeorm.io/) (PostgreSQL)
- **Containerização:** [Docker](https://www.docker.com/) & [Docker Compose](https://docs.docker.com/compose/)
- **Cache / Rate Limit:** [Redis](https://redis.io/)
- **Injeção de Dependência:** [TSyringe](https://github.com/microsoft/tsyringe)
- **Validação:** [Celebrate](https://github.com/arb/celebrate) (Joi)
- **Testes:** [Jest](https://jestjs.io/)
- **Documentação API:** [Swagger](https://swagger.io/)

---

## 🛠️ Pré-requisitos

Antes de começar, você vai precisar das seguintes ferramentas:

- [Node.js](https://nodejs.org/en/) (v14+ recomendado)
- [Yarn](https://yarnpkg.com/) ou [NPM](https://www.npmjs.com/)
- [Docker](https://www.docker.com/get-started) e [Docker Compose](https://docs.docker.com/compose/install/) (opcional para rodar local via container)
- [PostgreSQL](https://www.postgresql.org/) (se não for usar Docker)
- [Redis](https://redis.io/) (se não for usar Docker)

---

## ⚙️ Configuração do Ambiente

1. Clone o repositório.
2. Copie o arquivo `.env.example` para `.env`:
   ```bash
   cp .env.example .env
   ```
   ```powershell
   Copy-Item .env.example .env
   ```
3. Preencha as variáveis de ambiente no `.env`. As principais são:
   - `DATABASE_URL`: URL de conexão com o Postgres.
   - `SECRET_TOKEN`: Chave secreta para JWT.
   - `AWS_ACCESS_KEY_ID` / `AWS_SECRET_ACCESS_KEY`: Credenciais para S3.
   - `PORT`: Porta em que o servidor irá rodar (padrão: 3001).

---

## 🏃 Como Rodar / Inicialização

As instruções detalhadas de como instalar dependências, lidar com múltiplos ambientes (`.env.dev` / `.env.prod`), rodar as migrações e inicializar via Docker estão centralizadas no guia abaixo:
- [Guia de Inicialização (Como Rodar)](./README_RUN.md)

---

## 🏗️ Estrutura e Arquitetura

O projeto segue padrões de Clean Architecture e DDD. Para entender mais sobre a organização das pastas e padrões de design, veja:
- [Documentação de Arquitetura](./README_ARCHITECTURE.md)

---

## 🗄️ Banco de Dados

Utilizamos PostgreSQL e TypeORM. Detalhes sobre entidades e migrações:
- [Documentação do Banco de Dados](./README_DATABASE.md)

---

## 🚀 Deploy e CI/CD

O deploy é automatizado via GitHub Actions. Veja como funciona:
- [Documentação de Deploy](./README_DEPLOY.md)

---

## 📚 Operações Comuns

Guia passo a passo para ações como trocar senha, recuperar conta e gerenciar perfis:
- [Guia de Operações](./README_OPERATIONS.md)

---

## 📜 Licença

Este módulo segue a licença definida no repositório de origem: [tecteca-app/api-node](https://github.com/tecteca-app/api-node).
