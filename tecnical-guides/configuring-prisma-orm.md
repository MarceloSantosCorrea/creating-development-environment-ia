# Configurando o Prisma ORM

> **Nota Importante**
> Todos os comandos neste guia devem ser executados de dentro do diretório `app`, que é o diretório raiz do projeto Next.js.

Este guia detalha os passos para instalar e configurar o Prisma em nosso projeto, permitindo uma interação type-safe com o banco de dados, conforme decidido no [ADR-0005](../ADR/0005-use-prisma-orm.md).

A configuração irá conectar-se ao banco de dados PostgreSQL provisionado pelo Docker Compose. Para mais detalhes, consulte o [guia de configuração do Docker Compose](./configuring-docker-compose.md).

## Passos

### 1. Instalação

Primeiro, adicione o Prisma CLI como uma dependência de desenvolvimento:

```bash
pnpm add -D prisma
```

### 2. Inicialização do Prisma

Execute o comando a seguir para inicializar o Prisma no projeto:

```bash
pnpm exec prisma init
```

Este comando realiza duas ações principais:
1.  Cria o diretório `prisma/` com um arquivo `schema.prisma` dentro. Este arquivo é onde você definirá seus modelos de dados e a conexão com o banco.
2.  Cria um arquivo `.env` na raiz do projeto (se não existir) e adiciona a variável de ambiente `DATABASE_URL`.

### 3. Configuração do Schema

Abra o arquivo `prisma/schema.prisma` e configure-o. Ele deve se parecer com o seguinte:

```prisma
// This is your Prisma schema file,
// learn more about it in the docs: https://pris.ly/d/prisma-schema

// Define o gerador do Prisma Client, que será em TypeScript
generator client {
  provider = "prisma-client-js"
}

// Define a fonte de dados (nosso banco de dados)
datasource db {
  provider = "postgresql" // Usaremos PostgreSQL
  url      = env("DATABASE_URL") // Carrega a URL de conexão do arquivo .env
}
```

**Importante:** Se o arquivo gerado automaticamente contiver a linha `output = "../src/generated/prisma"` no bloco `generator client`, remova essa linha para usar o diretório padrão do Prisma.

**Importante:** Certifique-se de que a variável `DATABASE_URL` no seu arquivo `.env` está correta e aponta para o contêiner do PostgreSQL. O valor deve ser o mesmo definido no guia do Docker Compose:

```env
DATABASE_URL="postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@localhost:${POSTGRES_PORT}/${POSTGRES_DB}?schema=public"
```

### 4. Usando o Prisma Client

Após configurar o schema, você precisa gerar o Prisma Client para poder usá-lo na sua aplicação. Execute o seguinte comando:

```bash
pnpm exec prisma generate
```

Este comando lê o `schema.prisma` e gera o código do client no diretório padrão.
