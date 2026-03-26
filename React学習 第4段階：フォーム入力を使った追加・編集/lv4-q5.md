
# Q5

## テーマ

**追加ではなく、既存ユーザーの名前を編集する**

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
  const [inputName, setInputName] = useState("");

  return (
    <>
    </>
  );
}
```

## 問題

次の動きを作ってください。

* input に新しい名前を入れる
* 「id: 2 のユーザー名を変更」ボタンを押す
* `id === 2` のユーザーの `name` だけを、input の値に更新する
* 他のユーザーはそのまま
* 更新後は input を空に戻す

---

## 条件

* `inputName` が空文字または空白だけなら更新しない
* 更新対象は **id が 2 のユーザー固定**
* `map` を使って更新する
* 一覧はそのまま表示する

---

## 一覧表示

```jsx
<li key={user.id}>
  {user.name} - {user.age}
</li>
```

---

## ゴール

ここで覚えたいのは
**「追加は [...prev, newUser]」
「1件更新は map」**
という違いです。

---

## ヒント

形はこの方向です。

```jsx
setUsers((prev) =>
  prev.map((user) =>
    user.id === 2
      ? { ...user, name: inputName }
      : user
  )
);
```

---

あなたのコードを書いて貼ってください。
