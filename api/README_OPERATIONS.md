# Guia de Operações Comuns 🛠️

Este guia descreve como realizar as ações mais comuns de gerenciamento de conta e perfis através da API.

---

## 🔐 Gerenciamento de Senha

### 1. Alterar Senha (Usuário Logado)
Para alterar a senha enquanto o usuário está autenticado.

- **Rota:** `PUT /user/:id`
- **Headers:** `Authorization: Bearer <token>`
- **Corpo (JSON):**
  ```json
  {
    "password": "senha_atual",
    "newPassword": "nova_senha"
  }
  ```

### 2. Esqueci minha Senha (Fluxo de Recuperação)
Se o usuário esqueceu a senha, o fluxo segue dois passos:

**Passo A: Solicitar Recuperação**
Envia um e-mail com um token de recuperação.
- **Rota:** `POST /password/forgot`
- **Corpo (JSON):** `{ "email": "usuario@exemplo.com" }`

**Passo B: Resetar Senha**
Utiliza o token recebido no e-mail para definir a nova senha.
- **Rota:** `POST /password/reset`
- **Query Params:** `?token=TOKEN_RECEBIDO`
- **Corpo (JSON):** `{ "password": "nova_senha" }`

---

## 👤 Gerenciamento de Perfis

### 1. Criar novo Perfil
Um usuário pode ter múltiplos perfis (ex: um para cada filho).
- **Rota:** `POST /profile`
- **Corpo (JSON):** `{ "name": "Nome do Perfil" }`

### 2. Editar Perfil
- **Rota:** `PUT /profile/:profile_id`
- **Corpo (JSON):** `{ "name": "Novo Nome" }`

### 3. Excluir Perfil
- **Rota:** `DELETE /profile/:profile_id`
- **Nota:** Esta ação exclui o perfil e todos os dados vinculados a ele (histórico, avatares customizados).

---

## 🚫 Gerenciamento de Conta (Administrativo)

### Excluir Usuário
Apenas usuários com permissão de Admin podem excluir contas de usuários.
- **Rota:** `DELETE /user/:user_id/admin`
- **Headers:** `Authorization: Bearer <admin_token>`

### Alterar Senha de outro Usuário (Admin)
O administrador pode alterar a senha de qualquer usuário sem precisar da senha atual dele.
- **Rota:** `PUT /user/:user_id/admin`
- **Headers:** `Authorization: Bearer <admin_token>`
- **Corpo (JSON):**
  ```json
  {
    "newPassword": "nova_senha_para_o_usuario"
  }
  ```

---

## 📝 Notas Importantes
- Quase todas as operações exigem o header de **Authentication**.
- O parâmetro `:id` ou `:profile_id` deve ser o UUID correspondente ao recurso.
