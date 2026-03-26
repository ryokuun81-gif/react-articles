では始めます。
**React学習 第6段階：集計・グルーピング・一覧表示をReactに持ち込む**
10問形式で、1問ずつ進めます。

今回は **Q1** です。

---

# Q1

## テーマ

**group ごとに人数を集計して表示する**

## 初期データ

```jsx
const initialUsers = [
  { id: 1, name: "Taro", active: true, group: "A", score: 80 },
  { id: 2, name: "Hanako", active: false, group: "B", score: 90 },
  { id: 3, name: "Jiro", active: true, group: "A", score: 70 },
  { id: 4, name: "Saburo", active: true, group: "C", score: 60 },
  { id: 5, name: "Goro", active: false, group: "B", score: 100 },
];
```

## 基本state

```jsx
const [users, setUsers] = useState(initialUsers);
```

## 問題

`users` を使って、**group ごとの人数** を集計してください。
そのあと JSX で一覧表示してください。

## 期待する表示例

```jsx
A: 2人
B: 2人
C: 1人
```

---

## 条件

* `reduce` を使って集計する
* 集計結果はオブジェクトでOK
* その集計結果を `Object.entries(...)` などで JSX に表示してOK

---

## ヒント

まずはこんな形の集計結果を目指します。

```jsx
{
  A: 2,
  B: 2,
  C: 1
}
```

そのあと表示では、たとえば `Object.entries(groupCounts)` を使うと扱いやすいです。

---

## 学びたいポイント

この問題では次の流れを練習します。

* 配列を `reduce` で集計する
* 集計結果をオブジェクトにする
* そのオブジェクトを JSX で一覧表示する

---

あなたの回答を貼ってください。
書けたら添削して、次は **Q2: active / inactive ごとに人数集計** に進みます。


```javascript

import { useState } from "react";
const initialUsers = [
  { id: 1, name: "Taro", active: true, group: "A", score: 80 },
  { id: 2, name: "Hanako", active: false, group: "B", score: 90 },
  { id: 3, name: "Jiro", active: true, group: "A", score: 70 },
  { id: 4, name: "Saburo", active: true, group: "C", score: 60 },
  { id: 5, name: "Goro", active: false, group: "B", score: 100 },
];

export default function App() {
  const [users, setUsers] = useState(initialUsers);

  const groupCounts = users.reduce((acc, cur)=>{
    const key = cur.group;
    acc[key] = (acc[key] || 0) + 1;
    return acc;
  }, {})

  return(
    <>
      <ul>
          {Object.entries(groupCounts).map(([group, count])=>
            <li key={group}>{group}-{count}人</li>
          )}
      </ul>    
    
    </>
  );
}
```

