
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


