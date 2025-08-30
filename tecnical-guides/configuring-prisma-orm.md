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
  output   = "./client"
}

// Define a fonte de dados (nosso banco de dados)
datasource db {
  provider = "postgresql" // Usaremos PostgreSQL
  url      = env("DATABASE_URL") // Carrega a URL de conexão do arquivo .env
}

// Exemplo de um modelo de dados.
// Adicione seus modelos aqui.
model User {
  id    String @id @default(uuid())
  email String @unique
  name  String?
}
```

**Importante:** Certifique-se de que a variável `DATABASE_URL` no seu arquivo `.env` está correta e aponta para o contêiner do PostgreSQL. O valor deve ser o mesmo definido no guia do Docker Compose:

```env
DATABASE_URL="postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@localhost:${POSTGRES_PORT}/${POSTGRES_DB}?schema=public"
```

### 4. Usando o Prisma Client

Após configurar o schema, você precisa gerar o Prisma Client para poder usá-lo na sua aplicação. Execute o seguinte comando:

```bash
pnpm exec prisma generate
```

Este comando lê o `schema.prisma` e gera o código do client no diretório de saída especificado (`./prisma/client`).

O client fornece uma API fluente e totalmente tipada para interagir com as tabelas do seu banco de dados.

Como especificamos um diretório de saída customizado, o caminho de importação do `PrismaClient` mudou. Em vez de importar de `@prisma/client`, você deve usar o caminho relativo para o diretório `prisma/client`.

Veja um exemplo de como usá-lo em um arquivo TypeScript na raiz do projeto:

```typescript
import { PrismaClient } from './prisma/client';

const prisma = new PrismaClient();

async function main() {
  // Exemplo: Listar todos os usuários.
  // Nota: A tabela 'User' correspondente ao modelo no schema.prisma
  // deve existir no banco de dados para que esta consulta funcione.
  const allUsers = await prisma.user.findMany();
  console.log('Todos os usuários:', allUsers);
}

main()
  .catch((e) => {
    throw e;
  })
  .finally(async () => {
    await prisma.$disconnect();
  });
```

Com estes passos, o Prisma está configurado para se conectar ao banco e gerar o client.
