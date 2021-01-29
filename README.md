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
