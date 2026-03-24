# Como Rodar

Este guia cobre a execução local do frontend da Tecteca.

## 📋 Pré-requisitos

- Node.js 18 LTS recomendado.
- Yarn 1.22.x, que é o gerenciador já definido no projeto.
- Backend REST da Tecteca disponível e acessível.
- Acesso à internet para páginas públicas que dependem de Storyblok e para integrações externas.

## ⚙️ Variáveis de ambiente

O frontend depende da variável `URL_REST`, exposta via `next.config.js`.

Use o arquivo `.env.example` como referência e crie ou ajuste `.env.local` na raiz do projeto:

```env
URL_REST=http://localhost:3001/
```

Se o backend estiver em homologação, produção ou outra porta, ajuste esse valor.

## 📦 Instalação

```bash
yarn install
```

Se for necessário usar `npm`, os comandos equivalentes funcionam, mas o repositório está preparado para `yarn`.

## ▶️ Executando em desenvolvimento

```bash
yarn dev
```

Depois disso, acesse:

- `http://localhost:3000` para a home pública;
- `http://localhost:3000/signIn` para login;
- `http://localhost:3000/admin` para a área administrativa, se o usuário autenticado for admin;
- `http://localhost:3000/customer` para a área do cliente.

## 🛠️ Scripts disponíveis

```bash
yarn dev
yarn build
yarn start
yarn eslint
```

## 🔄 Fluxo esperado ao subir localmente

1. A home pública deve abrir normalmente.
2. O login deve enviar credenciais para `POST /session` no backend configurado em `URL_REST`.
3. Após autenticar:
   - usuários com `admin = true` são redirecionados para `/admin`.
   - usuários comuns são redirecionados para `/customer`.

## ⚠️ Problemas comuns

### A aplicação abre, mas nenhuma ação funciona

Na maior parte dos casos, `URL_REST` está ausente, incorreta ou apontando para um backend indisponível.

### O login entra em loop ou volta para `/signIn`

O projeto depende dos cookies `app.token`, `app.refreshToken` e `app.user`. Se estiverem vencidos ou inconsistentes, limpe os cookies do domínio local e faça login novamente.

### Páginas públicas com conteúdo vazio

As páginas públicas dependem do Storyblok. Se a estrutura estiver correta mas o conteúdo não carregar, valide acesso de rede e configuração do espaço de conteúdo usado pela aplicação.

### Erros de autenticação após algum tempo

O cliente Axios tenta renovar o token por meio de `POST /refresh-token`. Se o refresh token não for aceito pelo backend, a sessão é encerrada e o usuário volta para o login.

## ✅ Validação rápida de ambiente

Antes de começar a desenvolver, vale validar este checklist:

- `yarn install` concluiu sem erro.
- `.env.local` tem `URL_REST` válido.
- `yarn dev` sobe em `localhost:3000`.
- a tela de login abre.
- o backend responde a autenticação.

Se tudo isso estiver funcionando, o ambiente está pronto para desenvolvimento.

---

← [Voltar ao README](../README.md) · Próximo: [Estrutura e Arquitetura](ESTRUTURA_E_ARQUITETURA.md) →