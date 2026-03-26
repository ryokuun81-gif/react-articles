
# Q8

## テーマ

**編集対象の id を select で選んで、name を変更する**

## 初期データ

```jsx
const initialUsers = [
  { id: 1, name: "Taro", age: 23 },
  { id: 2, name: "Hanako", age: 45 },
  { id: 3, name: "Jiro", age: 30 },
];
```

## 基本形

```jsx
import { useState } from "react";

export default function App() {
  const [users, setUsers] = useState(initialUsers);
  const [selectedId, setSelectedId] = useState("1");
  const [inputName, setInputName] = useState("");

  return (
    <>
    </>
  );
}
```

## 問題

次の動きを作ってください。

* `select` で編集したいユーザーの id を選ぶ
* input に新しい名前を入れる
* 「名前を変更」ボタンを押す
* 選ばれた id のユーザーの `name` を更新する
* 更新後は input を空に戻す
* `select` はそのままでよい

---

## 条件

* `inputName` が空文字または空白だけなら更新しない
* `selectedId` は `select` から来るので文字列です
* 比較時は数値に変換してもよいです
* `map` を使って1件更新してください

---

## 一覧表示

```jsx
<li key={user.id}>
  {user.id} / {user.name} / {user.age}
</li>
```

---

## ヒント

`select` はこんな形です。

```jsx
<select
  value={selectedId}
  onChange={(e) => setSelectedId(e.target.value)}
>
  <option value="1">1</option>
  <option value="2">2</option>
  <option value="3">3</option>
</select>
```

更新の形はこの方向です。

```jsx
setUsers((prev) =>
  prev.map((user) =>
    user.id === Number(selectedId)
      ? { ...user, name: inputName }
      : user
  )
);
```

---

コードを書いて貼ってください。
