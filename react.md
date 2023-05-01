-------------------------useState---------------------------
// useStateはReactのフックで関数コンポーネントで状態管理を行える
import { useState } from 'react';
import './App.css'
// Appコンポーネントの定義
function App() {
  // count という状態変数と、その状態を変更するための setCount 関数を作成。setCountは変数countを更新するためのきっかけがなにかを定義する。
  // useState は引数として状態の初期値0を受け取り、状態変数をその状態を更新する関数のペアを返す。
  // count0 VDOM(前)　→　count1 VDOM(後) 差分の検出を行う
  const [count, setCount] = useState(0);

  // handleClick 関数を定義します。この関数は、ボタンがクリックされたときに呼び出されます。
  const handleClick = () => {
    // handleClick 関数内で setCount を使って count の値を 1 ずつ増やします。(count更新のきっかけ)
    setCount(count + 1);
  };

  // アプリケーションが表示する JSX を返します。
  return (
    <div className='App'>
      <h1>UseState</h1>
      // ボタンを作成し、handleClick 関数がクリック時に実行されるように設定します。
      // onClickは、Reactで使用されるイベントハンドラの一種で、ユーザーが要素をクリックしたときに発生するイベントを処理するために使われます。
      <button onClick={handleClick}>＋</button>
      // 現在の count の値を表示する p 要素を作成します。
      <p>{count}</p>
    </div>
  );
};

// 他のファイルから App コンポーネントをインポートできるように、デフォルトエクスポートします。
export default App;
