# Configuração do Docker Compose

> **Nota Importante**
> Todos os comandos e arquivos neste guia (como `.env` e `docker-compose.yaml`) devem ser criados ou executados de dentro do diretório `app`, que é o diretório raiz do projeto Next.js.

Este guia explica como configurar um ambiente de desenvolvimento local com Docker Compose, incluindo PostgreSQL, Redis, Mailpit e RabbitMQ.

## 1. Crie o arquivo `.env`

Antes de configurar o Docker Compose, crie um arquivo `.env` na raiz do seu projeto com as seguintes variáveis de ambiente:

```env
# PostgreSQL
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_DB=myapp_db
POSTGRES_PORT=5432

# Redis
REDIS_PASSWORD=redispass
REDIS_PORT=6379

# RabbitMQ
RABBITMQ_DEFAULT_USER=rabbit
RABBITMQ_DEFAULT_PASS=rabbitpass
RABBITMQ_DEFAULT_VHOST=/
RABBITMQ_DEFAULT_PORT=5672
RABBITMQ_MANAGEMENT_PORT=15672

# Mailpit
MAILPIT_PORT=1025
MAILPIT_HTTP_PORT=8025

# URLs de Conexão (serão usadas pela aplicação)
DATABASE_URL=postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@localhost:${POSTGRES_PORT}/${POSTGRES_DB}?schema=public
REDIS_URL=redis://:${REDIS_PASSWORD}@localhost:${REDIS_PORT}
RABBITMQ_URL=amqp://${RABBITMQ_DEFAULT_USER}:${RABBITMQ_DEFAULT_PASS}@localhost:${RABBITMQ_DEFAULT_PORT}${RABBITMQ_DEFAULT_VHOST}
```

## 2. Crie o arquivo `docker-compose.yaml`

Crie um arquivo chamado `docker-compose.yaml` na raiz do seu projeto com o seguinte conteúdo:

```yaml
services:
  # Banco de Dados PostgreSQL
  postgres:
    image: postgres:17
    container_name: myapp-postgres
    env_file: .env
    environment:
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_DB: ${POSTGRES_DB}
    ports:
      - "${POSTGRES_PORT}:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U ${POSTGRES_USER} -d ${POSTGRES_DB}"]
      interval: 5s
      timeout: 5s
      retries: 5
    restart: unless-stopped

  # Cache Redis
  redis:
    image: redis:alpine
    container_name: myapp-redis
    command: redis-server --requirepass ${REDIS_PASSWORD}
    env_file: .env
    ports:
      - "${REDIS_PORT}:6379"
    volumes:
      - redis_data:/data
    restart: unless-stopped

  # Servidor de Mensagens RabbitMQ
  rabbitmq:
    image: rabbitmq:3-management
    container_name: myapp-rabbitmq
    env_file: .env
    environment:
      RABBITMQ_DEFAULT_USER: ${RABBITMQ_DEFAULT_USER}
      RABBITMQ_DEFAULT_PASS: ${RABBITMQ_DEFAULT_PASS}
      RABBITMQ_DEFAULT_VHOST: ${RABBITMQ_DEFAULT_VHOST}
    ports:
      - "${RABBITMQ_DEFAULT_PORT}:5672"
      - "${RABBITMQ_MANAGEMENT_PORT}:15672"
    volumes:
      - rabbitmq_data:/var/lib/rabbitmq
      - rabbitmq_logs:/var/log/rabbitmq
    healthcheck:
      test: ["CMD", "rabbitmq-diagnostics", "status"]
      interval: 30s
      timeout: 10s
      retries: 5
    restart: unless-stopped

  # Servidor de Email para Desenvolvimento
  mailpit:
    image: axllent/mailpit:latest
    container_name: myapp-mailpit
    env_file: .env
    ports:
      - "${MAILPIT_PORT}:1025"
      - "${MAILPIT_HTTP_PORT}:8025"
    restart: unless-stopped

# Definindo volumes para persistência de dados
volumes:
  postgres_data:
  redis_data:
  rabbitmq_data:
  rabbitmq_logs:
```

## 3. Executando o Docker Compose para Iniciar os Contêineres

Com os arquivos `.env` e `docker-compose.yaml` prontos, o próximo passo é iniciar todos os serviços de infraestrutura (banco de dados, Redis, etc.) como contêineres.

Execute o seguinte comando para fazer o Docker Compose criar e iniciar tudo em segundo plano (modo "detached"):

```bash
docker compose up -d
```

## 4. Verificando os Serviços

Após a inicialização, você pode verificar o status dos contêineres com:

```bash
docker compose ps
```

## 5. Acessando as Interfaces Web

- **RabbitMQ Management**: http://localhost:15672/
  - Usuário: `rabbit`
  - Senha: `rabbitpass`

- **Mailpit**: http://localhost:8025/

## 6. Parando os Contêineres

Para parar todos os serviços, execute:

```bash
docker compose down
```

Para remover também os volumes (cuidado, isso apagará todos os dados):

```bash
docker compose down -v
```

## Notas Importantes

- As credenciais definidas no arquivo `.env` são para ambiente de desenvolvimento. Em produção, use um gerenciador de segredos adequado.
- O Docker Compose está configurado para reiniciar automaticamente os contêineres em caso de falha (`restart: unless-stopped`).
- Os volumes são usados para persistir os dados entre reinicializações dos contêineres.

Para configurar o Prisma para usar esse banco de dados, consulte o guia de configuração do Prisma.
