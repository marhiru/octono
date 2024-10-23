## Setup a basic ```electron-forge + vite``` project


Initializing project
```
npm init electron-app@latest my-new-app -- --template=vite-typescript
```

### **Before installing packages uninstall eslint on your entire project**

Installing packages
```
pnpm install
```

### Lets start the react setup in our project

Install react % packages
```
pnpm add -D react react-dom @types/react @types/react-dom
```

Also you will need to install scheduler for react-dom work
```
pnpm add -D scheduler
```

If not installed install ```@electron-forge/shared-types```
```
pnpm add -D electron-forge/shared-types
```

## The react is installed now we gonna setup in project

Install the vitejs react dependecie
```
pnpm add -D @vitejs/plugin-react
```

Put the code below on the respective file

```vite.rendered.config.ts```
```typescript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

// https://vitejs.dev/config
export default defineConfig({
    plugins: [react()],
    build: {
        commonjsOptions: {
            include: [/node_modules/],
        },
    },
    optimizeDeps: {
        include: ['react', 'react-dom'],
    },
});
```

Now react will be recognized by the vite renderization

## React is not fully configurated yet

**To complete those minor configurations you will need to**

Create a ```app.tsx``` file inside ```./src``` path.

Create a React root to react render in screen

```app.tsx```
```tsx
import React from 'react'; // Import React
import { createRoot } from 'react-dom/client'; // Import ReactDOM

function App(){
    return (
        <h1>Hello World</h1>
    );
}

const root = createRoot(document.getElementById('root')!); // Ensure these id be the same your HTML file
root.render(
    <React.StrictMode>
        <App />
    </React.StrictMode>
);
```

**In this example im using ```app``` as root ID

Whenever name you put you will need to implement this id in a div inside ```index.html``` body tag

```index.html```
```html

  <!-- <div id="root" /> this id name need to be the same on react root file -->

  <body>
    <!-- PLACE HERE -->>
    <script type="module" src="/src/renderer.ts"></script>
  </body>

```

## Your project is done! try using 

```npm
npm start
``` 
or
```pnpm
pnpm start
```

**After getting done your can do whatever your want or see the nexts steps if you want to use tailwindcss & shadcn-ui**
______________________________________________________________________________________________________________________
## Install and configure tailwindcss & postcss

```npm
pnpm add -D tailwindcss autoprefixer
```
and
```npm
pnpm add postcss
```

## Initialize tailwind on project

```npm
pnpm dlx tailwindcss init
```

**Add ```./src``` **PATH** to the tailwind content**

```tailwind.config.js```
```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './src/**/*.{ts,tsx,html}' // <== New line code
  ],
  theme: {
    extend: {}
  },
  plugins: []
}

```

## Now lets configure postcss on our project 

Create a ```postcss.config.js``` file

Put this respective code inside

```postcss.config.js```
```javascript
import tailwindcss from 'tailwindcss'
import autoprefixer from 'autoprefixer'
export default {
  plugins: [tailwindcss('./tailwind.config.js'), autoprefixer]
}
```

Now postcss setup is finished

## Tailwind last configs to be done

Create a ```globals.css``` file in ```./src/styles``` **PATH**

Inside ```globals.css```file import tailwind structure attributes

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## That's it

After that your tailwindcss will work pretty well


## To use shadcn@ui

**Follow this tutorial**
[Installation shadcn](https://ui.shadcn.com/docs/installation/manual)

Also following this tutorial from the scratch shadcn cant work

you will need to create a ```components.json``` by your self

Default code down below

```components.json```
```json
{
    "$schema": "https://ui.shadcn.com/schema.json",
    "style": "new-york",
    "rsc": false,
    "tsx": true,
    "tailwind": {
        "config": "tailwind.config.js",
        "css": "@/styles/global.css",
        "baseColor": "zinc",
        "cssVariables": true,
        "prefix": ""
    },
    "aliases": {
        "components": "@/components",
        "utils": "@/lib/utils"
    }
}
