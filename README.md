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
