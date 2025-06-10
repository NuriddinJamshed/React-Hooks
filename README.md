# React-Hooks

## UseState
### 🔍 UseSatate чист ва мо онро барои чи истифода мебарем?
+ useState як React Hook аст, ки имкон медиҳад ба компонентҳои функсионалӣ state (ҳолат) илова кунем.
+ useState = имконияти нигоҳ доштан ва тағйир додани маълумот дар компонент.
+ 📦 Синтаксиси асосӣ:
+ ```javascript
    const [state, setState] = useState(initialValue);
  ```
  + state — арзиши ҳозира
  + setState — методе, ки барои тағйири state истифода мешавад
  + initialValue — арзиши ибтидоии state
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
    + count = 0 аввал.
    + Ҳар дафъа ки кнопка клик шавад, setCount(count + 1) иҷро мешавад.
    + React компонентро ре-рендер мекунад ва count-и навро нишон медиҳад.
      
#### 📘 Чаро мо useState истифода мебарем?
  + ✅ Барои нигоҳ доштани маълумоти муваққатӣ:
      + Мисол: рақам, матн, массив, object...
  + ✅ Барои тағйир додани UI:
      + Агар state иваз шавад → React компонентро бозсозӣ мекунад.
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
  + useState як Hook аст, ки ба мо имкон медиҳад маълумотро дар дохили компонент нигоҳ дорем ва онро тағйир диҳем. Ҳар бор ки мо state-ро бо setState иваз мекунем, React UI-ро навсозӣ мекунад. Бо он мо метавонем UI-ро интерактивӣ гардонем, мисли ҳисобкунакҳо, формҳо, матнҳо ва ғ.
  
