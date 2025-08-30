# 0003: Adoção do Husky para Gerenciamento de Git Hooks

*   **Status:** Aceito
*   **Data:** 2025-08-30

## Contexto

Para garantir a qualidade e a consistência do código em nosso repositório, é crucial que verificações como linting e testes sejam executadas antes que o código seja enviado (commit/push). Realizar essas verificações manualmente é ineficiente e propenso a erros humanos.

## Decisão

Decidimos adotar a biblioteca **Husky** para automatizar o gerenciamento e a execução de Git hooks.

## Consequências

### Positivas:

*   **Automação de Qualidade:** O Husky permite a execução automática de scripts (ex: `lint`, `test`) em eventos específicos do Git, como `pre-commit` e `pre-push`.
*   **Prevenção de Erros:** Impede que código que não atende aos padrões de qualidade (falha no lint ou nos testes) seja introduzido na base de código.
*   **Configuração Centralizada:** A configuração dos hooks é feita diretamente no `package.json` ou em arquivos dedicados no diretório `.husky/`, mantendo a configuração versionada e consistente para toda a equipe.
*   **Integração:** Funciona muito bem em conjunto com outras ferramentas, como `lint-staged`, para executar verificações apenas nos arquivos modificados, otimizando o tempo de execução.

### Negativas:

*   **Nova Dependência:** Adiciona mais uma dependência de desenvolvimento ao projeto.
*   **Aumento no Tempo de Commit:** O processo de commit pode se tornar um pouco mais lento, pois precisará aguardar a execução dos scripts configurados. No entanto, esse tempo é um investimento na qualidade do código.
*   **Configuração Inicial:** Requer uma configuração inicial para instalar o Husky e definir os hooks desejados.
