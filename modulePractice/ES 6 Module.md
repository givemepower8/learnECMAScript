# ES Module

Modules encapsulates functionality, and expose them to other JavaScript files as libraries. Modules let you create clearly separate and reusable snippets of functionality, each testable on its own.

Client-side JavaScript that runs in the browser uses another standard, called ES Modules.

## Why ES Module

ECMAScript 6 modules borrow many of the best features from CommonJS and AMD predecessors.

ECMAScript 6 modules are unique in their ability to be loaded both natively by the browser as well as in conjunction with third-party loaders and build tools.

In CommonJS, modules are loaded synchronously, and processed in the order the JavaScript runtime finds them. This system was born with server-side JavaScript in mind, and is not suitable for the client-side as the payload like network overhead. This is why ES Modules were introduced which tries to download the script needed on the fly.

## Named exports

```js
//------ lib.js ------
export const sqrt = Math.sqrt;
export function square(x) {
  return x * x;
}
export function diag(x, y) {
  return sqrt(square(x) + square(y));
}

//------ main.js ------

// import named exports only
import { square, diag } from 'lib';

// import the whole module
// import * as lib from 'lib';
console.log(square(11)); // 121
console.log(diag(4, 3)); // 5
```

Default exports (one per module)

```js
//------ myFunc.js ------
export default function() {} // no semicolon!

//------ main1.js ------
import myFunc from 'myFunc';
myFunc();

//------ MyClass.js ------
export default class {} // no semicolon!

//------ main2.js ------
import MyClass from 'MyClass';
const inst = new MyClass();

export default function foo() {} // no semicolon!
export default class Bar {} // no semicolon!
```

## Common issues

### ES6 module in node

As node is using commonJS as the module loader, ES6 import and export was not supported until [Announcing a new --experimental-modules](https://medium.com/@nodejs/announcing-a-new-experimental-modules-1be8d2d6c2ff).

Run it in node and VS Code

`node --experimental-modules main.js`

An alternative is using @babel/register.

`npm install --save-dev @babel/core @babel/cli @babel/preset-env @babel/node`

`node --require @babel/register "d:\Wei\GitHub\learnECMAScript\ECMA6\module\Practice\main.js"`

`node --require @babel/register "d:\Wei\GitHub\learnECMAScript\ECMA6\module\RediscoveringJSModuleExamples\left.mjs`

Or use the [esm ES module loader](https://github.com/standard-things/esm)

How to debug ECMAScript modules in VS Code?

If you use esm or pass --experimental-modules to Node.js in order to use ECMAScript modules, you can pass these options through the runtimeArgs attribute of launch.json:

- `"runtimeArgs": ["--experimental-modules"]` - Use the experimental ECMAScript modules support in Node v8.5.0+
- `"runtimeArgs": ["-r", "esm"]` - Use the esm ES module loader (Note that ["-r esm"] without a comma won't work)
