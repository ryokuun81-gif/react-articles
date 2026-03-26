
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
