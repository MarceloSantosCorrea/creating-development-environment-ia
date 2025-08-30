# Configurando o shadcn/ui (Modo Automatizado)

> **Nota Importante**
> Todos os comandos neste guia devem ser executados de dentro do diretório `app`, que é o diretório raiz do projeto Next.js.

Este guia detalha o processo de inicialização do `shadcn/ui` de forma totalmente automatizada e não-interativa, ideal para garantir consistência na configuração, conforme decidido no [ADR-0008](./../ADR/0008-use-shadcn-ui.md).

## Passo 1: Executar o Comando de Inicialização

O comando a seguir irá configurar o `shadcn/ui` usando as opções padrão, a cor base "Slate", e forçará a criação de todos os arquivos de configuração necessários sem nenhuma interação manual.

```bash
pnpm dlx shadcn@latest init -b slate --yes --defaults --force
```

## Passo 2: Verificar os Arquivos Criados

O comando anterior terá criado e modificado os seguintes arquivos de configuração:

- **`tailwind.config.ts`**
- **`postcss.config.js`**
- **`src/lib/utils.ts`**
- **`src/app/globals.css`**
- **`components.json`**

## Passo 3: Adicionando Componentes

Com a inicialização concluída, você pode adicionar componentes com o comando `add`.

Por exemplo, para adicionar um botão:

```bash
pnpm dlx shadcn@latest add button
```

Este comando irá criar o arquivo `button.tsx` dentro de `src/components/ui`, pronto para ser usado.