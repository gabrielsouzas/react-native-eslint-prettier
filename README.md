# Instalação e configuração do ESLint e do Prettier em um projeto com React Native

Este repositório mostra um passo-a-passo para instalar e configurar o ESLint e o Prettier em um projeto React Native.

Este projeto foi criado com o video do canal **[Sujeito Programador](https://www.youtube.com/c/Sujeitoprogramador/)**.

### Links:

-   **[Como configurar Eslint e Prettier com React Native](https://youtu.be/e_nJ5DxZ900)**
-   **[Repositório do video](https://github.com/devfraga/react-native-eslint-prettier)**

## Passo a passo

1. Desistale o que o react native trouxe instalado do eslint.

    - Vá até o `package.json` e encontre os pacotes do `eslint` e execute os comandos para a desinstalação:

        ```bash
        npm uninstall eslint-config-universe
        npm uninstall eslint
        ```

2. Em seguida remova os arquivos `eslintrc.js` e `prettierrc.js` caso existam e reinstale o `ESLint`:

    ```bash
    npm install eslint --save-dev
    ```

3. Depois da instalação execute o comando abaixo para inicializar a configuração do `Eslint`.

    ```bash
    npx eslint --init
    ```

4. Responda ao questionário que aparecer de acordo com as suas preferências.

    - Exemplo:

    ```bash
    # pergunta 1:
    ? How would you like to use ESLint? …
    To check syntax only
    To check syntax and find problems
    ❯❯ To check syntax, find problems, and enforce code style

    # pergunta 2:
    ? What type of modules does your project use? …
    ❯❯ JavaScript modules (import/export)
    CommonJS (require/exports)
    None of these

    # pergunta 3:
    ? Which framework does your project use? …
    ❯❯ React
    Vue.js
    None of these

    # pergunta 4 (selecione "No", porque nesse projeto nao iremos usar TypeScript):
    ? Does your project use TypeScript? ❯ No / Yes

    # pergunta 5: Aqui vai vir com ambos selecionados você pode apertar ESPAÇO do seu teclado para selecionar ou desmarcar uma opção do cmd.
    ? Where does your code run? …
    Browser
    ✔ Node

    # question 6:
    ? How would you like to define a style for your project? …
    ❯❯ Use a popular style guide
    Answer questions about your style
    Inspect your JavaScript file(s)

    # question 7 (Vamos usar o padrao do Airbnb):
    ? Which style guide do you want to follow? …
    ❯❯ Airbnb: https://github.com/airbnb/javascript
    Standard: https://github.com/standard/standard
    Google: https://github.com/google/eslint-config-google

    # question 8:
    ? What format do you want your config file to be in? …
    JavaScript
    YAML
    ❯❯ JSON

    # O cmd final aqui é onde o eslint perguntará se você deseja instalar todas as dependências necessárias. Selecione "YES" e pressione enter:
    Checking peerDependencies of eslint-config-airbnb@latest
    The config that you have selected requires the following dependencies:

    eslint-plugin-react@^7.21.5 eslint-config-airbnb@latest eslint@^5.16.0 || ^6.8.0 || ^7.2.0 eslint-plugin-import@^2.22.1 eslint-plugin-jsx-a11y@^6.4.1 eslint-plugin-react-hooks@^4 || ^3 || ^2.3.0 || ^1.7.0

    ? Would you like to install them now with npm? › No / ❯ Yes
    ```

5. Vá até o arquivo `eslintrc.json` e insira `react-native` em plugins:

    ```json
    "plugins": [
        "react",
        "react-native"
    ],
    ```

6. Em seguida instale o plugin do `react native` do `eslint`:

    ```bash
    npm install --save-dev eslint-plugin-react-native
    ```

7. Crie o arquivo `.eslintignore` para criar um controle dos arquivos que devem ser ignorados pelo `Eslint`.

    - Exemplo:

        ```bash
        # Ignora a pasta de instalação do Node
        node_modules/
        ```

8. Em seguida instale o `Prettier`.

    ```bash
    npm install --save-dev prettier
    ```

9. Para não gerar conflitos de congigurações entre o `prettier` e o `eslint`, instale a seguinte dependência:

    ```
    npm install --save-dev eslint-config-prettier
    ```

10. Vá em `eslintrc.json` e adicione o `prettier:`

    ```json
    "extends": [
            "plugin:react/recommended",
            "airbnb",
            "airbnb/hooks",
            "prettier"
        ],
    ```

11. Crie o arquivo de configuração do `Prettier` `.prettierrc.json`.

    ```json
    {
        "arrowParens": "always",
        "bracketSpacing": true,
        "jsxBracketSameLine": false,
        "jsxSingleQuote": false,
        "quoteProps": "as-needed",
        "singleQuote": true,
        "semi": true,
        "printWidth": 100,
        "useTabs": false,
        "tabWidth": 2,
        "trailingComma": "es5"
    }
    ```

12. Instale ou habilite as extensões do `ESLint` e do `Prettier`.

    - Vá até o arquivo de configuração do `VSCode` através da pesquisa pelo `Ctrl+Shif+P`, digitando `User Settings` na caixa de busca.

    - Acesse o arquivo no formato `JSON`.

    - Insira o código a seguir para forçar o `Eslint` a corrigir o seu código.

        ```json
        "editor.formatOnSave": true,
        "editor.codeActionsOnSave": {
            "source.fixAll.eslint": true
            },
        ```

    - Insira o código a seguir para definir o formatador padrão:

        ```json
        "editor.defaultFormatter": "esbenp.prettier-vscode"
        ```

13. Volte até o `eslintrc.json` para inserir algumas regras que vão evitar acusações de erros desnecessários.

    ```json
    "rules": {
            // permite arquivos .js possuam JSX
            "react/jsx-filename-extension": [1, { "extensions": [".js", ".jsx"] }],

            // Evitar que o eslint reclame sobre a variável "styles" sendo usada antes de ser definida
            "no-use-before-define": ["error", { "variables": false }],

            // Ajustar para nao passar por erros com react-navigation
            "react/prop-types": ["error", {"ignore": ["navigation", "navigation.navigate"]}]
        }
    ```
