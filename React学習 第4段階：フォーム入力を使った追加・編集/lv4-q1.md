では始めます。
**第4段階：フォーム入力を使った追加・編集** です。

今回は **Q1** から、少しずつ進めましょう。

---

# Q1

## テーマ

**input の値を state で管理して、一覧に追加する**

## 初期データ

```jsx
const initialUsers = [
  { id: 1, name: "Taro" },
  { id: 2, name: "Hanako" },
];
```

## 基本形

```jsx
import { useState } from "react";

export default function App() {
  const [users, setUsers] = useState(initialUsers);
  const [inputName, setInputName] = useState("");

  return (
    <>
    </>
  );
}
```

## 問題

次の動きを作ってください。

* input に名前を入力する
* 「追加」ボタンを押す
* `users` に新しいユーザーを追加する
* 追加後は input を空に戻す
* 一覧に名前を表示する

---

## 条件

* 追加するオブジェクトは `{ id, name }`
* `id` は今入っている users の中で最大の id に `+1` したものにする
* `input` が空文字、または空白だけのときは追加しない
* `useState` を使う
* `onChange` と `onClick` を使う

---

## 出力イメージ

最初はこう表示されます。

```jsx
Taro
Hanako
```

input に `Jiro` と入れて追加したら、

```jsx
Taro
Hanako
Jiro
```

となればOKです。

---

## ヒント

必要になる形はこのあたりです。

```jsx
<input
  type="text"
  value={inputName}
  onChange={(e) => setInputName(e.target.value)}
/>
```

```jsx
setUsers((prev) => {
  // 新しい配列を返す
});
```

---


```js
import { useState } from "react";

const initialUsers = [
  { id: 1, name: "Taro" },
  { id: 2, name: "Hanako" },
];

export default function App() {
  const [users, setUsers] = useState(initialUsers);
  const [inputName, setInputName] = useState("");

  const addUser = () => {
    if (!inputName.trim()) return;

    const newId =
      users.length > 0 ? Math.max(...users.map((u) => u.id)) + 1 : 1;

    const newUser = {
      id: newId,
      name: inputName.trim(),
    };

    setUsers((prev) => [...prev, newUser]);
    setInputName("");
  };

  return (
    <>
      <input
        type="text"
        value={inputName}
        onChange={(e) => setInputName(e.target.value)}
      />
      <button onClick={addUser}>追加</button>

      <ul>
        {users.map((u) => (
          <li key={u.id}>{u.name}</li>
        ))}
      </ul>
    </>
  );
}
```