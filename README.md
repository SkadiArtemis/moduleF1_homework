# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).


--------------------------
MY NOTES
--------------------------
1. Create app (in console):
   
    **$** npx create-react-app --template typescript my_first_react_app

2. src/index.tsx:

        import React from 'react';
        import ReactDOM from 'react-dom/client';
        import './index.css';
        import App from './App';

        const root = ReactDOM.createRoot(
            document.getElementById('root') as HTMLElement
        );
        root.render(<App />);

3. src/App.tsx:

        import React from 'react';

        function App() {
            return (
                    <h1>Hello React</h1>
            );
        }

        export default App;

4. To test set up configurations type in console:
   
   **.../my_first_react_app$** npm start


5. Install [tailwind](https://tailwindcss.com/docs/installation)



----------------------------
My notes based on SF lecture
----------------------------
1. in the project directiory (e.x. my_first_react_app) create dirs:
   > components
   
   > styles
2. > $ npm init -y

    create scripts for **package.json**

        "scripts": {
            "start": "webpack --mode=development --watch",
            "build": "webpack --mode-production",
            ...
            ...
        },

3. > $ npm i webpack webpack-cli -D
4. > $ npm install @babel/core babel-loader @babel/preset-env @babel/preset-react
5. > $ npm install react react-dom
6. >**./$** touch <b>webpack.config.js</b>
   
            const path = require('path');

            module.exports = {
                mode: 'development',
                entry: "./src/index.js",
                output: {
                    path: path.join(__dirname, "/dist"),
                    filename: "bundle.js"
                },
                module: {
                    rules: [
                        {
                            test: /\.js$/,
                            exclude: /node_modules/,
                            use: {
                                loader: "babel-loader"
                            }
                        },
                        {
                            test: /\.css$/,
                            use: ["style-loader", "css-loader"]
                        }
                    ]
                }
            };

7. npm install style-loader css-loader
8.  > **/src$** touch <b>index.html</b>

            <!DOCTYPE html>
            <html lang="en">
            <head>
                <meta charset="utf-8" />
                <title>F1. React</title>
            </head>
            <body>
                <div id="root"></div>
            </body>
            </html>

9.  > **/src/components$** touch **App.js**

            import React, {Component} from "react"; // from React import Component


            class App extends Component {
                render() {
                    return (
                        <div>
                            <h1>Hello React</h1>
                        </div>
                    )
                }
            }

            export default App;

10. > **/src/styles$** touch **App.css**
    
            div {
                padding: 10px;
            }

            h1 {
                text-align: center;
                color: darkblue;
            }    

    > import styles to **App.js**      

            ...
            import "../styles/App.css"
            ...


11. > **/src$** touch **index.js**
    
 
    **index.js** подключает **App.js** к **index.html** с помощью ReactDOM, поэтому нам необходимо их импортировать.

    Все компоненты собираются в **App.js**.

    **App.js** - это верхний уровень, внутрь которого подгружаются
    остальные компоненты.
    Далее, всё рендерится с помощью ReactDOM и подвязывается
    к **index.html** через **\<div id="root">**


        import React from "react";
        import ReactDOM from "react-dom"; 
        import App from "./components/App.js"


        ReactDOM.render(<App/>, document.getElementById("root"));


12.  > npm i html-webpack-plugin
    
        добавляем в <b>webpack.config.js</b> HtmlWebpackPlugin для рендеринга страницы:

                ...
                const HtmlWebpackPlugin = require("html-webpack-plugin");

                module.exports = {
                    ...
                    plugins: [
                        new HtmlWebpackPlugin({
                            template:"./src/index.html"
                        })
                    ]

                };

13. Установим webpack сервер, чтобы не делать каждый раз перезагрузку страницы:
    > npm install webpack-dev-server

    make changes to *start script* in **package.json** file:

        "scripts": {
            "start": "webpack-dev-server --mode development --open",
            ...
            ...
        },


--------------------------
VirtualDOM
--------------------------
Если репозиторий был скачан, то сначала нужно выполнить команду:

### `npm install`

Главный файл React --> **index.js**. 
В него импортируется компонент **App.js**

        index.js
            ^
            |
            | 
            App.js
                ^
                | 
                | App.css, 
                | class App
                |
                |
              Header.js
                    ^
                    |
                    | Header.css
                    | class Header
                    |



1. Добавим header в компонент реката.
   Для этого, в папке components создадим новый файл **Header.js**:

    > **./src/components$** touch Headers.js

    и добавим в него следующие строки:
   
        import React, {Component} from "react";
        import "../styles/Header.css"


        class Header extends Component {

            render(){
                return(
                    <header>This is header</header>
                )
            }
        }

        export default Header

        
     * В начале импортируем объект Components из React

     * Создаем новый класс для нашего компонента, который расширяет объект Component из библиотеки React

     * Далее рендерим JSX код в HTML используя функцию render()

    <hr>

    ### Теперь добавим стили к данному компоненту, создав файл: 
    > **/src/styles$** touch **Header.css**:


        @import "App.css";


        header {
            color: wheat;
            background-color: rgb(29, 41, 26);
            font-size: 40px;
            height: 60px;
            text-align: center;
            display: flex;
            justify-content: center;
            align-items: center;
        }

    <hr>

    ### Теперь добавим вновь созданный объект Header к нашему базовому компоненту **App.js**:

            import React, { Component } from "react";
            import "../styles/App.css";

       ---> import Header from "./Header.js";

            class App extends Component {
                render() {
                    return (
                        <>
                      ----> <Header />
                            <main>
                                <div>
                                    <h1>Hello React</h1>
                                </div>
                            </main>
                        </>
                    )
                }
            }

            export default App;

2. Вынесем \<main>...\</main> из файла **App.js**
   
   > для этого, создадим файл: **./src/components$** touch **Main.js**
   
   и перенесем из App.js весь внутри тега **\<main>...\</main>**

        import React, { Component } from "react";


        class Main extends Component{
            render(){
                return(
                    <div>
                        <h1>Hello Main</h1>
                    </div>
                )
            }
        }

        export default Main

    <hr>
    
    перенесем стили из **App.css** в **Main.js**: 
    > **./src/styles$** touch **Main.js**

    

        /* импортирую стили из файла */
        @import "App.css";


        h1 {
            text-align: center;
            color: rgb(2, 14, 6);
        }

    <hr>
    В результате файлы **App.css** и **App.js** будут выглядеть так:

    > App.css

        /* подключение локальных шрифтов */
        @font-face {
            src: url('../../fonts/OpenSans-Regular.ttf');
            font-family: "OpenSans Regular";
        }

        @font-face {
            src: url('../../fonts/OpenSans-Bold.ttf');
            font-family: "OpenSans Bold";
        }

        @font-face {
            src: url('../../fonts/OpenSans-ExtraBold.ttf');
            font-family: "OpenSans ExtraBold";
        }


        html,
        body {
            padding: 10px;
            margin: 10px;
        }

    > App.js

        import React, { Component } from "react"; // from React import Component

        // import styles
        import "../styles/App.css";

        // import Header object
        import Header from "./Header.js";

        // import Main object
        import Main from "./Main.js"

        class App extends Component {
            // React renders jsx --> html
            render() {
                return (
                    <>
                        {/* using Header object */}
                        <Header />
                        <Main />
                    </>
                )
            }
        }

        export default App;


<h3>3. В <b>Header.js</b> класс Header переделаем в функцию и добавим вызов действия в консоль при нажатии на кнопку:</h3>

        import React, { Component } from "react";
        import "../styles/Header.css";

        function Header() {

            let buttonName = "Click Here!"

            const handleClick = () => {
                console.log('hello');
            }

            return (
                <header>
                    This is header
                    <button className="click-here" onClick={handleClick}>{buttonName}</button>
                </header>
            )
        }

        export default Header
<hr>

## props

Передать переменную из App.js в Header.js можно посредствам параметра **props**

> App.js

        ...
        ...

        class App extends Component {
            
            render() {
                return (
                    <>
                ---->   <Header buttonName={"Click Here!"}/>
                        <Main />
                    </>
                )
            }
        }

        export default App;
> Header.js

Через ключевое слово **props**, функция получает передаваемые ей из **App.js** параметры.

В данном случае, из **App.js** в **props** передается аргумент **buttonName**,
который вызывается через переменную **props.buttonName**:

        ...
        ...

      --->  function Header(props) {
                let [count, setNewCount] = useState(0);
                const handleClick = () => {
                    setNewCount(count + 1)
                };

                return (
                    <header>
                        This is header
                        <button className="click-here" onClick={handleClick}>
                    ---->    {props.buttonName}, is clicked: {count} times
                        </button>
                    </header>
                )
            }

            export default Header

<hr>
<h2>Countries</h2>
Add example with downloading countries

1. In order to download from the internet, we are using here **axios**

    ### `npm install axios`

2. Add new component:

    ### <h4 style="color:lightgreen">**./src/components$** touch **Countries.js**</h4><br>

    > Countries.js

        import React from "react";

        function Countries() {
            // get countries from web
            

            return (
                <h1>Hello</h1>
            )
        }

        export default Countries;

3. Using **Countries** in **Main.js**:
    
    > Main.js

        import React from "react";
        import "../styles/Main.css"
        import Countries from "./Countries";


        function Main() {

            return (
                <main>
            --->    <Countries />
                </main>
            )
        }


        export default Main

<hr>

##  **Create beautiful table with bootstrap**

### `npm install react-bootstrap bootstrap`

<br>

1. Import table styles from bootstrap to js file:

    > Countries.js

        import Table from 'react-bootstrap/Table'

        ...
        ...

           return (
                <Table>
                    ...
                    ...
                    ...
                </Table>
            )
        
        ...

2. import styles from bootstrap to **App.js**

    > App.js

        
        import "bootstrap/dist/css/bootstrap.min.css"

<hr>

## **Add/Remove to the beautiful table**

### <h4 style="color:lightgreen">>> **./src/components$** touch **Country.js**</h4>

<br>

#### `Country.js`

        import React, { useState } from "react";
        import Button from 'react-bootstrap/Button'
        import "../styles/Country.css"


        function Country(props) {
            const [selected, addCity] = useState(false);

            return (
                // if selected = true: className = "selected-country", else: className = "nothing"
                <tr className={!selected ? "" : "selected-country"}>
                    <td>{props.country.city}</td>
                    <td>{props.country.country}</td>

                    <td>
                        { !selected ? 
                            <Button variant="success" onClick={() => addCity(true)}>Add</Button> :
                            <Button variant="danger" onClick={() => addCity(false)}>Remove</Button>
                        }
                    </td>
                </tr>

            )
        }

        export default Country;

#### `Country.css`

        .selected-country{
            background-color: darkgray;
        }

#### `Countries.js`

        ...
        import Table from 'react-bootstrap/Table'
        import Country from "./Country.js"

        function Countries() {
            const [countries, setCountries] = useState([]);

            ...

            return (
                <Table striped bordered hover>

                    <thead>
                        <tr>
                            <th>City</th>
                            <th>Country</th>
                        </tr>
                    </thead>

                    <tbody>
                        {/* 
                        * с помощью map() нужно отрендерить полученный список.
                        * на вход получаем список стране country и возвращаем => в формате jsx
                        */}
                        {countries.map(country => <Country key={country.city} country = {country}/>)};

                    </tbody>

                </Table>
            )
        }

        export default Countries;
