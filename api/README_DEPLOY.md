# Deploy & CI/CD 🚀

Este projeto utiliza **GitHub Actions** para automatizar o processo de Integração Contínua (CI) e Continuidade de Entrega (CD). O fluxo está definido no arquivo `.github/workflows/ci.yml`.

---

## 🔄 Fluxo de Trabalho

O deploy é disparado automaticamente sempre que há um **push** para a branch `master`.

### Passos do Pipeline:

1.  **Build:**
    - O GitHub Actions prepara um ambiente Ubuntu com Node.js 16.
    - Instala as dependências (`yarn install`).
    - Gera o código transpilado (`yarn build`).

2.  **Transferência:**
    - Os arquivos são enviados para o servidor via SSH usando a action `ssh-deploy`.
    - O destino no servidor é o diretório `~/api-node`.
    - A pasta `node_modules` é excluída da transferência para garantir rapidez.

3.  **Execução no Servidor:**
    - Após a transferência, o GitHub Actions se conecta ao servidor para:
        - Atualizar as dependências no ambiente de produção (`yarn install`).
        - Executar as migrações do banco de dados (`yarn typeorm migration:run`).
        - Reiniciar o processo via **PM2** (`pm2 restart all`).
        - Salvar a configuração do PM2 (`pm2 save`).

---

## 🔐 Configuração do GitHub Secrets

Para que o deploy funcione corretamente, o repositório no GitHub deve ter as seguintes **Secrets** configuradas:

| Secret | Descrição |
| :--- | :--- |
| `SSH_PRIVATE_KEY` | Chave privada SSH para acesso ao servidor. |
| `REMOTE_HOST` | Endereço IP ou hostname do servidor de produção. |
| `REMOTE_USER` | Usuário para conexão SSH (ex: `ubuntu`, `root`). |
| `REMOTE_PORT` | Porta SSH do servidor (padrão: `22`). |

---

## 🖥️ Gerenciamento no Servidor

A API em produção é gerenciada pelo **PM2**. Alguns comandos úteis no servidor:

```bash
# Ver status dos processos
pm2 status

# Ver logs em tempo real
pm2 logs

# Reiniciar a aplicação manualmente
pm2 restart all
```

---

## 📝 Notas de Deploy

- Certifique-se de que as variáveis de ambiente (`.env`) estejam configuradas corretamente no servidor dentro da pasta `~/api-node`.
- O banco de dados deve estar acessível pelo servidor de produção.
