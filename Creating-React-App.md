# Creating a React App
  
## create-react-app
使用create-react-app來建立 React app，它簡化了一些工作。需求版本 node >= 8.10 和 npm >= 5.6，利用npx指令。  

```
npx create-react-app project-name
cd project-name
npm start
```
  
## 從零開始建立
首先建立 React app的目錄，然後使用npm init 來initialize 專案，同時可順便進行 git init。  

```
$mkdir exApp
$cd exApp
$npm init	//然後會進行這專案 package.json一些設定
$npm install --save body-parser express morgan qs	//安裝基本套件
```
![image for npm init]()  

```
$mkdir public		//建立這兩個目錄 for static assets
$mkdir src
```

### Babel
利用Babel 來將ES6+ 轉換到ES5，讓比較舊的瀏覽器也能運作。  

```
$npm install --save-dev babel-core babel-eslint babel-loader babel-preset-es2015 babel-preset-react babel-preset-stage-1
$npm install --save babel-polyfill babel-register
```



### Webpack
Webpack 模組化工具，利用來將你的檔案整合。  
  

```
$npm install --save-dev html-webpack-plugin webpack webpack-dev-server style-loader css-loader babel-loader
```


### ESLint
ESLint 是一個Javascript Linter, Linter 可以用來做語法分析，捉出可能的錯確誤，確保程式碼的品質有一定的水準。  

這邊使用Airbnb的設定。

```
$npm install --save-dev eslint eslint-config-airbnb eslint-loader eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react
```

### React

React Component

```
$npm install --save react react-dom react-router
```

### Redux

State Store

```
$npm install --save redux react-redux react-router redux-actions redux-thunk
$npm install --save-dev redux-logger
```

### Immutable

```
$npm install --save immutable redux-immutable
```
