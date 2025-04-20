# Understanding JSX 

#### Q1:Paint to the DOM "Hello World!" using JSX 

**Answer**:

Index.js

```js
import React from 'react';
import { createRoot } from 'react-dom/client';

const element = (

  <p id="hello">
    Hello World!
  </p>

);

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

In the example above, we wrap the JSX in parentheses, like this:

```jsx
const element = (

  <p id="hello">
    Hello World!
  </p>

);
```

This is done purely for formatting purposes. It allows us to push the JSX onto the next line.

#### Q2:What is transpiling ? 

**Answer** : transpiling is the process of converting a higher level language to another higher level language , like the process of converting JSX to JS is called transpiling 

#### Q3:Can browsers understand JSX ? 

**Answer**: 

If we try to run this JSX code in the browser, we'll get an error. JavaScript engines don't understand JSX, they only understand JavaScript. And so we need to transpire  our code into plain JS.

This is most commonly done as part of a build step, using a tool like Babel

The JSX we write gets converted into `React.createElement`. By the time our code is running in the user's browser, all of the JSX has been zapped out, and we're left with a JS file full of nested `React.createElement` calls. 

#### Q4:Can a js file contain JSX ? 

**Answer**:

In the early days of React, any file that included JSX had to use the `.jsx` file extension. This was how we told the compiler: “Hey! This file has some JSX in it, and needs to be compiled to JS.”

This turned out to be a bit annoying. It was one more thing to think about, one more bit of friction in the development process. Having to rename a file whenever we add/remove JSX is a bit of a pain!

And so, the rules were loosened. These days, we can include JSX in a `.js` file, and everything will work perfectly*. Compilers assume that any `.js` file can contain JSX.

#### Q5: What is JSX transformer and why did React Team came up with JSX transformer in React 17 ?

**Answer**:

Let's look again at this code snippet:

```jsx
import React from 'react';
import { createRoot } from 'react-dom/client';

const element = (
  <p id="hello">
    Hello World!
  </p>
);

const container = document.querySelector('#root');
const root = createRoot(container);
root.render(element);
```

On the very first line, we're importing `React`, but we aren't actually using it anywhere… Are we? Can we omit it?

After we compile away the JSX, we're left with the following code:

```js
import React from 'react';

import { createRoot } from 'react-dom/client';

const element = React.createElement(

  'p',

  { id: 'hello' },

  'Hello World!'

);

const container = document.querySelector('#root');

const root = createRoot(container);

root.render(element);
```

When the JSX is compiled into plain JS, the dependency makes itself clear. That `<p>` tag becomes a `React.createElement` call! It's obfuscated? by the JSX.

In earlier versions of React, you'd get an error if you forgot to include the React import:

![react-not-defined](../assets/react-not-defined.png)

This was such a common stumbling block for beginners that the React team decided to spend some time seeing how they could improve things. And they came up with a pretty clever solution!

With React 17, the React team introduced a new “JSX transformer”, used by Babel and other compilers. Essentially, it *automatically injects the import* during the build process.

For example, let's suppose we had this code:

```js
const element = (
  <p id="hello">
    Hello World!
  </p>
);
```

Using the modern JSX transformer, it will get compiled to:

```js
import { jsx as _jsx } from 'react/jsx-runtime';



const element = _jsx(

  'p',

  { id: 'hello' },

  'Hello World!'

);
```

Note that our original code *didn't* include that import statement. It was included automatically by the compiler.

`_jsx` is a fancy optimized version of `React.createElement`. It includes some shortcuts when we use certain React features like Fragments or Portals. Otherwise, it does the exact same thing as `React.createElement`: it creates a React element.

And so, these days, we *don't* have to import React. The JSX compiler will solve this problem for us.