
# Q2

## テーマ

**名前と年齢を input から追加する**

## 初期データ

```jsx
const initialUsers = [
  { id: 1, name: "Taro", age: 23 },
  { id: 2, name: "Hanako", age: 45 },
];
```

## 基本形

```jsx
import { useState } from "react";

export default function App() {
  const [users, setUsers] = useState(initialUsers);
  const [inputName, setInputName] = useState("");
  const [inputAge, setInputAge] = useState("");

  return (
    <>
    </>
  );
}
```

## 問題

次の動きを作ってください。

* 名前入力欄がある
* 年齢入力欄がある
* 「追加」ボタンを押す
* `users` に `{ id, name, age }` の形で追加する
* 追加後は両方の input を空に戻す
* 一覧には `名前 - 年齢` の形で表示する

---

## 条件

* `name` が空文字または空白だけなら追加しない
* `age` も空なら追加しない
* `age` は **数値として保存する**
* 一覧表示はこうする

```jsx
<li key={user.id}>
  {user.name} - {user.age}
</li>
```

---

## 出力イメージ

最初は

```jsx
Taro - 23
Hanako - 45
```

`Jiro` と `30` を入れて追加したら

```jsx
Taro - 23
Hanako - 45
Jiro - 30
```

となればOKです。

---

## ヒント

年齢は input から入ると文字列なので、数値化が必要です。

```jsx
Number(inputAge)
```

または

```jsx
const age = Number(inputAge);
```

---


```javascript
あなたのコードを書いて貼ってください。



import { useState } from "react";

const initialUsers = [
  { id: 1, name: "Taro", age: 23 },
  { id: 2, name: "Hanako", age: 45 },
];

export default function App() {
  const [users, setUsers] = useState(initialUsers);
  const [inputName, setInputName] = useState("");
  const [inputAge, setInputAge] = useState("");

  const addUser = () => {
    if (!inputName.trim() || !inputAge.trim()) return;

    const newId =
      users.length > 0 ? Math.max(...users.map((u) => u.id)) + 1 : 1;

    const newUser = {
      id: newId,
      name: inputName.trim(),
      age: Number(inputAge),
    };

    setUsers((prev) => [...prev, newUser]);
    setInputName("");
    setInputAge("");
  };

  return (
    <>
      <input
        type="text"
        value={inputName}
        onChange={(e) => setInputName(e.target.value)}
      />
      <input
        type="number"
        value={inputAge}
        onChange={(e) => setInputAge(e.target.value)}
      />
      <button onClick={addUser}>追加</button>

      <ul>
        {users.map((u) => (
          <li key={u.id}>
            {u.name} - {u.age}
          </li>
        ))}
      </ul>
    </>
  );
}
```
