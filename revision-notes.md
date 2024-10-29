## Overview

----- React is a library that focuses on responsive, dynamic UIs. ReactDOM is often bundled in with it, however it's a separate library that handles DOM access and manipulation, allowing for React to be integrated into HTML.

----- React is a composable and declarative library; "composable" in that it deals with smaller components that are arranged to produce a larger project, and "declarative in that it ...




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
root.render(
    <React.StrictMode>
	<App />)
    </React.StrictMode>;
```

----- This should render the words "Hello, React!", which are encapsulated by a <h1> element; this forms a component. The argument of "root.render()" is the component(s) to be rendered.











## Importing React

----- Since React 17, there's no need to directly import React anymore; instead, at the top of the "App.tsx" or "App.js" file, "useState" and "useEffect" are imported. ReactDOM also doesn't need to be entirely imported, with only "createRoot" needed for the basics of accessing the root of the DOM... 

```JSX
import { useState, useEffect } from "react";
import { createRoot } from 'react-dom/client';
```

----- However, in order to use "<React.StrictMode>", the entirety of React must be imported...

```JSX
import React from "react";
import { createRoot } from 'react-dom/client';
```










## Structure

----- The typical structure of a React project goes like this...

#1) index.html /// main.tsx accesses a single <div id = "root"></div> element.

#2) main.tsx /// "App.tsx", "React", and "createRoot" are imported. The App is rendered here.

#3) App.tsx /// Components are imported as modules and composed in a DOM hierarchy similar to HTML.  

#4) Components /// Defined within their own files, and their own ".module.css" files are imported for styling. Components are exported as modules.

#5) CSS Modules /// Defined within their own ".module.css" files and exported to their paired, unique components.






#### TypeScript Boilerplate

```Typescript
//main.tsx//
import React from "react";
import { createRoot } from 'react-dom/client';
import App from './App';

const container = document.getElementById('root');
const root = createRoot(container!);

root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

```Typescript
//App.tsx//

import React from "react";
import Component from "path./to/component";

const App: React.FC = () => {
  return (
    <React.StrictMode>
        <Component value="Hello!" />
    </React.StrictMode>
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

#### React.StrictMode ####

----- "React.StrictMode" is a built-in component designed to help write better React code. By wrapping parts of the application in <StrictMode> and </React.StrictMode>, React will run additional checks and provide warnings about potential problems in the code. This includes...

// Components with unsafe lifecycle methods.
// Deprecated APIs.
// Unexpected side effects.
// Sections that need updating.

----- <React.StrictMode> is a very powerful component and tool that has no performance concerns on the finished build, encapsulating the traditional <div> for the composition of the App and its rendering.

----- <React.StrictMode> can also be used in the definition of a component; combined with TypeScript. This ensures absolute safety at the cost of increased complexity, so it isn't recommended except in the largest projects...

const Box: React.FC<BoxProps> = ({ value }) => {
    return(
        <React.StrictMode>
            <div>This is my box component!</div>
        </React.StrictMode>
    );
};

----- As such, it's always recommended to use <React.StrictMode> in the "App" and "main" files. Note that <React.StricMode> requires React to be imported in its entirety within both "App" and "main"...

```JSX
import React from "react";
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
const MyComponent: React.FC <MyComponentProps> = ({propname1}, {propname2, etc...}) =><div>This is a component!</div>;

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
      <React.StrictMode>
          <Square value="X"/>
      </React.StrictMode>
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

----- Outside of libraries such as Tailwind, React components are typically styled with a core "style.css" script for unified styles and multiple "CSS modules".
 
----- Using CSS modules is considered a best practice as the scope of the style is entirely centered around an individual component, which helps separate the concerns between components and the DOM as well as allow for easy adjustments without worrying too much about style specificity. 

----- CSS Modules are defined with ".module.css" instead of ".css", and are exported. They are typically named after their component type with "Style" at the end, and use camelCase. For example...


```CSS
// filename is "paragraphStyles.module.css" //

.color {
    color: whitesmoke;
    background-color: grey;
}

.size {
    height: 50vh;
    width: 75vh;
}
```

----- Note that an export statement isn't needed for CSS Modules; it's emplicitly exported due to its nature as a ".module.css". The module is then imported into a component, with its style(s) being defined as attributes within the React elements. If using multiple class styles within the same module, a template literal is used with space separators between each style...  


```TypeScript
import paragraphStyles from "path/to/the/style.module.css";

interface ParagraphProp {
    value: string;
};

const Paragraph: React.FC<ParagraphProp> = ({value}) => {
    return <p className={`${paragraphStyles.color} ${paragraphStyles.size}`}>{value}</p>;
};   

export default Paragraph;
```

----- ... and then when it is composed in the App, the "className" attribute isn't needed as it has already been defined at the same time as the component, making it an innate style of the component...

```Typescript
const App: React.FC = () => {
  return (
      <React.StrictMode>
          <Paragraph value="This is my first paragraph... />
          <Paragraph value="This is my second... />
          <Paragraph value="And my third! />
      </React.StrictMode>
  );
};

export default App;
```

----- And it is finally rendered in the "main.tsx" file...

```Typescript
root.render(
    <React.StrictMode>
        <App />
    </React.StrictMode);
```







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