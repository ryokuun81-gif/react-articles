
# Q9

## テーマ

**selectで編集対象を選び、age を変更する**

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
  const [inputAge, setInputAge] = useState("");

  return (
    <>
    </>
  );
}
```

## 問題

次の動きを作ってください。

* `select` で編集したいユーザーの id を選ぶ
* input に新しい age を入れる
* 「年齢を変更」ボタンを押す
* 選ばれた id のユーザーの `age` を更新する
* 更新後は input を空に戻す

---

## 条件

* `inputAge` が空文字または空白だけなら更新しない
* `age` は **数値で保存**
* `map` を使って1件更新
* `selectedId` は文字列で持っても数値で持ってもよい

---

## 一覧表示

```jsx
<li key={user.id}>
  {user.id} / {user.name} / {user.age}
</li>
```

---

## ヒント

更新はこの方向です。

```jsx
setUsers((prev) =>
  prev.map((user) =>
    user.id === Number(selectedId)
      ? { ...user, age: Number(inputAge) }
      : user
  )
);
```

---

コードを書いて貼ってください。
