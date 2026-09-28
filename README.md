# Nuxt Minimal Starter

Look at the [Nuxt documentation](https://nuxt.com/docs/getting-started/introduction) to learn more.

## Atualizações Recentes

**1. Nova Página de Cadastro (`/cadastro`)**
- Criada uma nova rota nativa no Nuxt (`app/pages/cadastro.vue`).
- Adicionado um formulário funcional, responsivo (com Tailwind CSS) e reativo utilizando Vue Composition API.
- Campos implementados: Nome completo, E-mail, Curso/Área, Semestre, Interesses (múltipla seleção) e Bio/Mensagem.
- Adicionado feedback visual na submissão, simulando um carregamento e exibindo mensagem de sucesso antes da limpeza reativa dos dados.

**2. Ajustes de Dependências**
- Corrigidos problemas na instalação e resolução de pacotes relacionados ao módulo SEO do Nuxt.
- Pacotes adjacentes (`unhead` e `nuxt-schema-org`) foram instalados diretamente para garantir que o servidor de desenvolvimento e o script de pré-build (`nuxt prepare`) funcionem sem erros.

## Setup

Make sure to install dependencies:

```bash
# npm
npm install

# pnpm
pnpm install

# yarn
yarn install

# bun
bun install
```

## Development Server

Start the development server on `http://localhost:3000`:

```bash
# npm
npm run dev

# pnpm
pnpm dev

# yarn
yarn dev

# bun
bun run dev
```

## Production

Build the application for production:

```bash
# npm
npm run build

# pnpm
pnpm build

# yarn
yarn build

# bun
bun run build
```

Locally preview production build:

```bash
# npm
npm run preview

# pnpm
pnpm preview

# yarn
yarn preview

# bun
bun run preview
```

Check out the [deployment documentation](https://nuxt.com/docs/getting-started/deployment) for more information.
