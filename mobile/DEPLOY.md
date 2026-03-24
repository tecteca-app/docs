# Build para Produção e Deploy

O aplicativo pode ser empacotado para distribuição pela Google Play Store e Apple App Store.

## 1. Configurando Chaves e Certificados

Antes de iniciar os builds, garanta que:
- **Android:** Você precisa configurar o arquivo com as credenciais da sua chave de assinatura (Keystore).
  1. Copie o arquivo de exemplo executando na raiz do projeto:
     ```bash
     cp keystore.properties.exemple keystore.properties
     ```
  2. Edite o arquivo `keystore.properties` recém-criado, substituindo os valores padrão com as credenciais reais do seu certificado `.keystore` (ou `.jks`). O arquivo de chave `.keystore` também deve estar localizado na pasta `android/app` ou conforme especificado no `build.gradle`.
- **iOS:** Você possui a conta de desenvolvedor da Apple configurada no Xcode e os perfis de provisionamento definidos para o App ID e certificados de Distribuição correspondentes.

## 2. Gerando a versão Android

O formato recomendado de publicação na Google Play é o App Bundle (`.aab`).

### Passo a passo (Build APK / AAB)

Abra o terminal e acesse a pasta `android`:

```bash
cd android
```

Para gerar um App Bundle:
```bash
./gradlew bundleRelease
```
O arquivo gerado ficará em: `android/app/build/outputs/bundle/release/app-release.aab`.

Para gerar um APK padrão (Distribuição externa / testes manuais em hardware):
```bash
./gradlew assembleRelease
```
O arquivo gerado ficará em: `android/app/build/outputs/apk/release/app-release.apk`.

### Publicação (Google Play)
Envie o arquivo `.aab` pelo Google Play Console, criando um novo lançamento de produção, teste aberto ou teste fechado.

## 3. Gerando a versão iOS

O build de iOS depende fortemente do uso do Mac.
### Passo a Passo (Build pelo Xcode)

1. Rode `yarn` e `cd ios && pod install` primeiro para garantir os pacotes atualizados.
2. Abra o arquivo `.workspace` (ex: `Tecteca.xcworkspace`) localizado na pasta `/ios` usando o Xcode.
3. No painel de Build Target, selecione a aba **Signing & Capabilities** e verifique se as configurações de assinatura da Apple apontam para seu Team correto para "Release".
4. Defina o dispositivo alvo no topo do Xcode como **Any iOS Device (arm64)**.
5. Vá ao menu superior do seu Mac: **Product > Archive**.
6. Aguarde o fim da compilação. A janela do "Organizer" se abrirá.

### Publicação (App Store Connect)
Da janela do Organizer, valide e distribua o aplicativo pressionando **Distribute App** usando as opções do TestFlight / App Store Connect. Siga as etapas na tela para assinar adequadamente e enviar para a Apple.
