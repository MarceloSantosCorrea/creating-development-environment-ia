# 0007: Adoção do Zod para Validação de Dados

*   **Status:** Aceito
*   **Data:** 2025-08-30

## Contexto

Em uma aplicação TypeScript, é crucial validar dados que vêm de fontes externas (ex: requisições HTTP, formulários, variáveis de ambiente) para garantir que eles correspondam aos tipos esperados antes de serem processados. Confiar apenas nos tipos do TypeScript não é suficiente, pois eles são removidos em tempo de execução.

## Decisão

Decidimos adotar a biblioteca **Zod** para a declaração de esquemas e validação de dados em todo o projeto.

## Consequências

### Positivas:

*   **Validação e Inferência de Tipo:** Zod permite declarar um esquema uma única vez e infere automaticamente o tipo estático do TypeScript a partir dele. Isso elimina a necessidade de declarar tipos e validadores separadamente, mantendo-os sempre sincronizados.
*   **API Intuitiva:** A API do Zod é fluente, declarativa e fácil de ler, tornando a criação de esquemas de validação complexos uma tarefa simples.
*   **Integração com TypeScript:** Foi construído do zero com o TypeScript em mente, oferecendo uma experiência de desenvolvimento superior com excelente auto-complete e checagem de tipos.
*   **Sem Dependências:** É uma biblioteca pequena e sem dependências, o que mantém o bundle final leve.
*   **Mensagens de Erro Claras:** Fornece mensagens de erro detalhadas por padrão, facilitando a depuração de dados inválidos.

### Negativas:

*   **Nova Dependência:** Adiciona outra dependência ao projeto.
*   **Curva de Aprendizagem:** Embora a API seja simples, a equipe precisará aprender a sintaxe e os diferentes métodos de validação disponíveis no Zod.
*   **Overhead de Execução:** Como toda validação em tempo de execução, há um pequeno overhead de performance. No entanto, o benefício de garantir a integridade dos dados supera em muito esse custo.
