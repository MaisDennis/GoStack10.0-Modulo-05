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
