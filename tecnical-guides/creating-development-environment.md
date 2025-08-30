# Guia de Criação do Ambiente de Desenvolvimento

Este guia centraliza e ordena todos os passos necessários para configurar um ambiente de desenvolvimento completo para o projeto, desde a criação da aplicação até a configuração das ferramentas de qualidade de código e infraestrutura.

Siga os passos na ordem apresentada e consulte os guias técnicos detalhados para cada etapa.

## Passos

### 1. Criar o Projeto Next.js

O primeiro passo é criar a estrutura base da nossa aplicação front-end com Next.js.

➡️ **Guia Detalhado: [Criando um Projeto Next.js com PNPM](./creating-nextjs-project.md)**

### 2. Instalar e Configurar o Husky

Para garantir a qualidade do código, configuramos o Husky para automatizar a execução de scripts (como o linter) antes de cada commit.

➡️ **Guia Detalhado: [Configurando o Husky para Git Hooks](./configuring-husky.md)**

### 3. Instalar e Configurar o Conventional Commits

Padronizamos as mensagens de commit para melhorar a legibilidade do histórico e automatizar a geração de changelogs. O Commitlint, integrado ao Husky, garantirá esse padrão.

➡️ **Guia Detalhado: [Configurando Conventional Commits com Commitlint](./configuring-conventional-commits.md)**

### 4. Instalar e Configurar o shadcn/ui

Com a base do projeto pronta, configuramos o `shadcn/ui` para gerenciar nossos componentes de UI.

➡️ **Guia Detalhado: [Configurando o shadcn/ui](./configuring-shadcn-ui.md)**

### 5. Configurar o Docker Compose

Para um ambiente de desenvolvimento consistente e isolado, utilizamos o Docker Compose para gerenciar os serviços de infraestrutura, como o banco de dados.

➡️ **Guia Detalhado: [Configuração do Docker Compose](./configuring-docker-compose.md)**

### 6. Instalar e Configurar o Prisma ORM

A interação com o banco de dados é feita de forma segura e tipada através do Prisma ORM.

➡️ **Guia Detalhado: [Configurando o Prisma ORM](./configuring-prisma-orm.md)**

### 7. Criar o Repositório Git e Fazer o Primeiro Commit

Após concluir todas as configurações anteriores, é hora de inicializar o repositório Git e salvar o progresso.

1.  **Inicialize o repositório Git na raiz do projeto:**
    ```bash
    git init
    ```

2.  **Adicione todos os arquivos ao stage:**
    ```bash
    git add .
    ```

3.  **Faça o primeiro commit seguindo o padrão de Conventional Commits:**
    ```bash
    git commit -m "feat: initial project setup"
    ```

Com todos os passos concluídos, seu ambiente de desenvolvimento está pronto.
