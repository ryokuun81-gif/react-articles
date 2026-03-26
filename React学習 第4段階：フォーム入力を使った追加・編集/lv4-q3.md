
---

# Q3

## テーマ

**追加時に active をチェックボックスで決める**

## 初期データ

```jsx
const initialUsers = [
  { id: 1, name: "Taro", age: 23, active: true },
  { id: 2, name: "Hanako", age: 45, active: false },
];
```

## 基本形

```jsx
import { useState } from "react";

export default function App() {
  const [users, setUsers] = useState(initialUsers);
  const [inputName, setInputName] = useState("");
  const [inputAge, setInputAge] = useState("");
  const [isActive, setIsActive] = useState(false);

  return (
    <>
    </>
  );
}
```

## 問題

次の動きを作ってください。

* 名前入力欄
* 年齢入力欄
* active 用のチェックボックス
* 「追加」ボタン

を用意して、追加時に

```jsx
{ id, name, age, active }
```

の形で `users` に追加してください。

---

## 条件

* 名前が空なら追加しない
* 年齢が空なら追加しない
* `age` は数値で保存する
* チェックが入っていたら `active: true`
* 入っていなければ `active: false`
* 追加後は

  * 名前を空に戻す
  * 年齢を空に戻す
  * チェックを `false` に戻す

---

## 一覧表示

一覧はこういう形で表示してください。

```jsx
<li key={user.id}>
  {user.name} - {user.age} - {user.active ? "active" : "inactive"}
</li>
```

---

## 出力イメージ

初期表示

```jsx
Taro - 23 - active
Hanako - 45 - inactive
```

たとえば

* 名前: Jiro
* 年齢: 30
* チェックあり

で追加したら

```jsx
Jiro - 30 - active
```

が追加されればOKです。

---

## ヒント

チェックボックスはこんな形です。

```jsx
<input
  type="checkbox"
  checked={isActive}
  onChange={(e) => setIsActive(e.target.checked)}
/>
```

---

あなたのコードを書いて貼ってください。


```javascript
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

  const addUser = () => {
    const ageNumber = Number(inputAge);

    if (!inputName.trim() || !inputAge.trim() || ageNumber <= 0) return;

    setUsers((prev) => {
      const newId =
        prev.length > 0 ? Math.max(...prev.map((u) => u.id)) + 1 : 1;

      const newUser = {
        id: newId,
        name: inputName.trim(),
        age: ageNumber,
        active: isActive,
      };

      return [...prev, newUser];
    });

    setInputName("");
    setInputAge("");
    setIsActive(false);
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

      <label>
        <input
          type="checkbox"
          checked={isActive}
          onChange={(e) => setIsActive(e.target.checked)}
        />
        active
      </label>

      <button onClick={addUser}>追加</button>

      <ul>
        {users.map((u) => (
          <li key={u.id}>
            {u.name} - {u.age} - {u.active ? "active" : "inactive"}
          </li>
        ))}
      </ul>
    </>
  );
}
```