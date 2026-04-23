# Acesso SSH e Operação da API com PM2

Este documento explica, com detalhes, como acessar o servidor via SSH usando chave privada, entrar na pasta da API e operar o processo com PM2.

## 1) Pré-requisitos

Antes de iniciar, você precisa ter:

- Acesso ao arquivo da chave privada no Google Drive:
  - https://drive.google.com/drive/folders/13B2fNEchtfyi9nNjVz_PY-BRHctZixgt
- Terminal disponível no seu computador (PowerShell, Prompt de Comando, Git Bash ou terminal Linux/macOS).
- Permissão de acesso ao servidor:
  - Usuário: ubuntu
  - Host: 193.123.117.113
- PM2 instalado no servidor (já utilizado neste ambiente).

## 2) Download e organização da chave SSH

1. Acesse o link do Google Drive.
2. Baixe o arquivo de chave (exemplo: tecteca.key).
3. Salve o arquivo em uma pasta fácil de localizar.

Sugestão no Windows:

- C:/keys/tecteca.key

Sugestão no Linux/macOS:

- ~/keys/tecteca.key

## 3) Ajuste de permissão da chave (importante)

A chave privada deve estar protegida para evitar erro de segurança no SSH.

### Windows (PowerShell)

Se necessário, restrinja permissões no arquivo para o seu usuário.

Comando de conexão normalmente funciona sem ajustes extras em muitos casos no Windows, mas se aparecer erro de permissões, mova a chave para uma pasta privada do usuário e evite compartilhamento do arquivo.

### Linux/macOS

Rode:

```bash
chmod 600 ~/keys/tecteca.key
```

## 4) Conexão SSH no servidor

Use o comando abaixo para acessar:

```bash
ssh -i ./tecteca.key ubuntu@193.123.117.113
```

Observações:

- Esse comando funciona quando o terminal está na mesma pasta do arquivo tecteca.key.
- Se a chave estiver em outro local, use caminho completo.

Exemplo no Windows:

```bash
ssh -i C:/keys/tecteca.key ubuntu@193.123.117.113
```

Exemplo no Linux/macOS:

```bash
ssh -i ~/keys/tecteca.key ubuntu@193.123.117.113
```

Na primeira conexão, pode aparecer confirmação da fingerprint do servidor. Digite yes para continuar.

## 5) Navegar para a pasta da API

Após conectar via SSH:

```bash
cd ~/api-node
pwd
ls
```

Resultado esperado:

- Você deve estar dentro de ~/api-node.
- Deve visualizar arquivos do projeto da API.

## 6) Subir a API com PM2

Comando informado para iniciar o processo:

```bash
pm2 start dist/shared/infra/http/server.js
```

Depois confirme se subiu corretamente:

```bash
pm2 status
```

## 7) Comandos principais do PM2

Abaixo estão os comandos mais usados no dia a dia.

### Ver processos ativos

```bash
pm2 list
```

ou

```bash
pm2 status
```

### Iniciar processo da API

```bash
pm2 start dist/shared/infra/http/server.js
```

### Iniciar definindo nome amigável

```bash
pm2 start dist/shared/infra/http/server.js --name api-tecteca
```

### Reiniciar processo

```bash
pm2 restart <nome-ou-id>
```

Exemplo:

```bash
pm2 restart api-tecteca
```

### Reiniciar todos os processos

```bash
pm2 restart all
```

### Parar processo

```bash
pm2 stop <nome-ou-id>
```

### Parar todos os processos

```bash
pm2 stop all
```

### Remover processo do PM2

```bash
pm2 delete <nome-ou-id>
```

### Remover todos os processos

```bash
pm2 delete all
```

### Ver logs em tempo real

```bash
pm2 logs
```

### Ver logs de processo específico

```bash
pm2 logs <nome-ou-id>
```

### Ver detalhes de um processo

```bash
pm2 show <nome-ou-id>
```

### Monitorar recursos (CPU e memória)

```bash
pm2 monit
```

### Salvar estado atual dos processos

Esse comando salva a lista atual para restaurar após reboot:

```bash
pm2 save
```

### Configurar inicialização automática no boot

```bash
pm2 startup
```

Depois do comando acima:

1. O PM2 exibirá um comando adicional.
2. Copie e execute exatamente o comando exibido.
3. Rode novamente:

```bash
pm2 save
```

## 8) Fluxo recomendado de atualização da API (com PM2)

Fluxo comum para aplicar alteração de código:

1. Entrar no servidor por SSH.
2. Acessar pasta da API:

```bash
cd ~/api-node
```

3. Atualizar código (exemplo com git pull, se aplicável):

```bash
git pull
```

4. Instalar dependências (se necessário):

```bash
npm install
```

5. Gerar build:

```bash
npm run build
```

6. Reiniciar processo no PM2:

```bash
pm2 restart <nome-ou-id>
```

7. Validar status e logs:

```bash
pm2 status
pm2 logs <nome-ou-id>
```

## 9) Troubleshooting rápido

### Erro Permission denied (publickey)

- Confirme usuário e host: ubuntu@193.123.117.113
- Confirme caminho da chave no parâmetro -i
- Verifique se a chave correta foi baixada
- Verifique permissões da chave (principalmente em Linux/macOS)

### Processo não sobe no PM2

- Confirme se o build existe em dist/shared/infra/http/server.js
- Rode build novamente:

```bash
npm run build
```

- Tente iniciar com nome:

```bash
pm2 start dist/shared/infra/http/server.js --name api-tecteca
```

- Confira logs:

```bash
pm2 logs api-tecteca
```

### API sobe e cai em seguida

- Geralmente indica erro de aplicação, variável de ambiente ausente ou falha de conexão externa
- Verificar logs completos:

```bash
pm2 logs <nome-ou-id>
```

- Verificar detalhes:

```bash
pm2 show <nome-ou-id>
```

## 10) Boas práticas de operação

- Sempre usar nome para o processo PM2 para facilitar suporte.
- Após configuração estável, executar pm2 save.
- Evitar usar pm2 delete all em produção sem confirmação.
- Conferir logs após qualquer restart.
- Manter a chave tecteca.key em local seguro, sem versionar no git.

## 11) Comandos essenciais (resumo operacional)

```bash
ssh -i ./tecteca.key ubuntu@193.123.117.113
cd ~/api-node
pm2 start dist/shared/infra/http/server.js --name api-tecteca
pm2 status
pm2 logs api-tecteca
pm2 restart api-tecteca
pm2 save
pm2 startup
```
