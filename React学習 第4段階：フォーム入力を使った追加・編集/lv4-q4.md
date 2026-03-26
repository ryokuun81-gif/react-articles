かなりよいです。
**ほぼ正解** です。

チェックボックスの扱いもできていますし、

* `checked={isActive}`
* `onChange={(e) => setIsActive(e.target.checked)}`

ここはしっかり書けています。
`active: isActive` もそのままでOKです。

---

## 1か所だけ直したい点

ここです。

```jsx
setUsers((prev) =>[...users, newUser]);
```

これは **関数型更新を使っている形に見えて、実際には `users` を使っている** のが少しズレています。

書くならこうです。

```jsx
setUsers((prev) => [...prev, newUser]);
```

### なぜか

`setUsers((prev) => ...)` と書いたら、
その中では **更新前の最新 state = `prev`** を使うのが基本だからです。

今のコードでもこの問題では動くことが多いですが、Reactでは

* 外側の `users` を使う
* 中の `prev` を使う

が混ざると、今後バグの元になりやすいです。

---

## 修正版

```jsx
import { useState } from "react";

const initialUsers = [
  { id: 1, name: "Taro", age: 23, active: true },
  { id: 2, name: "Hanako", age: 45, active: false },
];

export default function App() {
  const [users, setUsers] = useState(initialUsers);
  const [inputName, setInputName] = useState("");
  const [inputAge, setInputAge] = useState("");
  const [isActive, setIsActive] = useState(false);

  const handleAddUser = () => {
    if (inputName.trim() === "" || inputAge.trim() === "") {
      return;
    }

    const maxId = users.length > 0 ? Math.max(...users.map((u) => u.id)) : 0;

    const newUser = {
      id: maxId + 1,
      name: inputName,
      age: Number(inputAge),
      active: isActive,
    };

    setUsers((prev) => [...prev, newUser]);

    setInputName("");
    setInputAge("");
    setIsActive(false);
  };

  return (
    <div style={{ padding: "20px" }}>
      <div style={{ marginBottom: "20px" }}>
        <input
          type="text"
          placeholder="名前"
          value={inputName}
          onChange={(e) => setInputName(e.target.value)}
        />
        <input
          type="number"
          placeholder="年齢"
          value={inputAge}
          onChange={(e) => setInputAge(e.target.value)}
        />
        <label>
          <input
            type="checkbox"
            checked={isActive}
            onChange={(e) => setIsActive(e.target.checked)}
          />
          Active
        </label>
        <button onClick={handleAddUser}>追加</button>
      </div>

      <ul>
        {users.map((user) => (
          <li key={user.id}>
            {user.name} - {user.age} - {user.active ? "active" : "inactive"}
          </li>
        ))}
      </ul>
    </div>
  );
}
```

---

## 補足

さらに厳密にそろえるなら、`maxId` も `prev` から計算できます。

```jsx
setUsers((prev) => {
  const maxId = prev.length > 0 ? Math.max(...prev.map((u) => u.id)) : 0;

  const newUser = {
    id: maxId + 1,
    name: inputName,
    age: Number(inputAge),
    active: isActive,
  };

  return [...prev, newUser];
});
```

この形だと完全に統一されます。
ただ、今はまず **`prev` を使うなら最後まで `prev`** くらいの感覚で大丈夫です。

---

# Q4

## テーマ

**selectで group を選んで追加する**

## 初期データ

```jsx
const initialUsers = [
  { id: 1, name: "Taro", age: 23, group: "A" },
  { id: 2, name: "Hanako", age: 45, group: "B" },
];
```

## 基本形

```jsx
import { useState } from "react";

export default function App() {
  const [users, setUsers] = useState(initialUsers);
  const [inputName, setInputName] = useState("");
  const [inputAge, setInputAge] = useState("");
  const [selectedGroup, setSelectedGroup] = useState("A");

  return (
    <>
    </>
  );
}
```

## 問題

次の入力を用意してください。

* 名前 input
* 年齢 input
* group を選ぶ `select`
* 追加ボタン

追加するときは、`users` に

```jsx
{ id, name, age, group }
```

の形で追加してください。

---

## 条件

* 名前が空なら追加しない
* 年齢が空なら追加しない
* `age` は数値にする
* `group` は `"A"`, `"B"`, `"C"` から選べるようにする
* 追加後は

  * 名前を空に戻す
  * 年齢を空に戻す
  * group は `"A"` に戻す

---

## 一覧表示

```jsx
<li key={user.id}>
  {user.name} - {user.age} - {user.group}
</li>
```

---

## ヒント

`select` はこんな形です。

```jsx
<select
  value={selectedGroup}
  onChange={(e) => setSelectedGroup(e.target.value)}
>
  <option value="A">A</option>
  <option value="B">B</option>
  <option value="C">C</option>
</select>
```

---

あなたのコードを書いて貼ってください。


