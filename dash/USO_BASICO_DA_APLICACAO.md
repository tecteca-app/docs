# Uso Básico da Aplicação

## 📌 O que é a aplicação

O Tecteca Dashboard é o frontend de operação da plataforma Tecteca. Ele combina uma área pública de apresentação e cadastro com um dashboard autenticado para clientes e administradores.

Na prática, a aplicação serve para:

- autenticar usuários da plataforma;
- permitir que clientes visualizem sua conta, perfis e jornada de assinatura;
- permitir que administradores operem o catálogo, usuários, assinaturas e demais módulos do ecossistema;
- exibir páginas públicas e institucionais alimentadas por Storyblok.

## 👥 Perfis de uso

### Cliente

O cliente entra no sistema para:

- consultar dados da conta;
- ver perfis vinculados;
- visualizar atividades associadas aos perfis;
- contratar ou acompanhar uma assinatura.

### Admin

O admin usa o dashboard para:

- acompanhar indicadores gerais;
- cadastrar e editar usuários;
- gerenciar livros e taxonomias;
- acompanhar assinaturas Iugu, Apple e sistema;
- operar grupos, feed, parceiros, personagens e exportações.

## 🗺️ Jornada básica do usuário

### 1. Acesso inicial

As portas de entrada mais comuns são:

- `/` para a home pública;
- `/signIn` para login;
- `/new-account` para auto cadastro;
- `/reset-forgot` para pedir recuperação de senha.

Em alguns cenários existe também a rota `/formulario`, conectada a um fluxo específico de formulário e integração externa.

### 2. Cadastro e validação

Depois de criar conta, o usuário pode precisar validar o cadastro por e-mail antes de usar o sistema. A validação é tratada pela rota `/user-validate`.

### 3. Login

Após autenticar:

- admins vão para `/admin`;
- clientes vão para `/customer`.

## 📺 Telas mais importantes

| Rota | Quem usa | Objetivo |
| --- | --- | --- |
| `/` | público | home institucional com conteúdo do Storyblok |
| `/landing` | público | landing page institucional |
| `/signIn` | público | entrada da aplicação |
| `/new-account` | público | criação de conta pelo frontend |
| `/reset-forgot` | público | solicitação de recuperação de senha |
| `/reset-password` e `/password/reset` | público | definição de nova senha com token |
| `/customer` | cliente | dashboard da conta, perfis, plano e atividades |
| `/customer/new-plan` | cliente | contratação de assinatura com boleto ou Pix |
| `/admin` | admin | dashboard com indicadores e gráficos |
| `/admin/users` | admin | lista e busca de clientes |
| `/admin/users/[id]` | admin | detalhe do cliente, perfis, plano e ações administrativas |
| `/admin/books` | admin | operação do catálogo de livros |
| `/admin/subscriptions` | admin | acompanhamento das assinaturas Iugu |
| `/admin/groups` | admin | gestão de grupos |
| `/admin/feed` | admin | gestão de feed e atividades |
| `/admin/partners` | admin | gestão de parceiros |
| `/admin/export` | admin | exportação de dados |

## 👤 O que o cliente enxerga

Na área do cliente, a tela principal é `/customer`.

Ela reúne:

- dados básicos do usuário;
- perfis associados;
- informações de plano do sistema, quando existirem;
- botão para iniciar uma nova assinatura;
- atividades vinculadas aos perfis.

Ao entrar em `/customer/new-plan`, o usuário segue a jornada de contratação, com campos de dados pessoais, endereço, opção de boleto ou Pix, suporte a cupom e, em alguns casos, dados de dependente.

## 👑 O que o admin enxerga

Na área administrativa, o ponto de partida é `/admin`.

O admin encontra:

- indicadores de clientes, perfis e assinaturas;
- gráficos de evolução de cadastros e assinaturas;
- listagens recentes de usuários e assinaturas Iugu.

Depois disso, o uso mais comum é navegar pelos módulos do menu lateral para operar clientes, acervo, assinaturas e cadastros auxiliares.

## ⭐ Telas mais críticas para operação

- `/admin/users`: suporte e manutenção de clientes.
- `/admin/users/[id]`: ajustes finos do usuário, inclusive reset de senha pelo admin.
- `/admin/books`: manutenção do catálogo.
- `/admin/subscriptions`: análise operacional de assinaturas.
- `/customer/new-plan`: jornada de conversão e cobrança.

## 📌 Resumo funcional

Se for preciso explicar a aplicação em uma frase: este projeto é o painel web da Tecteca para operação administrativa, gestão de clientes e contratação de acesso à plataforma.

---

← [Voltar ao README](../README.md) · Ver também: [Operações Comuns](OPERACOES_COMUNS.md)