# 0001: Adoção do PNPM como Gerenciador de Pacotes

*   **Status:** Aceito
*   **Data:** 2025-08-30

## Contexto

O projeto necessita de um gerenciador de pacotes para Node.js que seja rápido, eficiente no uso de espaço em disco e que lide bem com monorepos (workspaces). As opções mais comuns são NPM, Yarn e PNPM.

## Decisão

Escolhemos adotar o **PNPM** como o gerenciador de pacotes padrão para este projeto.

## Consequências

### Positivas:

*   **Eficiência de Espaço:** PNPM utiliza um content-addressable storage para armazenar pacotes, o que significa que cada versão de um pacote é salva apenas uma vez no disco, com links simbólicos sendo usados nos projetos. Isso economiza uma quantidade significativa de espaço.
*   **Velocidade de Instalação:** Devido à sua arquitetura, o PNPM é consideravelmente mais rápido na instalação e atualização de dependências em comparação com NPM e Yarn 1.
*   **Estrutura `node_modules` Rígida:** O PNPM cria uma estrutura de `node_modules` não plana, o que evita que pacotes acessem dependências que não foram declaradas explicitamente no `package.json`, tornando o projeto mais robusto e confiável.
*   **Suporte a Workspaces:** Possui um excelente suporte nativo para monorepos (workspaces), o que é um requisito para a escalabilidade futura do nosso projeto.

### Negativas:

*   **Menor Adoção:** Embora esteja crescendo em popularidade, o PNPM ainda é menos utilizado que o NPM e o Yarn, o que pode significar menos suporte da comunidade ou integração com algumas ferramentas mais antigas.
*   **Curva de Aprendizagem:** A equipe pode precisar de um breve período para se familiarizar com os comandos e o funcionamento do PNPM, embora a transição seja geralmente simples.
