# Onboarding Rápido para Devs e Suporte

Este guia é a versão curta da documentação do projeto. A ideia é fazer alguém novo entender o sistema, subir o ambiente e localizar os pontos principais sem ler tudo de uma vez.

## 💬 Em uma frase

O Tecteca Dashboard é o frontend da operação da Tecteca: ele tem páginas públicas, login, área do cliente e área administrativa para usuários, livros, assinaturas e suporte operacional.

## 🧠 O que você precisa saber primeiro

- o frontend é um projeto Next.js 12 com Pages Router;
- a aplicação depende de um backend REST configurado por `URL_REST`;
- páginas públicas usam Storyblok;
- usuários `admin` entram em `/admin` e usuários comuns entram em `/customer`;
- autenticação usa cookies `app.token`, `app.refreshToken` e `app.user`.

## 👨‍💻 Checklist do primeiro dia para dev

1. Instale dependências com `yarn install`.
2. Configure `.env.local` com `URL_REST`.
3. Rode `yarn dev`.
4. Abra `/signIn`.
5. Valide login com um usuário admin e um usuário customer, se possível.
6. Confira as rotas `/admin`, `/customer` e `/reset-forgot`.

## 🎧 Checklist do primeiro dia para suporte

1. Entenda se o problema está em login, cadastro, assinatura, conteúdo público ou operação admin.
2. Verifique qual perfil do usuário está envolvido: `admin` ou cliente.
3. Confirme em qual rota o problema acontece.
4. Valide se o backend está respondendo.
5. Se for problema de sessão, peça novo login ou limpeza dos cookies da aplicação.

## 🗺️ Rotas para decorar

| Rota | Uso |
| --- | --- |
| `/` | home pública |
| `/signIn` | login |
| `/new-account` | criação de conta |
| `/reset-forgot` | solicitar recuperação de senha |
| `/password/reset` | reset com token |
| `/customer` | área do cliente |
| `/customer/new-plan` | contratação de assinatura |
| `/admin` | dashboard administrativo |
| `/admin/users` | operação de clientes |
| `/admin/books` | operação do catálogo |
| `/admin/subscriptions` | assinaturas Iugu |

## 🔍 Onde olhar no código

- `src/pages/`: rotas e telas.
- `src/components/`: layout, formulários, tabelas e modais.
- `src/contexts/AuthContext.tsx`: login, sessão e redirecionamento.
- `src/services/api.ts` e `src/services/apiClient.ts`: cliente HTTP e refresh token.
- `src/services/hooks/`: consultas por domínio.
- `src/storyblok/`: componentes usados pelas páginas públicas.
- `src/utils/withSSRAuth.ts` e `src/utils/withSSRGuest.ts`: proteção de rotas.

## 🏗️ Como o sistema se organiza mentalmente

### Público

- home, landing pages e conteúdo institucional;
- forte dependência de Storyblok.

### Customer

- consulta da conta;
- perfis vinculados;
- assinatura e pagamento.

### Admin

- dashboard com indicadores;
- usuários, livros, grupos, parceiros, feed, assinaturas e exportação.

## ❓ Perguntas de triagem mais comuns no suporte

### O usuário não consegue entrar

Verifique credenciais, backend, cookies da sessão e se a conta já foi validada.

### O usuário esqueceu a senha

Comece por `/reset-forgot`. Se necessário, o admin pode redefinir a senha direto no detalhe do usuário em `/admin/users/[id]`.

### A assinatura não apareceu ou o pagamento não atualizou

Verifique a jornada em `/customer/new-plan` e a visão administrativa em `/admin/subscriptions`.

### A página pública está vazia ou diferente do esperado

Provavelmente o ponto de análise está no Storyblok ou nos componentes de `src/storyblok`.

## 📚 Ordem recomendada de leitura da documentação completa

1. [Como Rodar](COMO_RODAR.md)
2. [Estrutura e Arquitetura](ESTRUTURA_E_ARQUITETURA.md)
3. [Uso Básico da Aplicação](USO_BASICO_DA_APLICACAO.md)
4. [Operações Comuns](OPERACOES_COMUNS.md)
5. [Recuperação de Senha e Reset pelo Admin](RECUPERACAO_DE_SENHA_E_RESET_ADMIN.md)

Se a pessoa for trabalhar com infraestrutura ou publicação, complete com [Build para Produção e Deploy](BUILD_PRODUCAO_E_DEPLOY.md).

---

← [Voltar ao README](../README.md)