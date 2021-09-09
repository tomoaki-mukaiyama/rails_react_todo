# "/"にアクセスした時の処理の流れ  
  
1.[route.rb]  
  ```root to: redirect('/todos')```    
  ```get 'todos', to: 'site#index'```  
  
2.[site/index.html.erb]  
 ```<div id="root"></div>```を生成  
  
application.html.erb  
```<%= javascript_pack_tag 'index' %>```  
  
3.[index.jsx]  
ReactDOM.render(第一引数、第二引数)  
第一引数にコンポーネント  
第二引数にコンポーネントの描画先を指定 (今回は site/index.html.erb の ```<div id="root"></div>```)  
  
```document.addEventListener('DOMContentLoaded', () => {```  
  ```ReactDOM.render(```  
    ```<BrowserRouter>```  
    ```<App/>```  
  
4.[App.js]  
ヘッダー生成、描画  
  ```import { Switch, Route, Link } from 'react-router-dom'```  
  によって使えるこのようにルーティングが書ける  
      ```<Switch>  
          <Route exact path="/todos" component={TodoList} />```  
  
  ```"/todos"```の場合、TodoListを描画する  
  
5.[TodoList.js]  
  
```useEffect```  
  axiosがサーバ(rails)に話しかける  
  jsonを受け取る  
  useStateによって const todosに受け取ったjsonが格納される  
  
フォームに入力された内容に応じて、  
```todos.filter```した結果　(ここがインクリメンタルサーチ機能)  
をそのままチェーンでmapし、  
チェックボックスと編集ボタンと共にtodosが一覧表示される  
  