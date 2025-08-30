# 0005: Adoção do Prisma como ORM

*   **Status:** Aceito
*   **Data:** 2025-08-30

## Contexto

Nossa aplicação precisa de uma maneira segura, eficiente e type-safe para interagir com o banco de dados. Escrever SQL bruto é propenso a erros, difícil de manter e não se integra bem com TypeScript. Precisamos de uma camada de abstração de banco de dados (ORM ou Query Builder).

## Decisão

Decidimos adotar o **Prisma** como nosso principal ORM (Object-Relational Mapper) para a interação com o banco de dados.

## Consequências

### Positivas:

*   **Type-Safety:** O Prisma Client é gerado a partir do schema do banco de dados, fornecendo auto-complete e type-safety de ponta a ponta, o que reduz drasticamente os erros em tempo de execução.
*   **Schema Declarativo:** O schema do Prisma (`schema.prisma`) é intuitivo e serve como uma única fonte de verdade para os modelos de dados, facilitando a visualização e a manutenção.
*   **Migrações:** O Prisma Migrate simplifica o processo de evolução do schema do banco de dados com um sistema de migração declarativo e fácil de usar.
*   **Produtividade do Desenvolvedor:** A API do Prisma Client é moderna e intuitiva, tornando as consultas ao banco de dados mais simples e legíveis.
*   **Introspecção:** Capacidade de gerar o schema do Prisma a partir de um banco de dados existente, facilitando a adoção em projetos legados.

### Negativas:

*   **Abstração:** Como toda abstração, pode haver casos de consultas muito complexas onde o Prisma não é a ferramenta mais performática, exigindo o uso de SQL bruto (`$queryRaw`).
*   **Curva de Aprendizagem:** A equipe precisará se familiarizar com o schema do Prisma, o CLI e a API do Client.
*   **Não é um ORM Tradicional:** O Prisma funciona de maneira diferente de ORMs tradicionais como o TypeORM ou Sequelize (ele é mais um construtor de consultas type-safe), o que pode ser confuso para desenvolvedores com experiência em outros ORMs.
