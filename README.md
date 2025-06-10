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
### 🔍 UseEffet чист?
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

## UseLayoutEffect
### 🔍 useLayoutEffect чист?
  + **useLayoutEffect** як React Hook аст, ки ба монанди useEffect кор мекунад, аммо он пеш аз он ки браузер экранро навсозӣ кунад (paint), эффектро иҷро мекунад.
#### 🧠 Фарқи асосӣ миёни useEffect ва useLayoutEffect
  + | Хусусият                | `useEffect`                           | `useLayoutEffect`                                |
    | ----------------------- | ------------------------------------- | ------------------------------------------------ |
    | Вақти иҷро              | **пас аз** paint (тасвир)             | **пеш аз** paint (тасвир)                        |
    | Истинод ба DOM          | сусттар, пас аз намоиш                | фавран, пеш аз намоиш                            |
    | Қисми UI дидан мешавад? | Бале (лозим бошад, UI мебинад тағйир) | Не (пеш аз намоиш тағйир медиҳад)                |
    | Қолиб (recommended use) | Аксари ҳолатҳо                        | Вақте ки UI пеш аз намоиш бояд дақиқ тағйир ёбад |

  + ✅ Мисоли оддии useLayoutEffect
     ```javascript
     import { useLayoutEffect, useRef } from 'react';

     function Box() {
     const boxRef = useRef(null);

      useLayoutEffect(() => {
        const box = boxRef.current;
        box.style.width = '200px';
        box.style.backgroundColor = 'green';
      }, []);

      return <div ref={boxRef}>Ман box ҳастам</div>;
    }
     ```
    + 📌 Дар ин ҷо:
       + Мо пеш аз он ки box дар экран намоён шавад, паҳно ва ранги онро тағйир медиҳем.
       + Агар мо useEffect истифода мекардем, аввал box бо ранги аслӣ дидан мешуд, баъд тағйир меёфт → “мереҷидан” (flickering) рух медод.
    + ⛔ Эҳтиёт: useLayoutEffect метавонад UI-ро суст кунад
       + Азбаски он блок мекунад render-ро, агар дар он кори вазнин анҷом диҳӣ (мисли API-запрос), он метавонад UI-ро лангар кунад.
          + ✅ Танҳо дар ҳолатҳои зарурӣ истифода бурдан лозим аст, монанди чен кардани DOM, scroll position, ё муваққатан ғайб кардан/ташаккули UI.
    
#### 🧠 Ҷавоб ба саволи: "useLayoutEffect чист?"
  + **useLayoutEffect** як React Hook аст, ки ба мисли useEffect амал мекунад, вале пеш аз он ки React экранро тасвир кунад (paint). Онро мо истифода мебарем вақте ки UI бояд пеш аз намоиш дақиқ танзим ё тағйир дода шавад, масалан барои чен кардани DOM ё тағйири style.

## UseRef
### 🔍 UseRef чист?
  + **useRef** як React Hook аст, ки барои:
     + Нигоҳ доштани маълумот байни render-ҳо
     + Дастрасӣ ба DOM-элементҳо
     + Нигоҳ доштани ягон reference (нишондиҳанда)
истифода мешавад — бидуни сабаб шудан ба render.
+ 📦 Синтаксис:
+ ```java
  const myRef = useRef(initialValue);
  ```
    + **myRef.current** = арзиши ҳозира
    + Тағйири **myRef.current **ре-рендер намекунад компонентро
+ ✅ 1. Дастрасӣ ба DOM
   + ```java
     const inputRef = useRef(null);

        <input ref={inputRef} />
        <button onClick={() => inputRef.current.focus()}>Focus</button>
     ```
     + 📌 Ин ҷо useRef DOM-и <input>-ро нигоҳ медорад.
+ ✅ 2. Нигоҳ доштани арзише байни render-ҳо
   + ```java
     const countRef = useRef(0);

        function handleClick() {
          countRef.current += 1;
          console.log(countRef.current);
        }
     ```
     + 📌 Мо шумораро нигоҳ медорем, вале компонентро ре-рендер намекунем.
  + ✅ 3. Нигоҳ доштани object, instance, ё таймер
     ```java
     const timerRef = useRef(null);

     useEffect(() => {
      timerRef.current = setInterval(() => {
        console.log('Tick');
      }, 1000);

      return () => clearInterval(timerRef.current);
     }, []);
     ```
       + 📌 Мо таймерро нигоҳ медорем ва баъдтар тоза мекунем.
#### 🧠 Ҷавоби кутоҳ ба "useRef чист?"
  + **useRef** як Hook аст, ки ба мо имкон медиҳад маълумотро байни render-ҳо нигоҳ дорем, ё ба DOM дастрасӣ дошта бошем, бе он ки компонент дубора render шавад. Он одатан барои фокус кардан ба input, чен кардани DOM, ё нигоҳ доштани object истифода мешавад.
