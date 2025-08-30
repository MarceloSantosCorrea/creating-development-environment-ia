# Configurando o Husky para Git Hooks

> **Nota Importante**
> Todos os comandos neste guia devem ser executados de dentro do diretório `app`, que é o diretório raiz do projeto Next.js.

Este guia descreve como instalar e configurar o `husky` para automatizar a execução de scripts em hooks do Git, conforme decidido em nosso [ADR-0003](./../ADR/0003-use-husky-for-git-hooks.md).

Usaremos o `husky` para garantir que o linter seja executado antes de cada commit.

## Passos

1.  **Instale e inicialize o Husky**

    O comando a seguir irá adicionar o `husky` como dependência de desenvolvimento e configurá-lo no seu projeto de uma só vez.

    ```bash
    pnpm add --save-dev husky
    pnpm exec husky init
    ```

    Este comando faz o seguinte:
    *   Instala o `husky`.
    *   Cria um script `prepare` no seu `package.json` para habilitar os Git hooks após a instalação.
    *   Cria um arquivo de exemplo `.husky/pre-commit`.

2.  **Configure o Hook `pre-commit`**

    Por padrão, o arquivo `.husky/pre-commit` vem com o comando `npm test`. Precisamos alterá-lo para rodar nosso script de lint.

    > **Nota Importante:** Ao criar ou editar os arquivos de hook do Husky (como `pre-commit` ou `commit-msg`), **não adicione** as linhas `#!/usr/bin/env sh` e `. "$(dirname -- "$0")/_/husky.sh"`. Elas estão obsoletas e serão removidas em futuras versões do Husky. Adicione apenas os comandos que você deseja executar.

    Abra o arquivo `.husky/pre-commit` e substitua o conteúdo por:

    ```bash
    pnpm run lint
    ```

Com isso, o `husky` está configurado. A cada tentativa de `git commit`, o comando `pnpm run lint` será executado primeiro. Se o lint falhar, o commit será abortado.