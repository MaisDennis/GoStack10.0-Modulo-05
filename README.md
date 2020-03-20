# GoStack 10.0 || Módulo 05

* [1. Conceitos abordados](#1-conceitos-abordados)
* [2. Descrição do projeto](#2-descrição-do-projeto)
* [3. Iniciando o Projeto](#3-iniciando-o-projeto)
* [4. Criando o projeto](#4-criando-o-projeto)

##  1. Conceitos abordados

1. Iniciar um projeto react-app.
2. Incluir ESLint, Prettier & EditorConfig.
3. Criar routes, pages (index e styles).
4. Utilizar Styled components para a estilização.
5. Criação de componentes.
   1. **state = {}, e render() {};**
   2. funções **handleInputChange, handleSubmit**
6. Utilizar a biblioteca axios para fazer requisições API e criar a baseURL.
7. Utilizar localStorage do browser.
   1. **componentDidMount e componentDidUpdate** (Carregar e Salvar no LocalStorage, respectivamente).
8. Utilizar o { Link } from 'react-router-dom'.

##  2. Descrição do projeto

Um site para buscar repositórios no Github, retornando o nome, a descrição e issues atuais presentes no repositório.
A pagina principal cria uma lista de repositórios procurados, e em cada item, traz um link.

### Main
![Main](https://github.com/MaisDennis/GoStack10.0-Modulo-05/blob/master/src/assets/Main.png)

O link "Detalhes" nos leva a uma página contendo o nome, a descrição e issues.

### Repo
![Repo](https://github.com/MaisDennis/GoStack10.0-Modulo-05/blob/master/src/assets/Repo.png)

Cada issue tem um link para a página da respectiva issue no github.
obs. O site tem 2 páginas.

##  3. Iniciando o projeto
```
yarn start
```
<p>

##  4. Criando o projeto

1. Criando o projeto do zero.
   1. Terminal:
      ```
      yarn create react-app modulo05
      ```
      1. webpack, babel se encontram em "react-scripts"
   2. deletar eslintConfig: {}, pois vamos configurar do zero.
   3. ```<div id="root">"``` é onde vai todo o código React.
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
      1. **Add state = {}, e render() {};**
      2. Adicionar as funções: **handleInputChange, handleSubmit**
   2. browser: procurar: github api
      1. https://developer.github.com/v3/
      2. repositories -> get
      ```
      GET /repos/:owner/:repo
      ```
      3. Exemplo: http://api.github.com/repos/rocketseat/unform
   3. **biblioteca axios** serve para fazer requisições API e criar a baseURL: 'http://api.github.com' no ReactJS e React Native.
   ```
   yarn add axios
   ```
   4. Criar src/services/api.js
      1. Import axios
   5. Main/index.js
      1. **Alterar handleSubmit (incluir setState) e state.**
      2. Browser: Inspecionar -> React (ou Components).
         1. Vide o repositório em state (/rocketseat/unform).
      3. desabilitar o botão submit enquanto adiciona repo.
         1. Adicionar loading ao state, handleSubmit, setState, ```<SubmitButton>```
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


8. Listando repositórios
   1. Adicionar o componente List, adicionar const repositories no render().
   2. repositories.map()
   3. Adicionar styles. Vide browser: Lista de repositories c/ link: "Detalhes".

9. Utilizando LocalStorage
   1. Criar as funções **componentDidMount e componentDidUpdate** (Carregar e Salvar no LocalStorage, respectivamente).
   2. Vide browser, F5 e a lista permanece.

10. Navegação de rotas
    1. usando a href=..., o browser vai recarregar a pagina inteira. Não é essa função que queremos, portanto vamos usar um metodo do react-router.
    2. import { Link } from 'react-router-dom'; trocar o componente a por Link.
    3. Alterar routes.js (adicionar /:repository).
    3. Repository/index.js -> decodeURI.

11. Carregando dados da API
    1. Repository/index.js
       1. **Transformar em class**.
       2. **componentDidMount():**
          1. QUeremos puxar "Issues" do hub.
          2. chamada API simultaneo:
          ```Javascript
          const [ repository, issues] = await Promise.all([
            api.get(`/repos/${repoName}`),
            api.get(`/repos/${repoName}/issues`),
          ])
          ```
        3. **Add state**
           1. repository, issues, loading.
           2. {} quando tem 1 unico item. [ ] array para diversos itens.
           3. Add this.setState({}), and const {}.

12. Definindo PropTypes
    1. Repository/index.js
    ```
    yarn add prop-types
    ```
       1. Criar static propTypes = {}.

13. Exibindo repositório.
    1. Criar arquivo Repository/styles.js
    2. Repository/index.js
       1. If loading para não mostrar os dados de Repo enquanto estiver carregando.
    3. Criar src/components/Container/index.js
       1. Importar o componente Container para Main e Repository.
    4. Criar e estilizar o componente Owner.
    5. Criar e estilizar o componente Link para voltar a Main.

14. Exibindo issues
    1. Repository/index.js
       1. Criar e estilizar o componente IssueList.
       2. Criar e estilizar o issue.labels.



