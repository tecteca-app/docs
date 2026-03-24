# Como Rodar a Aplicação 🏃

Este guia detalha como inicializar o TECTECA API em diferentes ambientes (Desenvolvimento, Produção ou via Docker).

---

## 💻 Desenvolvimento Local (Múltiplos Ambientes)

Você pode configurar a aplicação para rodar apontando para diferentes bancos de dados ou serviços dependendo se está testando localmente, conectando ao ambiente de Staging (Homologação) ou Produção.

**1. Configuração dos Arquivos:**
Em vez de ter apenas um `.env`, você pode criar arquivos separados baseados no `.env.example`:
- `.env.dev`: Para o ambiente de Desenvolvimento / Homologação.
- `.env.prod`: Para espelhar Produção.

*Nota: O `.gitignore` já está configurado para ignorar esses arquivos, garantindo a segurança das suas chaves (não faça commit de arquivos `.env.*`).*

**2. Instalando Dependências:**
```bash
yarn install
# ou
npm install
```

**3. Iniciando a aplicação com o ambiente escolhido:**

Para carregar um arquivo `.env` específico, modifique o comando de inicialização passando o caminho do arquivo desejado, utilizando a tag `-r dotenv/config`:

```bash
# Rodar carregando as chaves de Desenvolvimento
npx dotenv -e .env.dev -- yarn dev

# Ou carregando as chaves de Produção (Apenas se precisar depurar localmente)
npx dotenv -e .env.prod -- yarn dev
```
*(Caso ocorra erros com `-e`, assegure-se de estar rodando as instâncias em terminais separados adequados)*.

**4. Migrações do Banco de Dados:**
```bash
yarn typeorm migration:run
# ou
npm run typeorm migration:run
```

O servidor estará disponível em `http://localhost:3001` (ou a porta definida no `.env`).

---

## 🐳 Usando Docker

O projeto já conta com `docker-compose.yaml` e `dockerfile` configurados para subir o banco de dados e a aplicação rapidamente.

```bash
docker-compose up -d
```
Isso iniciará a API, o banco PostgreSQL e o Redis em background.

---

## 🧪 Rodando os Testes

Para garantir a qualidade e integridade do código:

```bash
# Rodar todos os testes
yarn test

# Rodar testes com cobertura
yarn test:cov

# Rodar testes em modo watch
yarn test:watch
```
