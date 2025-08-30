# Configurando Conventional Commits com Commitlint

> **Nota Importante**
> Todos os comandos e arquivos neste guia devem ser criados ou executados de dentro do diretório `app`, que é o diretório raiz do projeto Next.js.

Este guia descreve como configurar o `commitlint` para forçar o padrão [Conventional Commits](https://www.conventionalcommits.org/) em nosso projeto, conforme decidido no [ADR-0004](./../ADR/0004-use-conventional-commits.md).

A validação será feita automaticamente a cada commit utilizando o `husky`.

## Passos

### 1. Instalação das Dependências

Primeiro, instale as bibliotecas necessárias para o `commitlint`:

```bash
pnpm add -D @commitlint/cli @commitlint/config-conventional
```

*   `@commitlint/cli`: A ferramenta de linha de comando para verificar as mensagens de commit.
*   `@commitlint/config-conventional`: Um conjunto de regras padrão que segue a especificação Conventional Commits.

### 2. Criação do Arquivo de Configuração

Crie um arquivo chamado `commitlint.config.js` na raiz do projeto com as regras personalizadas:

```javascript
// commitlint.config.js
module.exports = {
  extends: ['@commitlint/config-conventional'],
  rules: {
    // Desabilita a regra de limite de caracteres no cabeçalho
    'header-max-length': [0, 'always', Infinity],

    // Força que o tipo do commit seja sempre em minúsculas
    'type-case': [2, 'always', 'lower-case'],

    // Força que o escopo (se houver) seja sempre em minúsculas
    'scope-case': [2, 'always', 'lower-case'],

    // Força que o assunto seja sempre em minúsculas
    'subject-case': [
      2,
      'always',
      'lower-case',
    ],
  },
};
```

### 3. Integração com o Husky

Para que a validação ocorra automaticamente, precisamos adicionar um novo hook ao `husky`. A validação de mensagens de commit deve ocorrer no hook `commit-msg`, que é executado após você escrever a mensagem.

Para mais detalhes sobre a configuração do Husky, consulte o guia [Configurando o Husky para Git Hooks](./configuring-husky.md).

> **Nota Importante:** Ao criar ou editar os arquivos de hook do Husky (como `pre-commit` ou `commit-msg`), **não adicione** as linhas `#!/usr/bin/env sh` e `. "$(dirname -- "$0")/_/husky.sh"`. Elas estão obsoletas e serão removidas em futuras versões do Husky. Adicione apenas os comandos que você deseja executar.

Crie um novo arquivo de hook com o seguinte comando, que já adiciona o script necessário:

```bash
echo "pnpm exec commitlint --edit \$1" > .husky/commit-msg
```

Agora, a cada `git commit`, o `husky` irá acionar o `commitlint` para validar sua mensagem de commit contra as regras definidas. Se a mensagem estiver fora do padrão, o commit será abortado.