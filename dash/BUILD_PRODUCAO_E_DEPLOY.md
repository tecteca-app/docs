# Build para Produção e Deploy

Este documento descreve como gerar o build do frontend e quais cuidados tomar ao publicar a aplicação.

## 📋 Requisitos de produção

- Node.js 18 recomendado.
- Yarn 1.22.x.
- Backend REST acessível a partir do ambiente publicado.
- Variável `URL_REST` configurada no ambiente de build e execução.

## ⚙️ Variáveis de ambiente necessárias

```env
URL_REST=https://seu-backend.exemplo.com
```

Sem `URL_REST`, o frontend até pode subir, mas as telas autenticadas e integrações de negócio não vão operar corretamente.

## 🔨 Gerando o build

```bash
yarn install --frozen-lockfile
yarn build
```

Se o build terminar com sucesso, o artefato gerado fica em `.next/`.

## 🚀 Subindo em modo produção

```bash
yarn start
```

Esse comando inicia o servidor Next.js em modo produção. Em infraestrutura própria, o processo normalmente deve ficar atrás de um gerenciador de processo e, se necessário, de um proxy reverso.

## 📋 Fluxo recomendado de publicação

1. Defina `URL_REST` no ambiente de destino.
2. Instale dependências.
3. Execute `yarn build`.
4. Suba a aplicação com `yarn start`.
5. Faça smoke test nas rotas críticas.

## 🧪 Smoke test mínimo pós-deploy

Valide pelo menos estes pontos:

- `/` abre normalmente.
- `/signIn` carrega sem erro de JavaScript.
- o login autentica e redireciona corretamente para `/admin` ou `/customer`.
- `/customer/new-plan` consegue iniciar a jornada de assinatura.
- `/admin` carrega o dashboard.
- `/reset-forgot` aceita um e-mail e chama o backend.

## 🌐 Estratégias de deploy

### ☁️ Deploy em plataforma gerenciada

O projeto é compatível com provedores que executam aplicações Next.js tradicionais, desde que permitam definir variáveis de ambiente e rodar `yarn build` seguido de `yarn start`.

Checklist:

- definir `URL_REST` nas variáveis do projeto;
- confirmar versão do Node compatível;
- manter `yarn.lock` como referência do ambiente.

### 🖥️ Deploy em servidor Node.js

Fluxo comum:

1. publicar o código no servidor;
2. configurar `URL_REST` no ambiente;
3. rodar `yarn install --frozen-lockfile`;
4. rodar `yarn build`;
5. iniciar com `yarn start`;
6. manter o processo com PM2, NSSM, serviço do Windows, systemd ou equivalente da infraestrutura.

## ⚠️ Observações importantes

- O repositório não traz `Dockerfile`. Se a estratégia for container, o contêiner precisa reproduzir os passos de `install`, `build` e `start`.
- Como `typescript.ignoreBuildErrors` está ativo, o build pode passar mesmo com erros de tipagem. Não trate isso como sinal de qualidade por si só.
- O projeto possui integrações sensíveis e dependências externas. Antes de publicar, revise se tokens e chaves estão tratados da forma adequada para o ambiente.
- O deploy só fica saudável se o backend de `URL_REST` estiver estável e acessível a partir do frontend.

## ✅ Checklist final de produção

- `URL_REST` configurado corretamente.
- backend respondendo autenticação e refresh token.
- home pública carregando conteúdo.
- login, dashboard admin e dashboard customer funcionando.
- recuperação de senha funcionando.
- domínio, TLS e proxy reverso validados, quando aplicável.

---

← [Voltar ao README](../README.md)