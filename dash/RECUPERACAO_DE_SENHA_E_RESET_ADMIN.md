# Recuperação de Senha e Reset pelo Admin

Este documento separa dois fluxos diferentes que existem no projeto:

- recuperação de senha pelo próprio usuário, via e-mail e token;
- reset manual de senha realizado por um administrador dentro do dashboard.

## 📧 1. Recuperação de senha pelo usuário

### Entrada do fluxo

O usuário começa em `/signIn` e clica em `Esqueceu a senha?`, que leva para `/reset-forgot`.

### Solicitação de recuperação

Na rota `/reset-forgot`:

1. o usuário informa o e-mail;
2. o frontend chama `POST /password/forgot`;
3. o backend envia o link de recuperação;
4. a UI mostra confirmação e volta para o login.

### Reset com token

O projeto possui duas interfaces de reset, ambas ligadas ao mesmo endpoint do backend:

- `/reset-password`
- `/password/reset`

Nas duas telas, o frontend envia `POST /password/reset?token=...` com a nova senha.

### Diferença prática entre as duas telas

- `/reset-password` é uma tela simples e validada por `withSSRGuest`.
- `/password/reset` tem apresentação mais próxima da identidade visual da Tecteca e validação de senha mais forte.

Como ambas apontam para o mesmo endpoint, o que define a experiência em produção é o link enviado pelo backend no e-mail de recuperação.

### Validações relevantes

Dependendo da rota usada, a validação no frontend muda:

- em `/reset-password`, a regra principal é mínimo de 8 caracteres;
- em `/password/reset`, a regra exige mínimo de 6 caracteres, letra maiúscula, letra minúscula e número.

Se o time quiser padronizar a experiência, esse é um bom ponto para alinhar frontend e backend.

### Comportamento esperado após sucesso

Depois que a senha é redefinida com sucesso, o usuário é redirecionado para login ou para a home, conforme a tela utilizada.

### Problemas comuns nesse fluxo

- token expirado ou inválido;
- e-mail não recebido;
- diferença entre as duas rotas de reset causando experiência inconsistente;
- backend recusando a nova senha por regra adicional não refletida no frontend.

## 🔒 2. Reset de senha realizado por admin

Esse fluxo não depende de e-mail nem de token. Ele acontece diretamente dentro da área administrativa.

### Onde fica

O admin faz isso a partir do detalhe do usuário:

1. acessar `/admin/users`;
2. abrir o usuário desejado;
3. clicar em `Editar`;
4. usar o modal de atualização.

### Como funciona

No modal de edição:

1. aparece a opção `Altera Senha` para usuários que não são admin;
2. ao marcar essa opção, surgem os campos `Nova Senha` e `Confirme a senha`;
3. ao salvar, o frontend envia a atualização para `PUT /user/{id}/admin`.

### Regras de senha nesse fluxo

Quando o admin altera a senha, a validação exige:

- pelo menos 6 caracteres;
- pelo menos uma letra maiúscula;
- pelo menos uma letra minúscula;
- pelo menos um número;
- confirmação igual à nova senha.

### Observações operacionais

- Esse reset é imediato e não depende de confirmação por e-mail.
- O ideal é usar esse recurso para suporte administrativo, não como fluxo padrão do usuário final.
- Depois da alteração, o usuário deve autenticar com a nova senha.
- O checkbox de alteração de senha não aparece quando o alvo já é um usuário admin.

### Quando usar cada fluxo

- Use recuperação por e-mail quando o próprio usuário perdeu acesso.
- Use reset pelo admin quando o time de operação precisa intervir diretamente.

### Recomendação de documentação interna

Se houver playbook de suporte, vale registrar nele qual rota o backend envia por e-mail hoje, porque o projeto mantém duas telas de reset em paralelo.

---

← [Voltar ao README](../README.md) · Ver também: [Operações Comuns](OPERACOES_COMUNS.md)