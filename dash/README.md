
# Tecteca Dashboard

Frontend do dashboard da Tecteca, construído com Next.js 12, React 18, Chakra UI, React Query e TypeScript.

O projeto atende duas frentes principais:

- área do cliente para login, atualização de conta, visualização de perfis e contratação de assinatura;
- área administrativa para operação de usuários, livros, personagens, grupos, parceiros, planos, assinaturas e indicadores do negócio.

## O que a aplicação faz

- autentica usuários e diferencia o acesso entre `admin` e `customer`;
- consome um backend REST para regras de negócio e persistência;
- publica páginas públicas e landing pages com conteúdo vindo do Storyblok;
- oferece jornada de assinatura com integração de pagamento via Iugu e também visão de assinaturas Apple;
- permite recuperação de senha por e-mail e reset manual de senha na área administrativa.

## Stack principal

- Next.js 12 com Pages Router
- React 18
- Chakra UI
- React Query
- Axios
- Storyblok
- TypeScript

## Documentação

Use a trilha abaixo conforme o momento do trabalho:

### 🚀 Primeiros passos

- 🧩 [Onboarding Rápido para Devs e Suporte](./ONBOARDING_RAPIDO.md) - resumo objetivo para quem está chegando agora, com visão do sistema, rotas essenciais, pontos de triagem e atalhos para começar rápido.
- ▶️ [Como Rodar](./COMO_RODAR.md) - passo a passo para preparar o ambiente local, configurar `URL_REST`, instalar dependências e validar que o frontend está funcionando com o backend.

### 🧭 Entendimento do sistema

- 📘 [Uso Básico da Aplicação](./USO_BASICO_DA_APLICACAO.md) - explica o que a plataforma faz, quais são os perfis de usuário e quais telas são mais importantes nas jornadas pública, customer e admin.
- 🏗️ [Estrutura e Arquitetura](./ESTRUTURA_E_ARQUITETURA.md) - detalha a organização das pastas, as camadas da aplicação, o fluxo entre frontend, Storyblok e backend, e os principais pontos técnicos do projeto.

### 🛠️ Operação e suporte

- 📋 [Operações Comuns](./OPERACOES_COMUNS.md) - guia prático para tarefas recorrentes de operação, manutenção e navegação pelos módulos administrativos.
- 🔐 [Recuperação de Senha e Reset pelo Admin](./RECUPERACAO_DE_SENHA_E_RESET_ADMIN.md) - documenta os dois caminhos de recuperação de acesso: autoatendimento por e-mail e redefinição manual feita pelo administrador.

### ☁️ Publicação

- 🚢 [Build para Produção e Deploy](./BUILD_PRODUCAO_E_DEPLOY.md) - reúne os comandos de build, checklist de publicação e cuidados para subir o frontend com segurança em produção.

## Rotas mais importantes

- `/`, `/landing` e `/m` para páginas públicas renderizadas com Storyblok.
- `/signIn`, `/new-account`, `/reset-forgot`, `/reset-password` e `/password/reset` para autenticação e recuperação de acesso.
- `/customer` e `/customer/new-plan` para a área do cliente.
- `/admin`, `/admin/users`, `/admin/books`, `/admin/subscriptions`, `/admin/groups`, `/admin/feed`, `/admin/partners`, `/admin/export` para a operação administrativa.

## Resumo rápido para desenvolvimento

- Configure `URL_REST` em `.env.local`.
- Instale dependências com `yarn install`.
- Rode a aplicação com `yarn dev`.
- Gere build com `yarn build` e suba com `yarn start`.

Os detalhes estão nos documentos listados acima.
