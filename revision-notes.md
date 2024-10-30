## Overview

----- React is a library that focuses on responsive, dynamic UIs. ReactDOM is often bundled in with it, however it's a separate library that handles DOM access and manipulation, allowing for React to be integrated into HTML.

----- React is a composable and declarative library; "composable" in that it deals with smaller components that are arranged to produce a larger project, and "declarative" in that it provides a way to describe the UI in terms of its current state. This is completely opposite to JavaScript's imperative style, where you have to explicitly define each step needed to achieve a certain state. 

----- In React, you declare what the UI should look like for a given state, and React handles the rest. It’s about telling React what to achieve, not how to achieve it.





## JSX / TSX

----- JSX or TSX ("JavaScript XML" or "TypeScript XML") is used to write HTML within JavaScript, removing the need to type directly within a .html file. It's a proprietary language of React, and is mainly used within the definition of components and the composition of the DOM hierarchy within the "App.jsx" / "App.tsx" component before it's rendered by "main.jsx" / "main.tsx".


----- As such, there are a couple of differences between standard HTML and JSX / TSX...

* The "class" attribute is now the "className" property.
* The "for" attribute becomes "htmlFor".
* CamelCase is used for two-word attributes, such as "onClick" and "maxLength" instead of "onclick" and "maxlength". 
* Self-closing tags need a closing slash, e.g., <img />.

----- Effectively, JSX / TSX creates a JS / TS object representing a HTML tag, and then transpiles it into an HTML element by rendering it with ReactDOM. For example. a <h1> tag with "Hello, World!" in JSX / TSX is created with the following properties...

```Typescript

* type: "h1" // The type of tag, which is a <h1> in this case.

* key: null, // Used to uniquely identify elements in a list, akin to the "id" element. Often set to null when not used.

* ref: null, // Used to reference the DOM element or component instance for direct manipulation.

* props: // "props" contains the properties / attributes of the object...
{className: null, // ... with "className" representing classes...
children: "Hello, World!" // ... and "children" representing any encapsulated content. 
}, 

* _owner: null, // An internal property used by React to keep track of the component's owner.

* _store: {} // An internal property used by React for state management and internal bookkeeping.
```









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



----- With React, there are also a couple of special props that can be used to produce interesting interactions while remaining type safe...

```Typescript
interface ComponentProps {

  children: React.ReactNode; // Used to allow a component to encapsulate with opening and closing tags. "React.ReactNode" is used to encapsulate other nodes, but it can also be used with other types like "string" to remove the need for direct assignment to a {value} attribute.

  key: string | number; // Used to identify which items have changed, are added, or are removed. It's essential for rendering lists efficiently, as  without a key React struggles to determine what has changed. Consider it akin to an "id" tag for <li> elements.

  ref: React.Ref<any>;  // Provides a way to access the DOM nodes or React elements created in the render method. Useful for managing focus, text selection, or triggering animations. The "<any>" suffix specifies that it works with any component or value.

}

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












#### State Management

----- "useState" must be imported with React...

import React, { useState } from "react";

----- ... and then the state is defined within a component's definition. For example, for a basic counter...

```Typescript
const ExampleComponent: React.FC = () => {
  const [state, setState] = useState<number>(0);

  return (
    <div>
      <p>State: {state}</p>
      <button onClick={() => setState(state + 1)}>Increment</button>
    </div>
  );
};
```

//OR//

```Javascript
const ExampleComponent = () => {
    const [state, setState] = useState(0);

    return (
        <div>
            <p>State: {state}</p>
            <button onClick={() => setState(state + 1)}>Increment</button>
        </div>
    );
};
```

----- States that are updated through event handlers, such as with the "onClick" attribute, use this simple blueprint, however if multiple states need to be updated by a single event handler then it's a best practice to create a new method with the "handle" prefix and assign it to "onClick" within the component's structure...

```Javascript
const ExampleComponent = () => {
    const [counter, setCounter] = useState(0);
    const [tally, setTally] = useState(0);

    const handleClick = () => {
        setCounter(counter + 1);
	setTally(tally + "|");
    };

    return (
        <div>
            <p>Current Counter: {counter}</p>
	    <p>Current Tally: {tally}</p>
            <button onClick={handleClick}>Click This Button!</button>
        </div>
    );
};
```




---- Basically, a state has this basic blueprint...

const [SETTER, UPDATER] = useState(VALUEOFSETTER);

---- ... and there can be multiple states in the same component that manage different interactions...

```Javascript
  const [greeting, setGreeting] = useState("Hello!");
  const [counter, setCounter] = useState(0);
  const [trueOrFalse, setTrueOrFalse] = useState(true);
```

----- With TypeScript, states don't need their own interface; they can simply be typed within their definition by using arrow brackets, setting their types implicitly. They can even handle multiple types, such as <string | number>, or predefined union types...

```Typescript
  const [greeting, setGreeting] = useState<string>("Hello!");
  const [counter, setCounter] = useState<number>(0);
  const [trueOrFalse, setTrueOrFalse] = useState<boolean>(true);
```







## Inherited State

----- To reiterate, states are placed in isolated components, or otherwise parent components such as an "Inventory" component that holds multiple "InventorySlot" components, or a "Menu" component that holds "NewGame", "LoadGame", and "Quit" components.

----- Using parent containers allows for state to be defined solely in the parent, and then passed down to its children. This greatly simplifies state for simple interactions, such as clicking to access a component. Two key steps need to happen in order to pass states to a child component:

* In the parent component, the states must be set as attributes of the child components within the "return()" encapsulation.
* The child component must have the "state" and "setState" names of each state within their props.

---- For TypeScript, those inherited states must also be appropriately typed within the child component; typically within an interface. These are the required types:

* stateNameHere: typeshere; // string, Boolean, etc...
* setStateNameHere: React.Dispatch<React.SetStateAction<sametypeasstatehere>>;

## useEffect

----- "useEffect" is also commonly paired with "useState", and is imported in the same way...

import React, { useState, useEffect } from "react";

----- Anything that's encapsulated by "useEffect(), {}" is trigged once upon the component being loaded, meaning that it's best used for one-and-done state activation and events. For dynamic states, such as updating a counter, they should be defined outside of the "useEffect(), {}" expression. 

----- Essentially, "useEffect" is used to trigger any functions or methods upon the component being loaded; consider "useEffect" a single initialisation, and "useState" the continuous updates.











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