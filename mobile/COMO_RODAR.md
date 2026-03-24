# Como Rodar (Setup Local)

Este guia cobre os passos necessários para configurar o ambiente de desenvolvimento e executar o aplicativo Tecteca localmente.

## 1. Pré-requisitos

Antes de começar, certifique-se de que sua máquina atenda aos requisitos para desenvolvimento React Native:
- **Node.js** (versão 20 ou superior recomendada)
- **Yarn** (gerenciador de dependências utilizado pelo projeto)
- **JDK** (Java Development Kit) para Android
- **Android Studio** (com Android SDK e Emulador configurados)
- **Xcode** e **CocoaPods** (Apenas macOS, para desenvolvimento iOS)

Se você ainda não configurou seu ambiente React Native, siga o [Guia Oficial do React Native (React Native CLI)](https://reactnative.dev/docs/environment-setup).

## 2. Instalação das Dependências

Clone este repositório e acesse a pasta raiz (`mobile`). Em seguida, instale as dependências executando:

```bash
yarn install
```

### 2.1. Dependências do iOS (Apenas macOS)

Após a instalação das dependências do Node, é necessário instalar as dependências nativas do iOS através do CocoaPods:

```bash
cd ios
pod install
cd ..
```
*Dica: Se você estiver usando um Mac com chip Apple Silicon (M1/M2/M3), pode ser necessário rodar `arch -x86_64 pod install` dependendo da sua configuração do Ruby, ou apenas `pod install` nas versões mais recentes.*

## 3. Configurando a URL da API (Ambiente)

O projeto atualmente não utiliza um arquivo `.env`. A configuração do URL da API (Dev/Prod) é feita diretamente no arquivo de serviço.

Para alterar o ambiente, edite o arquivo `src/services/api.ts` e modifique a `baseURL`:

```typescript
const api = axios.create({
  // Descomente a linha abaixo para usar o ambiente de desenvolvimento
  // baseURL: 'https://api-dev.tecteca.com.br',
  baseURL: 'https://api.tecteca.com.br',
});
```

## 4. Executando o Aplicativo

### Android

1. Inicie um emulador Android via Android Studio ou conecte um dispositivo físico com a Depuração USB ativada.
2. Em um terminal na raiz do projeto, inicie o Metro Bundler:
   ```bash
   yarn start
   ```
3. Em outro terminal, rode o comando padrão:
   ```bash
   yarn android
   ```

**Alternativa: Gerando a build pelo Gradle**
Se preferir gerar o APK diretamente (ou se o comando acima falhar), você pode usar o `gradlew`:
```bash
cd android
./gradlew assembleDebug
```
*(O APK gerado ficará em `android/app/build/outputs/apk/debug/app-debug.apk`. Para instalar direto no emulador/dispositivo, use `./gradlew installDebug` em vez de `assembleDebug`)*

### iOS (Apenas macOS)

1. Inicie um Simulador iOS ou conecte um iPhone.
2. Inicie o Metro Bundler:
   ```bash
   yarn start
   ```
3. Rode o aplicativo no iOS:
   ```bash
   yarn ios
   ```

## 5. Resolução de Problemas Comuns

- **Erro de cache do Metro Bundler:** Rodar `yarn start --reset-cache`.
- **Erro de build no Android:** Abrir a pasta `android` no Android Studio e deixar o Gradle sincronizar, ou rodar `cd android && ./gradlew clean`.
- **Erro de Pods no iOS:** Rodar `cd ios && pod install --repo-update`.
