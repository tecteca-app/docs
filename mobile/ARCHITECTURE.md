# Estrutura e Arquitetura

O Tecteca Mobile é estruturado para ser escalável e modular, utilizando padrões modernos no ecossistema React Native.

## Estrutura de Pastas (`src/`)

```text
src/
├── assets/       # Arquivos estáticos (imagens, ícones, fontes customizadas)
├── components/   # Componentes reusáveis de UI (Botões, Cards, Inputs)
├── interfaces/   # Tipagens do TypeScript compartilhado (Modelos de domínio, respostas da API)
├── routes/       # Definições do React Navigation (Stacks, Tabs, Tipagem das rotas)
├── screens/      # Páginas principais do aplicativo (Views)
├── services/     # Configuração do Axios e abstrações de comunicação com a API (requests)
├── stores/       # Gerenciamento de estado global com Zustand
└── utils/        # Funções utilitárias, formatadores, máscaras, constantes globais
```

## Arquitetura e Decisões Técnicas

- **Gestão de Estado:** Usamos o [Zustand](https://github.com/pmndrs/zustand) para o estado global simplificado. Ele provê as "stores" que as telas consomem sem a verbosidade do Redux. Para cache e gestão assíncrona da API, as ferramentas recomendam o uso do **TanStack React Query**.
- **Navegação:** O roteamento principal utiliza [React Navigation v7](https://reactnavigation.org/). Na pasta `src/routes`, definimos as pilhas de navegação (Navigators) para separar fluxos de autenticação, fluxos de perfil, etc.
- **Requisições de Rede (API):** Centralizadas em `src/services` utilizando o **Axios**. Tokens de autenticação são passados via interceptors (podem ser lidos do MMKV).
- **Tratamento de Formulários:** Utiliza a stack padrão da indústria: **React Hook Form** junto com **Yup** para validação robusta focada em performance e menor número de _renders_ indesejáveis.
- **Estilização e UI:**
  - **NativeWind (v4):** Utiliza classes do Tailwind CSS dentro dos componentes, mantendo consistência no design system e facilitando a codificação fluída.
  - **Styled Components:** Utilizado com suporte do NativeWind ou para customizações detalhadas, conforme a preferência em partes legadas/específicas.
- **Animações (UX):** As animações da aplicação usam **Moti** e **Reanimated**, garantindo visual de alto nível rodando diretamente na thread de UI (evitando gargalos na ponte JavaScript).
- **Armazenamento Seguro e Caching:** O [React Native MMKV](https://github.com/mrousavy/react-native-mmkv) oferece um armazenamento transacional síncrono extremamente rápido para dados chave-valor (ex: Access Tokens, Configurações de UI).
