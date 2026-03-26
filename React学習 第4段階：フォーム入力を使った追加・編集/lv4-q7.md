かなりよいです。
方向は合っています。
ただし **2か所修正が必要** です。

---

## 修正点1

ここです。

```jsx
{...u, age : editAge }
```

今回は条件に

* `age` は **数値として保存する**

があるので、`editAge` をそのまま入れるのではなく、**数値化** が必要です。

こうします。

```jsx
{ ...u, age: Number(editAge) }
```

---

## 修正点2

ここです。

```jsx
setEditName("");
```

これは今の state には存在しないのでエラーになります。
正しくは `editAge` を空に戻したいので、

```jsx
setEditAge("");
```

です。

---

## 修正版

```jsx
import { useState } from "react";

const initialUsers = [ 
  { id: 1, name: "Taro", age: 23 }, 
  { id: 2, name: "Hanako", age: 45 }, 
  { id: 3, name: "Jiro", age: 30 }, 
];

export default function App() {
  const [users, setUsers] = useState(initialUsers);
  const [editAge, setEditAge] = useState("");

  const changeBtn = () => {
    if (!editAge.trim()) return;

    setUsers((prev) =>
      prev.map((u) =>
        u.id === 3 ? { ...u, age: Number(editAge) } : u
      )
    );

    setEditAge("");
  };

  return (
    <>
      <input
        type="text"
        value={editAge}
        onChange={(e) => setEditAge(e.target.value)}
      />
      <button onClick={changeBtn}>チェンジ</button>

      <ul>
        {users.map((u) => (
          <li key={u.id}>
            {u.name}-{u.age}
          </li>
        ))}
      </ul>
    </>
  );
}
```

---

## とてもよい点

今回ちゃんとできているのはここです。

* `map` で **id: 3 だけ更新** しようとしている
* `if (!editAge.trim()) return;` で空入力を防いでいる
* 更新後に input を空に戻そうとしている
* JSXで一覧表示できている

つまり、**更新の骨組みはできています。**
今回の修正は主に

* 型の修正
* state名の打ち間違い

です。

---

## ワンポイント

今回は input をこうしても自然です。

```jsx
<input
  type="number"
  value={editAge}
  onChange={(e) => setEditAge(e.target.value)}
/>
```

ただし `type="text"` でも動きます。
大事なのは **保存時に `Number(...)` すること** です。

---

では次に進みます。

# Q7

## テーマ

**active をチェックボックスで編集する**

## 初期データ

```jsx
const initialUsers = [
  { id: 1, name: "Taro", active: true },
  { id: 2, name: "Hanako", active: false },
  { id: 3, name: "Jiro", active: true },
];
```

## 基本形

```jsx
import { useState } from "react";

export default function App() {
  const [users, setUsers] = useState(initialUsers);
  const [checked, setChecked] = useState(false);

  return (
    <>
    </>
  );
}
```

## 問題

次の動きを作ってください。

* チェックボックスを1つ用意する
* 「id: 2 の active を変更」ボタンを押す
* `id === 2` のユーザーの `active` を、チェックボックスの状態で更新する
* 更新後はチェックを `false` に戻す

---

## 条件

* 更新対象は **id が 2 のユーザー固定**
* `map` を使う
* 一覧表示は次の形にする

```jsx
<li key={user.id}>
  {user.name} - {user.active ? "active" : "inactive"}
</li>
```

---

## ヒント

チェックボックスはこれです。

```jsx
<input
  type="checkbox"
  checked={checked}
  onChange={(e) => setChecked(e.target.checked)}
/>
```

更新はこの方向です。

```jsx
setUsers((prev) =>
  prev.map((user) =>
    user.id === 2
      ? { ...user, active: checked }
      : user
  )
);
```

---

あなたのコードを書いて貼ってください。
