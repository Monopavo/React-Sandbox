## Project Installation

----- There are multiple ways to include React into a project...


#### Vite

----- Simply type the following in GitBash / CLI while currently based within your preferred parent directory and follow the instructions...

```shell
npm create vite
```

----- And then whilst based within the folder, use the following commands to manipulate your project...

```shell
npm run dev // Opens up a local server with the project loaded (can also use Anthoy Fu's "VS Code for Vite" extension).
npm run build // Builds the project into optimized static files for deployment.
npm run preview // Previews the production build locally.
```

#### The Manual Way 

----- Without using a framework or build tool, you link React and React-DOM to a webpage, designed a <div> as the root access point, and then create and render components through a .js file...

1) Insert the following code in the webpage: 

```html
<script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
<script src="path/to/js/file.js or.ts" type="text/babel"></script>
```

```html
<div id="root"></div>
```

2) Insert the following code in the .js or .ts file:

```javascript
import { createRoot } from 'react-dom/client';

const container = document.getElementById('root');
const root = createRoot(container!);
root.render(<App />);
```

----- This should render the words "Hello, React!", which are encapsulated by a <h1> element; this forms a component. The argument of "root.render()" is the component(s) to be rendered.











## Importing React

----- Since React 17, there's no need to directly import React anymore; instead, at the top of the "App.tsx" or "App.js" file, "useState" and "useEffect" are imported. ReactDOM also doesn't need to be entirely imported, with only "createRoot" needed for the basics of accessing the root of the DOM... 

```JSX
import { useState, useEffect } from "react";
import { createRoot } from 'react-dom/client';
```









## Structure

----- The typical structure of a React project goes like this...

index.html, where main.tsx / main.tsx accesses a single <div id = "root"></div> element.
^
main.tsx / main.jsx, where "App.tsx" / "App.jsx" is imported as the sole module and rendered.
^
App.tsx / App.jsx, where the Components are imported as modules and arranged in a DOM hierarchy.  
^
Components, defined in their individual .tsx / .jsx files and exported as modules.

#### TypeScript Boilerplate

```Typescript
//main.tsx//
import { createRoot } from "react-dom/client";
import App from "./App";

const container = document.getElementById("root");
const root = createRoot(container!);
root.render(<App />);
```

```Typescript
//App.tsx//

import React from "react";
import Component from "path./to/component";

const App: React.FC = () => {
  return (
    <Component value="Hello!" />
  );
};

export default App;
```

```Typescript
//ComponentNameHere.tsx//

interface ComponentProps {
  value: string;
}

const ComponentNameHere : React.FC <ComponentProps>= ({value}) => {
  return <div>{value}</div>;
}

export { ComponentNameHere as Component };
```








## Components

----- React is a library that focuses on responsive UI, and it achieves this through creating modular "components", each with their own defined state and interactivity. "Functional components" are the concise, modern way of creating components, effectively replacing "class components"...

```javascript
/*Arrow function component */
const myComponent = () => <div>This is a component!</div>; 

/* Function literal component */
function MyComponent() {
    return <div>This is a component!</div>;
};

/* Class Component */
class MyComponent extends React.Component {
  render() {
    return <div>This is a component!</div>;
  }
};
```

----- When using TypeScript, the "React.FC" type is used for functional components. It is far more concise than the type for class components, so class components tend to be avoided in modern applications...

```typescript
// Arrow function component
const MyComponent: React.FC <MyComponentProps> = ({propname1}, {propname2, etc...}) => <div>This is a component!</div>;

// Function literal component
function MyComponent(): React.FC {
  return <div>This is a component!</div>;
};

// Class Component
class MyComponent extends React.Component<{}, {}> {
  render() {
    return <div>This is a component!</div>;
  }
};
```

----- Arrow function components are considered the ideal component syntax for modern applications, and therefore a best practice.











#### TypeScript Components - Interfaces

----- When defined, a TypeScript component is typed as just a "React Component"; its values, properties, and methods aren't, so an interface must be used to handle them. In the same script as the component, the following is used...

```JSX
interface MyComponentProps {
  value: string;
}

const MyComponent: React.FC <MyComponentProps> = ({value}) => <div>{value}</div>;
```

----- The "MyComponentProps" interface must be the name defined within the TypeScript component, within the arrow brackets. This specifies that the embedded expression {value} between the <div> must be a string. The value itself is defined in the "App.tsx" file, using the following syntax...

```JSX
const App: React.FC = () => {
  return (
      <Square value="X"/>
  );
};
```










#### Importing and Exporting

----- Creating components in their own files is the standard structure of a React project; it is both a separation of concerns from individual files and between components, making a well-kept React project robust and modular. Rather than link them through HTML, they are imported as modules instead by using the following syntax...

```JSX
import { MyComponent } from "/path/to/file/here";
```

----- ... however, that component must also be explicitly exported in its own file. This is simply a matter of using the following code near the end of the script...

```JSX
export default MyComponent
//OR//
export { MyComponent as Box }; // Assigns 'Box' as an alias.
```









#### Styling

?????




#### GitHub Pages Config


----- Go to vite.config.ts and place "base:" in the "defineConfig()" declaration...

```TypeScript
export default defineConfig({
  base: "/Repository-Name-Here/",
  plugins: [react()],
})
```

----- Add following deployment scripts to package.json...

```JSON
"scripts": {
  "predeploy": "npm run build",
  "deploy": "gh-pages -d dist"
}
```

----- Install GitHub pages (gh-pages) with CLI...

```shell
npm install gh-pages --save-dev
```

----- Build the project with CLI...

```shell
npm run build
```
----- Deploy to GitHub Pages with CLI...

```shell
npm run deploy
```

----- Set "gh-pages" to the source of the website in the repository settings.

----- Whenever making changes to the live website, you have to rebuild and redeploy from the CLI.