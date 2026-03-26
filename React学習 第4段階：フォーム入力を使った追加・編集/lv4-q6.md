とてもよいです。
**Q5は正解です。**

今回はまさに狙いどおりで、
**「1件更新は `map`」** がきれいに書けています。

## よい点

* `inputName.trim() === ""` で空入力を防げている
* `setUsers((prev) => prev.map(...))` の形が正しい
* `user.id === 2 ? ... : user` で対象だけ更新できている
* `{ ...user, name: inputName }` で他のプロパティを残せている
* 更新後に `setInputName("")` で input をリセットできている

かなり安定しています。

---

## 特によい理解ポイント

今回のコードで大事なのはここです。

```jsx
prev.map((user) =>
  user.id === 2
    ? { ...user, name: inputName }
    : user
)
```

これは、

* 配列全体は作り直す
* でも変えるのは1件だけ
* 変えない要素はそのまま返す

というReactの基本パターンです。

つまり、

* 追加 → `[...]`
* 削除 → `filter`
* 1件更新 → `map`

この区別がかなりできてきています。

---

# Q6

## テーマ

**既存ユーザーの age を input で編集する**

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
  const [inputAge, setInputAge] = useState("");

  return (
    <>
    </>
  );
}
```

## 問題

次の動きを作ってください。

* 年齢入力欄を用意する
* 「id: 3 の年齢を変更」ボタンを押す
* `id === 3` のユーザーの `age` を、input の値で更新する
* 更新後は input を空に戻す

---

## 条件

* `inputAge` が空文字または空白だけなら更新しない
* `age` は **数値として保存する**
* 更新対象は **id が 3 のユーザー固定**
* `map` を使って更新する

---

## 一覧表示

```jsx
<li key={user.id}>
  {user.name} - {user.age}
</li>
```

---

## ヒント

今回のポイントは、`name` 更新と違って **数値化が必要** なことです。

```jsx
Number(inputAge)
```

更新の形はこの方向です。

```jsx
setUsers((prev) =>
  prev.map((user) =>
    user.id === 3
      ? { ...user, age: Number(inputAge) }
      : user
  )
);
```

---

あなたのコードを書いて貼ってください。
