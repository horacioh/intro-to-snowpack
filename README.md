# Introduction to Snowpack & React

## 1. Getting Started: Setup the project

- create the base project with the "snowpack minimal template"

```bash
npx create-snowpack-app react-snowpack --template @snowpack/app-template-minimal
# you can add `--use-yarn` or `--use-pnpm` flag to use something other than npm

# when finished
cd react-snowpack
npm run start
```

![welcome to snowpack screen](https://www.snowpack.dev/img/guides/react/minimalist-hello-world.png)

- add React to the base project

```bash
npm install react react-dom --save
```

Snowpack has built in support for JSX. No configs or plugin needed to start using React

- change `index.js` to `index.jsx`

```bash
mv index.js index.jsx
```

- update `index.jsx` to render a simple React component

```javascript
import React from "react"
import ReactDOM from "react-dom"

ReactDOM.render(<div>"HELLO REACT"</div>, document.getElementById("root"))
```

- update `index.html`

```html
<body>
  <!-- <h1>Welcome to Snowpack</h1> -->
  <div id="root"></div>
</body>
```

![hello react](https://www.snowpack.dev/img/guides/react/minimalist-hello-world-react.png)

### References

- [Snowpack \- The faster frontend build tool](https://www.snowpack.dev/)
- [Getting Started with React](https://www.snowpack.dev/tutorials/react)

## 2.Customizeyour project layout

Snowpack is flexible enough to support whatever project layout that you prefer. In this guide, you’ll learn how to use a popular project pattern from the React community.

```bash
mkdir src
mkdir public
mv index.jsx src/index.jsx
mv index.html public/index.html
mv index.css public/index.css
```

If you run the site now, is broken. The `mount` configuration changes where Snowpack looks for and builds files. Every Snowpack project comes with a snowpack.config.js file for any configuration that you might need.

- add this to the `mount` object in `snowpack.config.js`

```javascript
// directory name: 'build directory'
public: "/",
src: "/dist",

```

- because we changed the `mount` config, we need to update the `index.html` file with this

```html
<!-- <script type="module" src="/index.js"></script> -->
<script type="module" src="/dist/index.js"></script>
```

- restart the snowpack server and check if is the same
- create `src/app.jsx` with the same content

```javascript
import React, { useState, useEffect } from "react"

function App() {
  // Create the count state.
  const [count, setCount] = useState(0)
  // Update the count (+1 every second).
  useEffect(() => {
    const timer = setTimeout(() => setCount(count + 1), 1000)
    return () => clearTimeout(timer)
  }, [count, setCount])
  // Return the App component.
  return (
    <div className="App">
      <header className="App-header">
        <p>
          Page has been open for <code>{count}</code> seconds.
        </p>
      </header>
    </div>
  )
}

export default App
```

- update `index.jsx` to use it

```javascript
import App from "./app.jsx"
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById("root")
)
```

## 3. Add Styling

- copy [this svg file](https://github.com/snowpackjs/snowpack/blob/main/create-snowpack-app/app-template-react/src/logo.svg) to the `src` folder
- Update `app.jsx`

```javascript
// import React, { useState, useEffect } from 'react';
import logo from "./logo.svg"

function App() {
// // Create the count state.
// const [count, setCount] = useState(0);
// // Create the counter (+1 every second).
//  useEffect(() => {
//   const timer = setTimeout(() => setCount(count + 1), 1000);
//  return () => clearTimeout(timer);
//   }, [count, setCount]);
//   // Return the App component.
  return (
//  <div className="App">
//    <header className="App-header">
      <img src={logo} className="App-logo" alt="logo" />
//    <p>
//    ...
  )

```

- create `app.css` and add this content:

```css
.App {
  text-align: center;
}

.App p {
  margin: 0.4rem;
}

.App-logo {
  height: 40vmin;
}

@media (prefers-reduced-motion: no-preference) {
  .App-logo {
    animation: App-logo-spin infinite 20s linear;
  }
}

.App-header {
  background-color: #282c34;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: calc(10px + 2vmin);
  color: white;
}

@keyframes App-logo-spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
```

- import the new `app.css` file into your `app.jsx` file

![result css](https://www.snowpack.dev/img/guides/react/react.gif)

## 4. Making Snowpack faster with Fast Refresh

React Fast Refresh? What’s that? It’s a Snowpack enhancement that lets you push individual file changes to update the browser without refreshing the page or clearing component state.

- update `index.jsx`

```javascript
// Hot Module Replacement (HMR) - Remove this snippet to remove HMR.
// Learn more: https://www.snowpack.dev/concepts/hot-module-replacement
if (import.meta.hot) {
  import.meta.hot.accept()
}
```

- update something in the file showing the browser

HMR can save you time on its own, but you may notice in the example above that the counter on the page still resets to 0. This can slow down your development, especially when you’re trying to debug a specific component state problem. Lets enable Fast Refresh to preserve component state across updates.

- install `@snowpack/plugin-react-refresh`

```bash
yarn add @snowpack/plugin-react-refresh --dev
```

- add it to the plugins array in `snowpack.config.js`

```
plugins: ['@snowpack/plugin-react-refresh'],
```

- restart server and apply a change to see that the counter does not resets

## Going Further

- add [Prettier](https://prettier.io/)
- add [Tests](https://www.snowpack.dev/guides/testing) (@web/test-runner is the recommended)
- use Typescript with [this starter](https://github.com/snowpackjs/snowpack/tree/main/create-snowpack-app/app-template-react-typescript)
- checkout all the Official [Snowpack Templates](https://github.com/snowpackjs/snowpack/tree/main/create-snowpack-app)

### Reference

- [Fast Refresh · React Native](https://reactnative.dev/docs/fast-refresh)
- [Snowpack Templates](https://github.com/snowpackjs/snowpack/tree/main/create-snowpack-app)

## Adding Typescript

Snowpack includes built-in support to build TypeScript files (\*.ts) to JavaScript.

if you want to add type-checking, you need to add the plugin `@snowpack/plugin-typescript`

```bash
yarn add @snowpack/plugin-typescript --dev
```

## Adding Preact

You can do it without any custom config needed. update `snowpack.config.js`:

```json
"alias": {
  "react": "preact/compat",
  "react-dom": "preact/compat"
}
```
