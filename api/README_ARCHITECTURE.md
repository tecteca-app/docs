# Arquitetura e Estrutura do Projeto 🏗️

Este projeto segue os princípios de **Clean Architecture** e **DDD (Domain Driven Design)** adaptados para o ecossistema Node.js, visando desacoplamento e facilidade de testes.

---

## 📂 Estrutura de Pastas (Raiz)

- `.github/workflows`: Configurações de CI/CD (GitHub Actions).
- `dist`: Código compilado em JavaScript (gerado após o build).
- `src`: Código fonte da aplicação em TypeScript.
- `dockerfile` / `docker-compose.yaml`: Configurações de containerização.
- `ormconfig.js`: Configuração do TypeORM CLI.

---

## 🧩 Camadas Internas (`src/`)

### 1. `modules/`
Contém os domínios de negócio da aplicação. Cada módulo (ex: `accounts`, `books`, `profiles`) é independente e possui sua própria estrutura:
- **`dtos/`**: Data Transfer Objects (definição de tipos para entrada de dados).
- **`infra/typeORM/entities/`**: Modelos do banco de dados.
- **`repositories/`**: Interfaces e implementações de acesso a dados.
- **`useCases/`**: A "lógica de negócio" real. Cada UseCase foca em uma única funcionalidade (ex: `CreateUser`, `ListBooks`).
- **`views/`**: Templates (ex: e-mails em Handlebars).

### 2. `shared/`
Contém tudo que é compartilhado entre múltiplos módulos:
- **`container/`**: Configuração da Injeção de Dependência (TSyringe).
- **`errors/`**: Tratamento global de exceções.
- **`infra/http/`**: Configuração do Express (rotas, middlewares, servidor).
- **`infra/typeORM/`**: Migrações globais e conexão com o banco.

---

## 🔄 Fluxo de uma Requisição

1.  A requisição chega via **HTTP** (`src/shared/infra/http/routes`).
2.  É direcionada para um **Controller** do módulo específico.
3.  O Controller chama o **UseCase** correspondente.
4.  O UseCase utiliza o **Repository** para interagir com o banco de dados.
5.  O UseCase retorna a resposta para o Controller, que a envia de volta ao cliente.

---

## 🎨 Padrões e Práticas

- **Dependency Injection:** Utilizamos `TSyringe` para injetar repositórios nos use cases, facilitando o uso de mocks em testes.
- **SOLID:** O código é desenvolvido buscando respeitar os 5 princípios, especialmente responsabilidade única (S) e inversão de dependência (D).
- **Entidades:** O TypeORM é usado para mapear as classes para as tabelas do PostgreSQL.
- **Migrations:** Controle de versão do banco de dados para evitar inconsistências entre ambientes.

---

## 📚 Outras Documentações
- [Configuração do Banco de Dados](./README_DATABASE.md)
- [Guia de Deploy e CI/CD](./README_DEPLOY.md)
