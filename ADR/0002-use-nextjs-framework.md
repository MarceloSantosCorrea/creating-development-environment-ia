# 0002: Adoção do Framework Next.js

*   **Status:** Aceito
*   **Data:** 2025-08-30

## Contexto

Precisamos de um framework robusto para o desenvolvimento do front-end da nossa aplicação. Os requisitos incluem renderização no lado do servidor (SSR) para melhor SEO e performance inicial, geração de site estático (SSG) para páginas de conteúdo, e uma ótima experiência de desenvolvimento. A equipe possui familiaridade com React.

## Decisão

Escolhemos adotar o **Next.js** como o framework principal para o desenvolvimento do nosso front-end.

## Consequências

### Positivas:

*   **Performance:** Ganhamos otimizações de performance prontas para uso, como SSR, SSG, e divisão de código (code splitting) automática.
*   **SEO:** A capacidade de renderizar páginas no servidor melhora significativamente a indexação por motores de busca.
*   **Experiência do Desenvolvedor:** O Next.js oferece um ambiente de desenvolvimento rápido e com *hot-reloading*, além de um sistema de roteamento baseado em arquivos que é intuitivo.
*   **Ecossistema:** Sendo baseado em React, temos acesso a um vasto ecossistema de bibliotecas e ferramentas.
*   **Vercel:** Integração nativa com a plataforma Vercel para deploy, o que simplifica o processo de CI/CD.

### Negativas:

*   **Curva de Aprendizagem:** Embora a equipe conheça React, alguns conceitos específicos do Next.js (como `getServerSideProps`, `getStaticProps`) podem exigir um tempo de adaptação.
*   **Opinião Forte:** O Next.js é um framework opinativo, o que pode limitar a flexibilidade em certas customizações mais complexas.
