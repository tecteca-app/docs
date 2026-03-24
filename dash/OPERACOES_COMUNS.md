# Operações Comuns

Este guia reúne as ações mais frequentes no uso técnico e operacional do dashboard.

## 🔧 1. Trocar o backend do ambiente

Quando for necessário apontar para local, homologação ou produção, ajuste `URL_REST` em `.env.local` ou nas variáveis do ambiente publicado.

Exemplo:

```env
URL_REST=https://api-homologacao.exemplo.com
```

Depois disso, reinicie a aplicação.

## ✅ 2. Validar se o login está funcionando

Use a rota `/signIn`.

Resultado esperado:

- credenciais válidas de admin redirecionam para `/admin`;
- credenciais válidas de cliente redirecionam para `/customer`;
- erros do backend aparecem em toast.

Se o login falhar mesmo com credenciais corretas, verifique `URL_REST`, disponibilidade do backend e estado dos cookies de autenticação.

## 🧹 3. Limpar a sessão local

Quando a navegação entrar em estado inconsistente, limpe os cookies abaixo no navegador e faça login novamente:

- `app.token`
- `app.refreshToken`
- `app.user`

Isso costuma resolver cenários de sessão expirada, mudança de ambiente ou token inválido.

## 👤 4. Criar ou editar clientes no admin

Fluxo típico:

1. acessar `/admin/users`;
2. usar filtros por nome, tipo e ordenação quando necessário;
3. criar novo usuário por `/admin/users/create`;
4. abrir o detalhe do usuário para editar dados, status, e-mail validado, limite de tokens e outros dados relacionados.

No detalhe do usuário, a tela também expõe perfis, plano do sistema e assinatura Iugu quando existirem.

## 🔐 5. Resetar senha de um usuário pelo admin

O passo a passo completo está em [RECUPERACAO_DE_SENHA_E_RESET_ADMIN.md](RECUPERACAO_DE_SENHA_E_RESET_ADMIN.md), mas o fluxo operacional é:

1. abrir `/admin/users`;
2. entrar no detalhe do usuário;
3. clicar em `Editar`;
4. marcar `Altera Senha`;
5. informar a nova senha e confirmar;
6. salvar.

## 📊 6. Consultar indicadores do negócio

Use `/admin` para acompanhar:

- total de clientes;
- total de perfis;
- assinaturas ativas e inativas em Iugu;
- premium do sistema;
- assinaturas Apple;
- gráficos de cadastros e assinaturas nas últimas semanas.

Essa é a primeira tela para checagem rápida da operação.

## 📚 7. Gerenciar livros

Use `/admin/books` para:

- listar livros;
- abrir o link do livro;
- editar metadados;
- criar novos livros;
- navegar para categorias e fases de leitura.

Esse módulo centraliza a operação editorial do acervo.

## 💳 8. Gerenciar assinaturas

Os pontos principais ficam em:

- `/admin/subscriptions` para assinaturas Iugu;
- `/admin/subscriptions/systems` para planos do sistema;
- `/admin/subscriptions/apple` para assinaturas Apple.

Em geral, essas telas são usadas para suporte, auditoria operacional e acompanhamento de status.

## ⚙️ 9. Gerenciar outras áreas do admin

No menu lateral existem módulos dedicados para:

- personagens e acessórios;
- grupos;
- feed;
- parceiros;
- planos;
- exportação.

Se a dúvida for onde uma manutenção administrativa acontece, o caminho mais comum é começar pelo menu lateral do `/admin`.

## 📝 10. Atualizar conteúdo institucional

As páginas públicas como `/`, `/landing` e `/m` dependem de Storyblok.

Na prática, isso significa:

- textos e blocos institucionais são controlados no CMS;
- quando a estrutura do bloco muda, o ajuste costuma acontecer em `src/storyblok`;
- quando a regra de negócio muda, o ajuste geralmente acontece nas páginas e componentes do dashboard, não no Storyblok.

## 🛒 11. Validar a jornada de assinatura do cliente

Fluxo recomendado de validação:

1. acessar `/customer` autenticado como cliente;
2. clicar em `Realizar Assinatura`;
3. preencher os dados exigidos em `/customer/new-plan`;
4. validar se o backend gera a cobrança;
5. em caso de Pix, conferir geração do QR Code e atualização posterior do status.

## ✉️ 12. Conferir ativação de conta

Após um cadastro novo, o backend pode exigir validação de usuário por meio da rota `/user-validate?active=...`.

Se o usuário relatar que não consegue entrar logo após o cadastro, vale verificar se a conta já foi validada.

---

← [Voltar ao README](../README.md) · Ver também: [Recuperação de Senha e Reset pelo Admin](RECUPERACAO_DE_SENHA_E_RESET_ADMIN.md)