#### Q1:Create a "Hello World" using vanilla Js ? 

**Answer**:

index.js

```js
// 1. Import dependencies
import React from 'react';
import { createRoot } from 'react-dom/client';

// 2. Create a React element
const element = React.createElement(
  'p',
  { id: 'hello' },
  'Hello World!'
);

// 3. Render the application
const container = document.querySelector('#root');
const root = createRoot(container);
root.render(element);
```

Index.html

```html
<html>
<body>

  <div id="root"></div>

</body>
</html>
```

#### Q2:Below we are writing the code to show "Hello World" on the browser 

```js
// 1. Import dependencies
import React from 'react';
import { createRoot } from 'react-dom/client';

// 2. Create a React element
const element = React.createElement(
  'p',
  { id: 'hello' },
  'Hello World!'
);

// 3. Render the application
const container = document.querySelector('#root');
const root = createRoot(container);
root.render(element);
```

```html
<html>
<body>

  <div id="root"></div>

</body>
</html>
```

Why there are seperate 2 packages ? 

**Answer**:

This is because React itself is “platform agnostic”. We have the core `react` package, and then there are different platform-specific *renderers*:

`react-dom` for the web

`react-native` for mobile (iOS / Android) or desktop (Windows / macOS) applications

`react-three-fiber` for 3D scenes using WebGL and Three.js

Every platform has its own “primitives”, the set of built-in elements we use  to create our UI. On the web, the primitives are HTML elements like `<div>` and `<p>` and `<button>`. By contrast, React Native doesn't have divs, it has `Text` and `View` and `Pressable`. And things get even more wild with react-three-fiber, where the  primitives are things like lights, geometries, materials, and cameras.

All of these platforms will use the same core React framework, which comes from the `react` package. But when it comes to actually turning all of the business  logic into a user interface, we need the correct bindings for our  platform.

#### Q3:What is the difference between DOM and HTML ? 

**Answer**:

To use an analogy: HTML is the blueprint for a specific car, and the DOM is the car itself, zipping around the city.

#### Q4:Fill in the blanks 

When we use a tool like React, it works by interacting with the DOM via  ___________. It'll create, update, and delete DOM elements as required.

**Answer**:

When we use a tool like React, it works by interacting with the DOM via  JavaScript. It'll create, update, and delete DOM elements as required.

#### Q5:Syntax of `React.createElement()` 

**Answer**:

`React.createElement` is a function that accepts 3 or more arguments:

1. The type of the element to create.
2. The properties we want this element to have.
3. The element's contents. We can omit this if the element should be empty.

```js
const element = React.createElement(
  'p',
  { id: 'hello' },
  'Hello World!'
);
```

#### Q6:What does the following code return ? 

```js
const element = React.createElement(
  'p',
  { id: 'hello' },
  'Hello World!'
);
```

This function returns a “React element”. React elements are plain old JavaScript objects. If we inspect it with `console.log(element)`, we'll see something like this:

```js
{
  type: "p",
  key: null,
  ref: null,
  props: {
    id: 'hello',
    children: 'Hello World!',
  },
  _owner: null,
  _store: { validated: false }
}
```

#### Q7:The following code paints to the DOM "Hello World"

Index.js

```js
// 1. Import dependencies
import React from 'react';
import { createRoot } from 'react-dom/client';

// 2. Create a React element
const element = React.createElement(
  'p',
  { id: 'hello' },
  'Hello World!'
);

// 3. Render the application
const container = document.querySelector('#root');
const root = createRoot(container);
root.render(element);
```

Index.html

```html
<html>
<body>

  <div id="root"></div>

</body>
</html>
```

Explain the following lines of code ? 

 

```js
const container = document.querySelector('#root');
const root = createRoot(container);
root.render(element);
```

**Solution**:

`document.querySelector` is a helpful function that lets us capture a reference to a pre-existing DOM element. 

It works in this case because our `index.html` file includes the following element:

```html
<div id="root"></div>
```

**This element will be our application's container.** When we render our React application, it will create and append new DOM element(s) to this container.

With `react-dom`'s `createRoot` function, we specify that this element should be the root of our application. And, finally, we render the application with `root.render(element)`.

You can think of the `render` function as a machine that converts React elements into DOM nodes. In  this case, our React element describes a paragraph tag, with an ID, and  some text inside. `render` will turn that description into the following DOM structure:

```html
<p id="hello">
  Hello World!
</p>
```

With that DOM element created, it then adds it to the page at the  specified root. In essence, this code takes a JavaScript-based  description of some HTML, and uses it to produce real-world DOM nodes.

#### Q8:The following code paints "Hello World" to the DOM 

Index.js

```js
// 1. Import dependencies
import React from 'react';
import { createRoot } from 'react-dom/client';

// 2. Create a React element
const element = React.createElement(
  'p',
  { id: 'hello' },
  'Hello World!'
);

// 3. Render the application
const container = document.querySelector('#root');
const root = createRoot(container);
root.render(element);
```

Index.html

```html
<html>
<body>

  <div id="root"></div>

</body>
</html>
```

Why there is no script tag in the HTML file ? 

**Answer**:

The thing to know about React is that it's used within a *build system*. The files we work with are inputs to this system.

The `index.js` file, along with the dependencies (React, React DOM), are bundled into cryptically-named files like `2.61b71a6f1.chunk.js`, and a `<script>` tag is dynamically injected into the HTML.

 There's an *active process* that transforms the files we write.

If you haven't used other JS frameworks, this probably seems wildly  overengineered to you. Why can't we add our code ourselves, using `<script>` tags, the way we do when working with jQuery and other libraries?

There are a few reasons for this:

As we'll learn, JSX needs to be compiled into JS

It enables quality-of-life improvements, like being able to use bleeding-edge JS features

It's necessary for good performance, since React apps often have hundreds or even thousands of JS files that need to be bundled together.