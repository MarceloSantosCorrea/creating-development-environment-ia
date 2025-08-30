# 0008: Adoção de shadcn/ui para Componentes de UI

*   **Status:** Aceito
*   **Data:** 2025-08-30

## Contexto

O projeto necessita de uma abordagem para a construção de sua interface de usuário (UI) que seja moderna, flexível, e que nos dê controle total sobre o código dos componentes. As bibliotecas de componentes tradicionais (como Material-UI ou Chakra UI) são excelentes, mas podem nos prender a um sistema de design específico e adicionar dependências de runtime pesadas, dificultando customizações profundas.

Buscamos uma solução que se integre bem com Next.js e Tailwind CSS, e que nos permita construir nossa própria biblioteca de componentes interna sem começar do zero absoluto.

## Decisão

Decidimos adotar **shadcn/ui** como a nossa principal ferramenta para adicionar componentes de UI ao projeto. É importante notar que shadcn/ui não é uma biblioteca de componentes tradicional, mas sim uma coleção de componentes reutilizáveis que são copiados para a nossa base de código através de um CLI.

Esta decisão implica também na adoção do **Tailwind CSS** como nossa principal ferramenta de estilização, pois é um pré-requisito para o shadcn/ui.

## Consequências

### Positivas:

*   **Propriedade Total do Código:** Como os componentes são adicionados diretamente ao nosso repositório (`src/components/ui`), temos controle absoluto para modificá-los e estilizá-los conforme a necessidade do projeto.
*   **Customização Ilimitada:** Usando Tailwind CSS, a customização e a criação de temas são extremamente simples e seguem as melhores práticas de utility-first CSS.
*   **Sem Dependências de Runtime:** shadcn/ui não adiciona um novo pacote ao `node_modules`. O código é nosso, o que mantém o `bundle` final mais leve.
*   **Acessibilidade Garantida:** Os componentes são construídos sobre primitivas de UI acessíveis e não estilizadas do Radix UI, o que nos garante uma base sólida de acessibilidade.
*   **CLI de Alta Produtividade:** O CLI do shadcn/ui facilita a adição de novos componentes de forma rápida e consistente.
*   **Construído com TypeScript:** Garante a integração type-safe com o resto do nosso projeto.

### Negativas:

*   **Responsabilidade de Atualização:** Como o código é nosso, não há um `pnpm update` para receber melhorias ou correções. As atualizações de componentes, se desejadas, precisam ser feitas manualmente, seja rodando o CLI novamente ou comparando as mudanças.
*   **Dependência do Ecossistema (Tailwind/Radix):** Nos acopla ao ecossistema do Tailwind CSS e Radix UI. Embora sejam excelentes ferramentas, exigem familiaridade da equipe.
*   **Não é "Plug-and-Play":** Exige uma abordagem mais prática e uma configuração inicial (Tailwind, utilitários, etc.) em comparação com bibliotecas que vêm com tudo pronto.
