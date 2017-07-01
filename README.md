# Babel progress on [ECMAScript](https://github.com/tc39/ecma262) proposals

## [Official TC39 Proposals Repo](https://github.com/tc39/proposals)

## Proposals

For the official list, check the [TC39 repo](https://github.com/tc39/proposals). This list only contains all proposals higher than Stage 0 that are compilable by Babel. (If Stage 4, it will be in [preset-env](https://github.com/babel/babel-preset-env))

| Proposal Repo                                                                                               | Stage |
|-------------------------------------------------------------------------------------------------------------|-------|
| [Rest/Spread Properties](#restspread-properties)                               | 3     |
| [Asynchronous Iteration](#asynchronous-iteration)                                  | 3     |
| [Dynamic Import](#dynamic-import)                                               | 3     |
| [RegExp Unicode Property Escapes](#regexp-unicode-property-escapes)         | 3     |
| [RegExp Named Capture Groups](#regexp-named-capture-groups)                         | 3     |
| [`s` (`dotAll`) flag for regular expressions](https://github.com/mathiasbynens/es-regexp-dotall-flag)       | 3     |
| [`function.sent` metaproperty](https://github.com/allenwb/ESideas/blob/master/Generator%20metaproperty.md)  | 2     |
| [Class Fields](https://github.com/tc39/proposal-class-fields)                                               | 2     |
| [Class and Property Decorators](http://tc39.github.io/proposal-decorators/)                                 | 2     |
| [Arbitrary-precision Integers](https://github.com/tc39/proposal-integer)                                    | 2     |
| [`import.meta`](https://github.com/tc39/proposal-import-meta)                                               | 2     |
| [`export * as ns from "mod";` statements](https://github.com/leebyron/ecmascript-export-ns-from)            | 1     |
| [`export v from "mod";` statements](https://github.com/leebyron/ecmascript-export-default-from)             | 1     |
| Generator arrow functions (`=>*`)                                                                           | 1     |
| [Null Propagation](https://docs.google.com/presentation/d/11O_wIBBbZgE1bMVRJI8kGnmC6dWCBOwutbN9SWOK0fU/view)| 1     |
| [`do` Expressions](#do-expressions)                        | 1     |
| [Numeric Separator](#numeric-separator)                              | 1     |
| [Function Bind](#function-bind)                                      | 0     |

## Implemented

### [Rest/Spread Properties](https://github.com/tc39/proposal-object-rest-spread)

**TC39 Champion**: Sebastian Markbage  
**Preset**: [babel-preset-stage-3](https://www.npmjs.com/package/babel-preset-stage-3)  
**Plugin**: [babel-plugin-transform-object-rest-spread](https://www.npmjs.com/package/babel-plugin-transform-object-rest-spread)  

<details>
<summary>Code Example</summary>

```js
// Rest properties 
let { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
console.log(x); // 1 
console.log(y); // 2 
console.log(z); // { a: 3, b: 4 } 
 
// Spread properties 
let n = { x, y, ...z };
console.log(n); // { x: 1, y: 2, a: 3, b: 4 } 
```
</details>

### [Asynchronous Iteration](https://github.com/tc39/proposal-async-iteration) 

**TC39 Champion**: Domenic Denicola  
**Preset**: [babel-preset-stage-3](https://www.npmjs.com/package/babel-preset-stage-3)  
**Plugin**: [babel-plugin-transform-async-generator-functions](https://www.npmjs.com/package/babel-plugin-transform-async-generator-functions)  

<details>
<summary>Code Example</summary>

```js
async function* agf() {
  await 1;
  yield 2;
}

async function f() {
  for await (let x of y) {
    g(x);
  }
}
```
</details>

### [Dynamic Import](https://github.com/tc39/proposal-dynamic-import) 

**TC39 Champion**: Domenic Denicola  
**Preset**: [babel-preset-stage-3](https://www.npmjs.com/package/babel-preset-stage-3)  
**Plugins**: [babel-plugin-syntax-dynamic-import](https://www.npmjs.com/package/babel-plugin-syntax-dynamic-import)  


Webpack 1: https://github.com/airbnb/babel-plugin-dynamic-import-webpack  
Webpack 2: supports this by default (just needs Babel to parse)  
Node: https://www.npmjs.com/package/babel-plugin-dynamic-import-node  

<details>
<summary>Code Example</summary>

```js
import('test-module').then(() => (
  import('test-module-2');
));
```
</details>

### [RegExp Unicode Property Escapes](https://github.com/tc39/proposal-regexp-unicode-property-escapes)

**TC39 Champion**: Brian Terlson, Daniel Ehrenberg, Mathias Bynens  
**Preset**: [babel-preset-stage-3](https://www.npmjs.com/package/babel-preset-stage-3)  
**Plugins**: [babel-plugin-transform-unicode-property-regex](https://www.npmjs.com/package/babel-plugin-transform-unicode-property-regex)  
<details>
<summary>Code Example</summary>

```js
const a = /^\p{Decimal_Number}+$/u;
const b = /\p{Script_Extensions=Greek}/u;
```
</details>

### [RegExp Named Capture Groups](https://github.com/tc39/proposal-regexp-named-groups)

**TC39 Champion**: Daniel Ehrenberg, Brian Terlson  
**Preset**: N/A
**Plugins**: [babel-plugin-transform-modern-regexp](https://www.npmjs.com/package/babel-plugin-transform-modern-regexp)  
<details>
<summary>Code Example</summary>

```js
let re = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/u;

let result = re.exec('2015-01-02');
// result.groups.year === '2015';
// result.groups.month === '01';
// result.groups.day === '02';

// result[0] === '2015-01-02';
// result[1] === '2015';
// result[2] === '01';
// result[3] === '02';
```
</details>

### [`do` Expressions](https://gist.github.com/dherman/1c97dfb25179fa34a41b5fff040f9879)

**TC39 Champion**: Dave Herman  
**Preset**: [babel-preset-stage-1](https://www.npmjs.com/package/babel-preset-stage-1)  
**Plugins**: [babel-plugin-transform-do-expressions](https://www.npmjs.com/package/babel-plugin-transform-do-expressions)  
<details>
<summary>Code Example</summary>

```js
let a = do {
  if (x > 10) {
    'big';
  } else {
    'small';
  }
};

// let a = x > 10 ? 'big' : 'small';
```
</details>

### [Numeric Separator](https://github.com/tc39/proposal-numeric-separator)

**TC39 Champion**: Sam Goto  
**Preset**: [babel-preset-stage-1](https://www.npmjs.com/package/babel-preset-stage-1)  
**Plugins**: [babel-plugin-transform-numeric-separator](https://www.npmjs.com/package/babel-plugin-transform-numeric-separator)  
<details>
<summary>Code Example</summary>

```js
// Decimal Literals
let budget = 1_000_000_000_000;
// Binary Literals
let nibbles = 0b1010_0001_1000_0101;
// Hex Literal
let message = 0xA0_B0_C0;
```
</details>

### [Function Bind](https://github.com/tc39/proposal-regexp-named-groups)

**TC39 Champion**: Brian Terlson & Matthew Podwysocki  
**Preset**: [babel-preset-stage-0](https://www.npmjs.com/package/babel-preset-stage-0)  
**Plugins**: [babel-plugin-transform-function-bind](https://www.npmjs.com/package/babel-plugin-transform-function-bind)  
<details>
<summary>Code Example</summary>

```js
obj::func
// is equivalent to:
func.bind(obj)

obj::func(val)
// is equivalent to:
func.call(obj, val)

::obj.func(val)
// is equivalent to:
func.call(obj, val)
```
</details>

## Parser Only

## Not Implemented
