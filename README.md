# React-TypeScript-Vite

React, Vite, and TypeScript offer several advantages when used together such as faster development, better code quality, and improved error handling. React allows developers to build complex UI components, Vite provides an efficient development experience, while TypeScript offers static type checking and better IDE support. The combination of React and TypeScript improves overall developer experience with features like autocompletion and error highlighting, while Vite's integration with TypeScript allows for realtime type checking during development.

```
|—— .gitignore
|—— index.html
|—— README.md
|—— package.json
|—— tsconfig.json
|—— vite.config.json
|—— src
|    |—— App.tsx
|    |—— index.tsx
```

## Bundle JavaScript with Vite

```
❯ yarn init
yarn init v1.22.17
question name (react-ts-vite): react-ts-vite
question version (1.0.0):
question description:
question entry point (index.js):
question repository url:
question author:
question license (MIT):
question private:
success Saved package.json
✨  Done in 22.51s.
```


#### Install Vite

```
  yarn add -D vite
```

#### Create HTML file
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React-TS-Vite</title>
  </head>
  <body>
    <div id="app"></div>
    <script type="module" src="/main.js"></script>
  </body>
</html>
```

#### main.js
```
document.querySelector('#app').innerHTML = `
  <div>
    hello
  </div>
`
```

#### Create Package.json
```
{
  ...
  "scripts": {
    "dev": "vite"
  },
  ...
}
```

With ```yarn dev```, you can see hello like below:

## Build with React
```
yarn add react react-dom
```
#### Install transpiler of React JSX
```
yarn add -D @vitejs/plugin-react
```
#### vite.config.js
```
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
})
```
#### Update main.js

Rename ```main.js``` to ```index.jsx```

```
import React from 'react'
import ReactDOM from 'react-dom/client'
import { App } from './App'

ReactDOM.createRoot(document.getElementById('app')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

#### Add App.jsx
```
export const App = () => (
    <h1>Hello React</h1>
);
```
#### Change index.html a bit
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React-TS-Vite</title>
  </head>
  <body>
    <div id="app"></div>
    <script type="module" src="src/index.jsx"></script>  <!-- CHANGE HERE -->
  </body>
</html>
```
With ```yarn dev```, you can see the resule like below:
[Uploading 0_B9DsdP8-HIMc4ruK.webp…]()

## Add TypeScript

#### Install typescript
```
yarn add -D typescript
```
#### Create tsconfig.json

```
{
  "compilerOptions": {
    "target": "ESNext",
    "useDefineForClassFields": true,
    "lib": ["DOM", "DOM.Iterable", "ESNext"],
    "allowJs": false,
    "skipLibCheck": true,
    "esModuleInterop": false,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "module": "ESNext",
    "moduleResolution": "Node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx"
  },
  "include": ["src"]
}
```

#### Add type declaration of React app
```
yarn add -D @types/react @types/react-dom
```
#### Update jsx files

Let's rename ```main.jsx``` to ```main.tsx``` and ```App.jsx``` to ```App.tsx```

index.tsx
```
import React from 'react';
import { createRoot } from 'react-dom/client';
import { App } from './App';

ReactDOM.createRoot(document.getElementById('app') as HTMLElement).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```
App.tsx
```
import React from "react";

export const App: React.FC = () => (
    <h1>Hello React</h1>
);
```
index.html
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React-TS-Vite</title>
  </head>
  <body>
    <div id="app"></div>
    <script type="module" src="src/main.tsx"></script> <!-- CHANGE HERE -->
  </body>
</html>
```

## Add Type Checking

#### Add type check command in package.json
```
{
  ...,
  "scripts": {    
    "dev": "vite",
    "tscheck": "tsc" // add here
  }
  ...
}
```
If you run ```yarn tscheck```, type error is detected by tsc like below.
```
❯ yarn tscheck
yarn run v1.22.17
$ tsc
✨  Done in 1.26s.
```
If you want to get a type error as soon as possible, you could add -w option. It will watch your code changes and notify type error.
```
❯ yarn tscheck -w
```
## Production Build

```
{
  ...
  "scripts": {
    "dev": "vite",
    "build": "yarn tscheck && vite build",
    "tscheck": "tsc"
  },
}
```

## Legacy Browser
```
Add @vitejs/plugin-legacy
```
