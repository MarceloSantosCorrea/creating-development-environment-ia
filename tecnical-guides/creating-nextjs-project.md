# Criando um Projeto Next.js com PNPM

Esta guia descreve como iniciar um novo projeto Next.js utilizando o `pnpm`, conforme decidido em nosso [ADR-0001](./../ADR/0001-use-pnpm-package-manager.md).

## Passos

1.  **Crie o projeto Next.js**

    Execute o comando abaixo para criar um novo projeto no diretório `app` com as configurações padrão.

    ```bash
    pnpm create next-app app --yes
    ```

2.  **Remova o repositório Git inicial**

    O `create-next-app` inicia um repositório Git por padrão. É uma boa prática removê-lo para iniciar um novo ou para integrar o projeto a um monorepo existente.

    ```bash
    rm -rf app/.git
    ```
