ルートにアクセスした時の処理の流れ
[route.rb]
  root to: redirect('/todos')
  get 'todos', to: 'site#index' *全部'site#index'に流す


'site#index' => siteコントローラのindexアクション  
[site/index.html.erb]
 <div id="root"></div>を生成

application.html.erb
<%= javascript_pack_tag 'index' %>
[index.jsx]
ReactDOM.render(第一引数、第二引数)
第一引数にコンポーネント
第二引数にコンポーネントの描画先を指定 (今回は site/index.html.erb の <div id="root"></div>)

document.addEventListener('DOMContentLoaded', () => {
  ReactDOM.render(
    <BrowserRouter>
    <App/>

[App.js]
ヘッダー生成、描画
  import { Switch, Route, Link } from 'react-router-dom'
  によって使えるこのようにルーティングが書ける
      <Switch>
          <Route exact path="/todos" component={TodoList} />

  "/todos"の場合、TodoListを描画する

[TodoList.js]

useEffect
  axiosがサーバ(rails)に話しかける
  jsonを受け取る
  useStateによって const todosに受け取ったjsonが格納される

フォームに入力された内容に応じて、
todos.filterした結果　(ここがインクリメンタルサーチ機能)
をそのままチェーンでmapし、
チェックボックスと編集ボタンと共にtodosが一覧表示される
