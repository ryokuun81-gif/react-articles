とてもよいです。
**Q4は正解です。**

今回はかなり安定しています。
特に、

* `select` を `value` と `onChange` で管理できている
* `selectedGroup` を state に持てている
* 追加後に `"A"` に戻している
* `age` を `Number(inputAge)` で数値化している
* `setUsers((prev) => [...prev, newUser])` に直せている

このあたりがしっかりできています。

---

## よい点

今回のコードは、フォーム入力の基本がかなりそろっています。

### 1. 入力欄ごとに state が分かれている

* `inputName`
* `inputAge`
* `selectedGroup`

これが整理できています。

### 2. controlled component になっている

* `input`
* `select`

どちらも state とつながっているのでReactらしい形です。

### 3. 追加処理の流れが自然

* バリデーション
* id作成
* newUser作成
* state更新
* フォーム初期化

この順番は実務でもよく使います。

---

## 細かい補足

今回はそのままで十分ですが、さらにそろえるなら `maxId` も `prev` から計算できます。

```jsx
setUsers((prev) => {
  const maxId = prev.length > 0 ? Math.max(...prev.map((u) => u.id)) : 0;

  const newUser = {
    id: maxId + 1,
    name: inputName,
    age: Number(inputAge),
    group: selectedGroup,
  };

  return [...prev, newUser];
});
```

ただ、今の段階では
**「追加処理を正しく書けていること」** が大事なので、現状で十分よいです。

---

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
