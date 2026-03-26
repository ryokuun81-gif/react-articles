よいです。
**かなり惜しいです。**
更新の本体はほぼできています。

今回は **3点直すと完成** です。

---

## まずよい点

* `select` の値を受け取れている
* `map` で1件更新しようとしている
* `{ ...user, name: keyword }` の形が書けている
* `onChange` で input と select を state 管理できている

この骨組みはちゃんとできています。

---

## 修正点1

`selectedId` に相当する state がこれです。

```jsx
const [selectId, setSelectId] = useState(false);
```

初期値は `false` より、問題文どおり **文字列の `"1"`** か、数値で統一するなら `1` のほうが自然です。

たとえば問題に寄せるならこうです。

```jsx
const [selectId, setSelectId] = useState("1");
```

今回あなたは `onChange` で `Number(e.target.value)` にしているので、数値で統一するならこうでもOKです。

```jsx
const [selectId, setSelectId] = useState(1);
```

---

## 修正点2

`inputName` が空のときは更新しない条件がまだ入っていません。

つまりここが必要です。

```jsx
if (keyword.trim() === "") return;
```

---

## 修正点3

問題では一覧表示が

```jsx
{user.id} / {user.name} / {user.age}
```

でした。
今は名前だけなので、できればそこも合わせたいです。

---

## 修正版

あなたの書き方に近い形で直すとこうです。

```jsx
import { useState } from "react";

const initialUsers = [
  { id: 1, name: "Taro", age: 23 },
  { id: 2, name: "Hanako", age: 45 },
  { id: 3, name: "Jiro", age: 30 },
];

export default function App() {
  const [users, setUsers] = useState(initialUsers);
  const [selectId, setSelectId] = useState(1);
  const [keyword, setKeyword] = useState("");

  const editSet = () => {
    if (keyword.trim() === "") return;

    setUsers((prev) =>
      prev.map((user) =>
        user.id === selectId ? { ...user, name: keyword } : user
      )
    );

    setKeyword("");
  };

  return (
    <>
      <select
        onChange={(e) => setSelectId(Number(e.target.value))}
        value={selectId}
      >
        <option value="1">1</option>
        <option value="2">2</option>
        <option value="3">3</option>
      </select>

      <input
        type="text"
        value={keyword}
        onChange={(e) => setKeyword(e.target.value)}
      />

      <button onClick={editSet}>編集</button>

      <ul>
        {users.map((u) => (
          <li key={u.id}>
            {u.id} / {u.name} / {u.age}
          </li>
        ))}
      </ul>
    </>
  );
}
```

---

## 補足

今回の問題文は

* `selectedId` は文字列
* 比較時に `Number(selectedId)` してもよい

という条件でした。

でもあなたは最初から

```jsx
onChange={(e)=>setSelectId(Number(e.target.value))}
```

としていて、**stateに数値で入れている** ので、それ自体は全然OKです。
その場合は比較時に `Number(...)` は不要です。

つまり今回のあなたは、

* 問題文の想定: 文字列で持つ
* あなたの実装: 数値で持つ

という違いはありますが、**実装としては自然** です。

---

# 判定

**ほぼ正解。**
不足は

* 空入力ガード
* input のリセット
* 初期値の整え
* 一覧表示の形式

このあたりです。

---

では **Q9** に進みます。

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
