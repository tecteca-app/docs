# Operações Comuns de Manutenção e Desenvolvimento

Aqui estão listados os comandos úteis usados no dia a dia da manutenção do projeto Tecteca Mobile.

Nas orientações abaixo, use os comandos sempre na raiz do projeto (`mobile/`).

### Testes e Lint
- **Checagem de Qualidade (Lint):**  
  Mapeia problemas de codificação, uso errado de variáveis e formatação:
  ```bash
  yarn lint
  # Se o projeto possuir script pra fix automático (tsc / eslint)
  yarn lint --fix
  ```

### Resolvendo Erros de Cache ("Clear Cache")

Quando ocorrem problemas de pacote/módulo ou mudanças brucas feitas no backend nativo, uma limpeza limpa os dados corrompidos.

- **Limpar o cache do React Native Packager (Metro):**
  ```bash
  yarn start --reset-cache
  ```

- **Limpar o cache do Gradle (Android):**
  ```bash
  cd android
  ./gradlew clean
  cd ..
  ```

- **Limpar as dependências Nativas no iOS:**
  ```bash
  cd ios
  rm -rf Pods
  rm -rf Podfile.lock
  pod install --repo-update
  cd ..
  ```

### Instalação Limpa de Pacotes Node
Se existir problema relacionado às extensões JS de pacotes NPM / Yarn:

```bash
rm -rf node_modules
rm yarn.lock
yarn cache clean
yarn install
```

### Checando Portas Ocupadas
Se erro `"Port 8081 already in use"` (Metro server em uso no fundo):

**No MacOS/Linux:**
```bash
lsof -i :8081
# Pega o PID na saída do comando acima, digamos 1234
kill -9 1234
```

**No Windows:**
```powershell
netstat -ano | findstr :8081
# Pega o PID final na saída do comando acima, digamos 12345
taskkill /PID 12345 /F
```
