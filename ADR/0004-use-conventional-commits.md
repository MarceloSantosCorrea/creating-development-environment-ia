# 0004: Adoção do Padrão Conventional Commits

*   **Status:** Aceito
*   **Data:** 2025-08-30

## Contexto

À medida que o projeto cresce, o histórico de commits pode se tornar confuso e difícil de navegar. A falta de um padrão claro para as mensagens de commit dificulta a automação de tarefas como a geração de changelogs e o versionamento semântico, além de prejudicar a comunicação sobre as mudanças realizadas.

## Decisão

Decidimos adotar a especificação **Conventional Commits** como o padrão obrigatório para todas as mensagens de commit neste projeto.

## Consequências

### Positivas:

*   **Changelogs Automatizados:** A estrutura do Conventional Commits permite a geração automática de changelogs claros e organizados.
*   **Versionamento Semântico:** Facilita a determinação automática de um novo número de versão (major, minor, patch) com base nos tipos de commits (`feat`, `fix`, `BREAKING CHANGE`).
*   **Melhora na Comunicação:** Torna o histórico do Git mais legível e explícito, ajudando os desenvolvedores a entenderem rapidamente o propósito de cada mudança.
*   **Integração com Ferramentas:** Permite a integração com ferramentas de CI/CD para acionar builds, testes e deploys com base no conteúdo dos commits.

### Negativas:

*   **Curva de Aprendizagem:** A equipe precisará aprender e se acostumar com a sintaxe e os tipos definidos pela especificação.
*   **Rigor:** Exige disciplina da equipe para seguir o padrão de forma consistente. Ferramentas como `commitlint` (integrado com `husky`) podem ser usadas para forçar o cumprimento do padrão, o que pode ser visto como uma barreira inicial.
