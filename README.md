# React-Hooks

## UseState
### 🔍 UseSatate чист ва мо онро барои чи истифода мебарем?
+ useState як React Hook аст, ки имкон медиҳад ба компонентҳои функсионалӣ state (ҳолат) илова кунем.
+ useState = имконияти нигоҳ доштан ва тағйир додани маълумот дар компонент.
+ 📦 Синтаксиси асосӣ:
+ ```javascript
    const [state, setState] = useState(initialValue);
  ```
  + **state** — арзиши ҳозира
  + **setState** — методе, ки барои тағйири state истифода мешавад
  + **initialValue** — арзиши ибтидоии state
+ ✅ Мисоли сода (Хиссобкунак):
+ ```javascript
  import { useState } from 'react';
  function Counter() {
  const [count, setCount] = useState(0);

  const increment = () => setCount(count + 1);

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </>
  );
  }
  ```
  +🔁 Чӣ рӯй медиҳад дар боло:
    + **count** = 0 аввал.
    + Ҳар дафъа ки кнопка клик шавад, setCount(count + 1) иҷро мешавад.
    + React компонентро ре-рендер мекунад ва count-и навро нишон медиҳад.
      
#### 📘 Чаро мо useState истифода мебарем?
  + ✅ Барои нигоҳ доштани маълумоти муваққатӣ:
      + Мисол: рақам, матн, массив, object...
  + ✅ Барои тағйир додани UI:
      + Агар **state** иваз шавад → **React** компонентро бозсозӣ мекунад.
  + ✅ Барои интерактивӣ кардани компонент:
      + Монанди: ҳисобкунак (counter), валидация, фаҳмондани input, диалог, табҳо ва ғ.
  + 🔤 Мисол бо матн:
  + ```javascript
    function NameChanger() {
    const [name, setName] = useState("Нуриддин");

    return (
    <>
      <p>Салом, {name}!</p>
      <button onClick={() => setName("Алишер")}>Тағйир диҳ</button>
    </>
    );
    }
    ```
    + ⚠️ Ҳар бор ки setState (яъне setCount, setName ва ғ.) фаро хонда мешавад:
        + ✅ Компонент аз нав render мешавад
        + ❌ Аммо худи компонентро дастӣ навсозӣ кардан лозим нест — React онро худаш мекунад.
### 🧠 Чӣ бояд бигӯӣ, агар пурсанд "useState чист?"
  + **useState** як **Hook** аст, ки ба мо имкон медиҳад маълумотро дар дохили компонент нигоҳ дорем ва онро тағйир диҳем. Ҳар бор ки мо state-ро бо setState иваз мекунем, React UI-ро навсозӣ мекунад. Бо он мо метавонем UI-ро интерактивӣ гардонем, мисли ҳисобкунакҳо, формҳо, матнҳо ва ғ.
  
## UseEffect
### UseEffet чист?
  + **useEffect** як React Hook аст, ки барои иҷрои амалҳои тарафӣ (side effects) истифода мешавад.
#### 📘 Амалҳои тарафӣ яъне чӣ?
Side effects — ин корҳоест, ки берун аз render мешаванд:
    + Иҷрои запрос ба сервер (fetch, axios)
    + Тағйир додани DOM
    + Гирифтани маълумот аз localStorage
    + Танзим кардани таймер (setTimeout, setInterval)
    + Сабт дар console, ё обуна шудан ба event-ҳо
  + 📦 Синтаксиси асосӣ:
     + ```javascript
       useEffect(() => {
          // Коде, ки бояд пас аз render иҷро шавад
        }, [dependencies]);
       ```
         + dependencies — массиви вобастагӣ:
            + Агар холӣ бошад [], эффект танҳо як маротиба иҷро мешавад (мисли componentDidMount)
            + Агар дар дохилаш арзиш бошад, эффект ҳар бор ки он арзиш иваз шавад, кор мекунад
  + ✅ Мисоли сода: Як бор иҷро шавад
     + ```javascript
       import { useEffect } from 'react';

        function Hello() {
          useEffect(() => {
            console.log('Компонент бор карда шуд!');
          }, []);

          return <p>Салом!</p>;
        }
        ```
       + 📌 Ин эффект танҳо як бор, пас аз аввалин render иҷро мешавад.
      
  + ✅ Мисол: Назорат кардани тағйирот
     + ```javascript
       import { useState, useEffect } from 'react';

        function Counter() {
          const [count, setCount] = useState(0);

          useEffect(() => {
            console.log('Count тағйир ёфт:', count);
          }, [count]);

          return (
            <>
              <p>Count: {count}</p>
              <button onClick={() => setCount(count + 1)}>+1</button>
            </>
          );
        }
       ```
    + 📌 Ҳар бор ки count тағйир ёбад, эффект кор мекунад.
   
  + ✅ Мисол: гирифтани маълумот аз сервер
     + ```javascript
       import { useEffect, useState } from 'react';

        function UsersList() {
          const [users, setUsers] = useState([]);

          useEffect(() => {
            fetch('https://jsonplaceholder.typicode.com/users')
              .then(res => res.json())
              .then(data => setUsers(data));
          }, []); // як бор пас аз render

          return (
            <ul>
              {users.map(user => <li key={user.id}>{user.name}</li>)}
            </ul>
          );
        }
       ```

  + 🧹 Тозакунии эффект (clean-up):
     ```java
     useEffect(() => {
       const timer = setInterval(() => {
         console.log('Tick');
      }, 1000);

      return () => {
        clearInterval(timer); // тоза кардан
      };
     },[]);
     ```
#### 🧠 Ҷавоби кутоҳ ба саволи "useEffect чист?"
+ **useEffect** Hook аст, ки имкон медиҳад мо баъд аз он ки компонент ба экран намоён шуд, амалҳои тарафӣ иҷро кунем — монанди запрос ба сервер, тағйири DOM, насб ё тоза кардани таймерҳо ва ғайра. Он ба React мегӯяд: "Пас аз render ин корро анҷом бидеҳ".
