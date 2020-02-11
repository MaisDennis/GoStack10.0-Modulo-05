<h1>Criando o projeto:</h1>

1. Criando o projeto
   1. Terminal:
      ```
      yarn create react-app modulo05
      ```
      webpack, babel se encontram em "react-scripts"
   2. deletar eslintConfig: {}, pois vamos configurar do zero.
   3. <div id="root"> é onde vai todo o código React.
   4. Delete: comments, manifest, manifest.json, App.css, App.test.js, index.css, logo, serviceWOrker.js

2. ESLint, Prettier & EditorConfig.
   1. Criar modulo05/.editorconfig
   2. Add/Create Eslint (Popular Language: AirBNB)
      ```
      yarn add eslint -D
      yarn eslint --init
      ```
      1. Excluir package-lock.json e yarn.
      ```
      yarn add prettier eslint-config-prettier eslint-plugin-prettier babel-eslint -D
      ```
      2. modulo05/.eslintrc.js
      ```
      extends: [
        'plugin:react/recommended',
        'airbnb',
        'prettier',
        'prettier/react',
      ],
      parser: 'babel-eslint',
      plugins: [
        'react',
        'prettier',
      ],
      rules: {
        'prettier/prettier': 'error',
        'react/jsx-filename-extension': [
          'warn',
          { extensions: ['.jsx', '.js']}
        ],
        import/prefer-default-export': 'off'
      },
      ```
    3. modulo05/.prettierrc
       ```
       "singleQuote": true,
       "trailingComma": "es5"
       ```

3. Roteamento do React
   1. React Router impede de recarregar toda a pagina (no refresh). Estamos trabalhando em SPA (single page application).
   ```
   yarn add react-router-dom
   ```
   2. Criar src/routes.js, src/pages/Main/index.js, src/pages/Repository/index.js
   3. Alterar App.js

4. Styled components
   1. Add (Vai mudar a forma como escrevemos .css em React e React Native):
    ```
    yarn add styled-components
    ```
   2. Instalar no VS Code: vscode-styled-components.
   3. Criar Main/styles.js
   4. vide o formato de escrever css dentro de um arquivo .js via styled (obs. vide o ``).
   5. Alterar Main/index.js

5. Estilos globais
   1. Criar src/styles/global.js e importar ao App.js

6. Estilizando a página Main
   1. Pacote com varios icones uteis (fontawesome, material icons, wionicons).
   ```
   yarn add react-icons
   ```
   2. import a Main/index.js, alterar Main/styles.js

7. Adicionando repositórios
   1. Main/index.js: Transformando a function Main() em componente Class.
      1. Adicionar as funções: handleInputChange, handleSubmit
   2. browser: procurar: github api
      1. https://developer.github.com/v3/
      2. repositories -> get
      ```
      GET /repos/:owner/:repo
      ```
      3. Exemplo: http://api.github.com/repos/rocketseat/unform
   3. biblioteca axios serve para fazer requisições API e criar a baseURL: 'http://api.github.com' no ReactJS e React Native.
   ```
   yarn add axios
   ```
   4. Criar src/services/api.js
      1. Import axios
   5. Main/index.js
      1. Alterar handleSubmit (incluir setState) e state.
      2. Browser: Inspecionar -> React (ou Components).
         1. Vide o repositório em state (/rocketseat/unform).
      3. desabilitar o botão submit enquanto adiciona repo.
         1. Adicionar loading ao state, handleSubmit, setState, <SubmitButton>
         2. Alterar SubmitButton no styles
         ```
         &[disabled] {
         cursor: not-allowed;
         opacity: 0.6;
         }

         export const SubmitButton = styled.button.attrs(props => ({
         type: 'submit',
         disabled: props.loading,
         }))`
         ```
      4. Add SPINNER, Main/index.js
         1. Main/styles.js
            1. keyframes = animation.
            2. import styled, { keyframes, css } from 'styled-components';


