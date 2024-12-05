### React Notes
https://thenewstack.io/mastering-progressive-hydration-for-enhanced-web-performance/?ref=dailydev

### React
The truly magical thing about React is that we don't have to worry about keeping our state (held in JavaScript) 
and our UI (in the DOM?) in sync.
With React, we're describing what we want the UI to be, based on the current application state.
React takes those descriptions and makes it real.

### What is JSX?
Instead of writing React.createElement, we use an HTML-like syntax to create React elements.

Why do we use JSX? It might not be obvious from this tiny example, but as our chunk of markup grows, it becomes increasingly clear that JSX is just easier to read.

With React 17, the React team introduced a new “JSX transformer”, used by Babel and other compilers. Essentially, it automatically injects the import during the build process.


### 1. Bootstrapping a local React Project

There are various ways to bootstrap a react project locally. Vite is the most widely used one today. 
Vite (French word for "quick", pronounced `/vit/`, like "veet") is a build tool that aims to provide a faster and leaner development experience for modern web projects. It consists of two major parts:

- A dev server that provides [**rich feature enhancements**](https://vite.dev/guide/features) over [**native ES modules**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules), for example extremely fast [**Hot Module Replacement (HMR)**](https://vite.dev/guide/features#hot-module-replacement).
- A build command that bundles your code with [**Rollup**](https://rollupjs.org/), pre-configured to output highly optimized static assets for production.

### HMR issue in WSL2, solution is to modify vite.config.js
```
export default defineConfig({
  plugins: [react()],
  server: {
    watch: {
      usePolling: true
    }
  }
})
```
### Intializing a react project

```
npm create vite@latest
```
### 2. Components

In React, components are the building blocks of the user interface. They allow you to split the UI into independent, reusable pieces that can be thought of as custom, self-contained HTML elements.

![Component](../../images/React_img1.webp)

### 3.useState

`useState` is a Hook that lets you add state to functional components. It returns an array with the current state and a function to update it.
```
import { useState } from "react";
function App() {
  const [count,setCount] = useState(0);
  return (
   <div>
    <button onClick={()=>setCount(count+1)}
    >Pressed {count} times.</button>
   </div>
  )
}
export default App
```

### 4. Tracking re-renders

Install the react dev tools to track which components are re-rendering as your state changes

https://chromewebstore.google.com/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?pli=1