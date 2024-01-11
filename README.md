# react
Learning React from [official docs](https://react.dev/learn) and various other sources.

## Helpful links
1. [JavaScript Info](https://javascript.info/)(Excellent)
2. [10 React Hooks Explained](https://youtu.be/TNhaISOUy6Q?si=uGvmrS5tMAKaxS8e)
3. [React Router in 45 minutes](https://youtu.be/Ul3y1LXxzdU?si=MPRoMioZ2wWVb7jH)

## Quickstart
https://react.dev/learn

### default export
[Read this](https://javascript.info/import-export) as this is an important concept.

### React project structure
[Reference](https://codesandbox.io/p/sandbox/react-dev-zjtyvn?file=%2Fpublic%2Findex.html%3A8%2C7)

A simple react app looks like this
```bash
some-project
├── public
│   └── index.html
├── src
│   ├── App.js
│   ├── index.js
│   └── styles.css
├── package.json
├── README.md
└── .gitignore
```

The files and the output look like this
<table>
<thead>
  <tr>
    <th><code>index.html</code></th>
    <th><code>index.js</code></th>
  </tr>
</thead>
<tbody>
  <tr>
  <td valign="top">
  
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  <body>
    <!-- It serves as a container for your React app -->
    <div id="root"></div>
  </body>
  </html>
  ```

  <p>This is what gets sent to the browser along with <code>index.js</code>. It serves as the entry point of your app.</p>
  <p>Even though there is no direct reference to <code>index.js</code> in this file, it will be bundled and loaded by some JS bundler (like webpack) when this app is built for production.</p>
  </td>
  <td valign="top">
  
  ```js
  import React, { StrictMode } from "react";
  import { createRoot } from "react-dom/client";
  import "./styles.css";
  
  import App from "./App";

  // This creates a root node in the React DOM.
  const root = createRoot(document.getElementById("root"));
  // When .render is called, App component is rendered into this root node of the React DOM.
  // The React DOM is reconciled with the actual DOM by the React library,
  // effectively "mounting" the App component to the real DOM.
  root.render(
    <StrictMode>
      <App />
    </StrictMode>
  );
  ```

  <p>Read the comments in this code above.</p>
  </td>
  </tr>
</tbody>
</table>

<table>
<thead>
  <tr>
    <th><code>App.js</code></th>
    <th><code>package.json</code></th>
    <th><code>styles.css</code></th>
  </tr>
</thead>
<tbody>
  <tr>
  <td valign="top">
  
  ```js
  const user = {
    name: 'Hedy Lamarr',
    imageUrl: 'https://i.imgur.com/yXOvdOSs.jpg',
    imageSize: 90,
  };
  
  export default function Profile() {
    return (
      <>
        <h1>{user.name}</h1>
        <img
          className="avatar"
          src={user.imageUrl}
          alt={'Photo of ' + user.name}
          style={{
            width: user.imageSize,
            height: user.imageSize
          }}
        />
      </>
    );
  }
  ```

  <p><i>Single curly brackets</i> <code>{}</code> are used to insert JavaScript expressions within the JSX.</p>
  <p><i>Double curly brackets</i> <code>{{}}</code> are typically used for inline styling in JSX, the outer curly brackets <code>{}</code> are a placeholder for a JavaScript expression, the inner curly brackets <code>{}</code> represent a JavaScript object. So, <code>style={{width: user.imageSize, height: user.imageSize}}</code> is passing an object to the style attribute.</p>

  <hr>

  The output looks like this

  <img width="150" alt="image" src="https://github.com/akhanalcs/react/assets/30603497/30c467fe-f21e-47d1-b258-2b1449793047">

  </td>
  <td valign="top">

  ```json
  {
    "name": "react.dev",
    "version": "0.0.0",
    "main": "/src/index.js",
    "scripts": {
      "start": "react-scripts start",
      "build": "react-scripts build",
      "test": "react-scripts test --env=jsdom",
      "eject": "react-scripts eject"
    },
    "dependencies": {
      "react": "^18.0.0",
      "react-dom": "^18.0.0",
      "react-scripts": "^5.0.0"
    },
    "devDependencies": {}
  }
  ```

  </td>
  <td valign="top">

  ```css
  * {
    box-sizing: border-box;
  }
  
  body {
    font-family: sans-serif;
    margin: 20px;
    padding: 0;
  }
  
  h1 {
    margin-top: 0;
    font-size: 22px;
  }
  
  h2 {
    margin-top: 0;
    font-size: 20px;
  }
  
  h3 {
    margin-top: 0;
    font-size: 18px;
  }
  
  h4 {
    margin-top: 0;
    font-size: 16px;
  }
  
  h5 {
    margin-top: 0;
    font-size: 14px;
  }
  
  h6 {
    margin-top: 0;
    font-size: 12px;
  }
  
  code {
    font-size: 1.2em;
  }
  
  ul {
    padding-inline-start: 20px;
  }
  
  .avatar {
    border-radius: 50%;
  }
  
  .large {
    border: 4px solid gold;
  }
  ```

  </td>
  </tr>
</tbody>
</table>

### Using Hooks
[Reference](https://react.dev/learn#using-hooks)

Functions starting with use are called Hooks. `useState` is a built-in Hook provided by React.  
Hooks are more restrictive than other functions. You can only call Hooks at the top of your components (or other Hooks). If you want to use `useState` in a condition or a loop, extract a new component and put it there.

For eg:
```js
function MyComponent(props) {
  if (props.condition) {
    const [value, setValue] = useState(0); // ❌ Invalid Hook call
  }
  // ...
}
```
The proper way:
```js
function MyComponent(props) {
  if (props.condition) {
    return <MySubComponent />;
  }
  // ...
}

function MySubComponent() {
  const [value, setValue] = useState(0); // ✅ Valid Hook call
  // ...
}
```

### Sharing data between components
[Reference](https://react.dev/learn#sharing-data-between-components)

Read the comments below to see how the code works.

```js
import { useState } from "react";

export default function MyApp() {
  console.log("MyApp rendered.");
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <div>
      <h1>Counters that update together</h1>
      <MyButton count={count} onClick={handleClick} />
      <MyButton count={count} onClick={handleClick} />
    </div>
  );
}

// {} in '{ count, onClick }' is because we're destructuring/ unpacking "props" object passed to it into distinct variables
// In JS, primitive values (like numbers, strings, booleans) are passed by value while objects
// (including arrays and functions) are passed by reference.
// Here 'count' is passed by value but 'onClick' is passed by reference.
// When this button is clicked, handleClick function in MyApp component is called which updates 'count' state
// in MyApp component. Since 'count' is part of MyApp component's state, changing it will trigger re-render of
// MyApp as well as child components that depend on that state (MyButton in this case).
function MyButton({ count, onClick }) {
  console.log("MyButton rendered.");
  return <button onClick={onClick}>Clicked {count} times</button>;
}
```

## Tic-tac-toe tutorial
[Reference](https://react.dev/learn/tutorial-tic-tac-toe#setup-for-the-tutorial)
### Setup local development
- Download the code from the link referenced above
- Clone this repo down to your local, and paste the code downloaded from previous step into it
- Navigate into this folder
  ```bash
  cd ./tic-tac-toe/
  ```
- Install dependencies
  ```bash
  npm install
  ```
- Add `node_modules` folder to .gitignore.  
  Right click `node_modules` folder -> Git -> Add to `.gitignore` -> `.gitignore`
- Add `package-lock.json` file to source control.  
  Right click `package-lock.json` file -> Git -> Add
- Start local server
  ```bash
  npm start
  ```
  The script that gets called is this
  https://github.com/akhanalcs/react/blob/f1943884e245f862ed69c4c22cbfa5d426321860/tic-tac-toe/package.json#L6

