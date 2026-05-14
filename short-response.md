# Short Response: Intro to React, Components, and useState

Answer each question below. Write in complete sentences (3–5 per answer).

---

## Question 1 — Components and JSX

What is a React component, and what is JSX? Explain how JSX differs from plain HTML. Use a brief code example to support your answer.

**Your answer:** A react component is a reusable piece of UI with defined logic. JSX is a syntax extension of JavaScript that React uses to return HTML-like syntax. Opposed to HTML, JSX can return React components by calling them with tags. It can run JS code within brackets `{...}`, and uses different attribute names such as `htmlFor` instead of `for`. However, this syntax is for developer convenience and must be compiled down to JavaScript code before the browser can run it.

```html
<main>
  <h1>My Profile!</h1>
  <figure>
    <img src='picture.jpg'>
    <figcaption>My profile picture!!!</figcaption> 
  </figure>
</main>
```

```jsx
const Header = () => {
  return <h1>My profile!</h1>
}

const Figure = () => {
  return (
    <figure>
      <img src='picture.jpg' />
      <figcaption>My profile picture!!!</figcaption> 
    </figure>
  )
}
```

---

## Question 2 — The Build Step and Vite

A browser cannot run a `.jsx` file directly. Why not? Explain the role of a build step and what it means to "compile" code in simple terms.

**Your answer:** The browser cannot run `.jsx` because it only interprets `.js` natively. **Vite** helps us by compiling and bundling the `.jsx` code into JavaScript by running `npm run build` in the terminal. This produces a compact and optimized production `.js` file for the browser to run. Compiling means to translate code written for developer convenience and experience into code that the browser can understand.

---

## Question 3 — useState

What does `useState` return, and what are the two things you get back from it? Describe how to use those values to render data and to update that data.

**Your answer:** `useState` returns a tuple with a variable with the current state value and a setter function that will change the variable's state. `useState` initializes the state variable to a default value and the setter function will update it to a new value by passing it as an argument or using a callback function. When the setter is called to change the state, a re-render will be triggered and React will replace the old value with the new state.

---

## Question 4 — Lifting State Up

What does it mean to "lift state up," and when is it necessary? Use a concrete example.

**Your answer:** "Lifting state up" means defining the state in a common parent/ancestor so other children components can use the same piece of data. This is necessary because sibling components cannot communicate direclty. Therefore, the state is moved up to their closest ancestor, which then passes it down as props. For instance, if an `AddMediaForm` and a `MediaItem` need to reference the same state, then the state should live in their most common ancestor, in this case `App`.

---

## Question 5 — Bug Fix

The component below has a bug. When the user clicks "Add Cherries," the list never updates on screen. Identify what is wrong, write the corrected code, and explain **why** the original code fails in React.

```jsx
const ShoppingList = () => {
  const [items, setItems] = useState(['apples', 'bananas']);

  const addItem = () => {
    items.push('cherries');
    setItems(items);
  };

  return (
    <>
      <ul>
        {items.map((item, i) => <li key={i}>{item}</li>)}
      </ul>
      <button onClick={addItem}>Add Cherries</button>
    </>
  );
};
```

**Your answer:** The original code fails because we are directly pushing the new value `cherries` to the array. Even though, the value changes, React is not triggered to re-render the new information. This happens because React, under the hood, compares if the memory location has changed and not the actual value. We need to create a new reference to that array, including the new value, using the spread operator.

Here's the updated code.

```jsx
const ShoppingList = () => {
  const [items, setItems] = useState(['apples', 'bananas']);

  const addItem = () => {
    setItems([...items, 'cherries']);
  };

  return (
    <>
      <ul>
        {items.map((item, i) => <li key={i}>{item}</li>)}
      </ul>
      <button onClick={addItem}>Add Cherries</button>
    </>
  );
};
```

---
