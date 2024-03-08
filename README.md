# Setup de projeto backend em TypeScript

Este guia detalha os passos necessários para configurar um projeto em TypeScript.

1. **Inicialização do Projeto**
   - Inicie um novo projeto Node.js utilizando `yarn`:

     ```bash
     yarn init -y
     ```

2. **Instalação do TypeScript**
   - Adicione TypeScript como dependência de desenvolvimento:

     ```bash
     yarn add -D typescript
     ```

   - Instale as definições de tipo para o Node.js:

     ```bash
     yarn add -D @types/node
     ```

3. **Configuração do Editorconfig**
   - Utilize a extensão do Editorconfig para gerar um arquivo `.editorconfig` para manter a consistência entre diferentes editores.

     ```bash
      root = true

      [*]
      indent_style = space
      indent_size = 2
      end_of_line = lf
      charset = utf-8
      trim_trailing_whitespace = true
      insert_final_newline = true

     ```

4. **Configuração do ESLint**
   - Utilize a extensão ESLint para configurar as regras de linting:

     ```bash
     yarn create @eslint/config
     ```
   - Responda conforme solicitado, mas se quiser usar um style guide tipo o do airbnb, será necessário dizer que o projeto não está utilizando TS:
    ![image](https://github.com/renanholler/setup-project-typescript/assets/51061210/45845b10-eae8-40f4-b4e7-ea37dbbdba64)

   - Caso responder que não está utilizando o TS, será necesário adicionar suporte para ele ao ESLint:

     ```bash
     yarn add -D @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-import-resolver-typescript
     ```

4. **Configuração do Prettier**
   - O Prettier é uma ferramenta que formata automaticamente o código, promovendo consistência e evitando conflitos de estilo em equipes de desenvolvimento.
   - Instale o Prettier e as extensões do ESLint para Prettier:

     ```bash
     yarn add -D prettier eslint-config-prettier eslint-plugin-prettier
     ```

   - Crie um arquivo `.prettierrc` para configurar as opções do Prettier.

     ```bash
     {
       "singleQuote": true
     }
     ```

6. **Lint-staged**
   - Instale o `lint-staged` para executar tarefas de linting em arquivos staged:

     ```bash
     yarn add -D lint-staged
     ```

   - Configure o arquivo `.lintstagedrc.json`.

     ```bash
     {
        "*.{ts}": [
          "prettier --write"
        ]
     }
     ```

7. **Husky**
   - Instale o Husky para automatizar tarefas antes de commits:

     ```bash
     npx husky-init
     yarn
     ```

   - Configure o arquivo `pre-commit` dentro do diretório `.husky`:

     ```bash
     #!/usr/bin/env sh
      . "$(dirname -- "$0")/_/husky.sh"
      
      yarn lint-staged
     ```

8. **Commitlint**
   - Instale o `commitlint` para validar as mensagens de commit seguindo o padrão dos conventional commits:

     ```bash
     yarn add -D @commitlint/{cli,config-conventional}
     ```

   - Crie um arquivo `.commitlintrc` para configurar o `commitlint`.
   - Adicione um gatilho no husky para chamar o commitlint para validar os commits
     
       ```bash
       yarn husky add .husky/commit-msg ‘yarn commitlint —edit ${1}’  
       ```

---

**Conventional Commits**
  - **`build`:** Alterações nas configurações de build (vite, webpack, npm, etc)
  - **`chore`:** Alterações que não modificam código ou testes (arquivos de configuração, ferramentas, bibliotecas, etc)
  - **`ci`:** Alterações nos arquivos de configuração do CI (exemplos Github Actions, Travis, etc)
  - **`docs`:** Alterações apenas na documentação
  - **`feat`:** Uma nova funcionalidade
  - **`fix`:** Uma correção de bug
  - **`perf`:** Uma alteração de código que melhora o desempenho
  - **`refactor`:** Uma alteração de código que não corrige um bug nem adiciona uma funcionalidade
  - **`revert`:** Alterações que desfazem alguma coisa (git revert, por exemplo)
  - **`style`:** Alterações que code style (espaços em branco, formatação, ponto e vírgula faltando, etc)
  - **`test`:** Implementação ou alterações em arquivos de teste

---
Sinta-se à vontade para ajustar qualquer seção conforme necessário e adicionar mais detalhes específicos ao seu projeto.
