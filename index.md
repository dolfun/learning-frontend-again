# Progress tracker

Do check out my [GitHub](http://github.com/dolfun/) or my [ShaderToy](https://www.shadertoy.com/user/Dolfun) profile. \
[Resources page](resources.md)

## Day 23 (Sep 14)

Read about [Browser environment, specs](https://javascript.info/browser-environment), [DOM tree](https://javascript.info/dom-nodes), [Walking the DOM](https://javascript.info/dom-navigation), [Searching: getElement*, querySelector*](https://javascript.info/searching-elements-dom), [Node properties: type, tag and contents](https://javascript.info/basic-dom-node-properties) and [Attributes and properties](https://javascript.info/dom-attributes-and-properties).

- `<html>` = `document.documentElement`, `<body>` = `document.body` and `<head>` = `document.head`.
- `childNodes` property lists all child nodes, including text nodes.
- `childNodes` is not an array, it is a collection. It is iterable, but we cannot use array methods.
- DOM collections are live and read-only.
- `nextSibling`, `previousSibling` and `parentNode`.
- For element only navigation: `children`, `parentElement`, `nextElementSibling`, `previousElementSibling`, `firstElementChild`, `lastElementChild`.
- `parentElement` and `parentNode` are the same, except in the case of `document.documentElement`.
- `document.getElementById(id)`
- `elem.querySelectorAll(css)`
- `elem.querySelector(css)` = `elem.querySelectorAll(css)[0]`
- `elem.matches(css)`: returns `true` or `false`
- `elem.closest(css)`: The nearest ancestor that matches the CSS-selector including itself.
- `elem.getElementsByTagName(tag)`, `elem.getElementsByClassName(className)` and `document.getElementsByName(name)`
- All methods `"getElementsBy*"` return a live collection.
- `elemA.contains(elemB)`
- The `innerHTML` property allows to get the HTML inside the element as a string.
- The `outerHTML` property is `innerHTML` plus the element itself.
- Writing to `outerHTML` replaces it in the DOM.
- For text node we have `nodeValue` and `data` properties.
- `textContent` is the text inside the elements without any tags.
- `hidden` property is the same as `style="display:none"`.
- `elem.hasAttribute(name)`, `elem.getAttribute(name)`, `elem.setAttribute(name, value)` and `elem.removeAttribute(name)`
- HTML attributes' names are case-insensitive nd their values are always strings.
- All attributes starting with `“data-”` are reserved for programmers’ use. They are available in the `dataset` property. (`data-order-state` become camel-cased: `dataset.orderState`)

## Day 22 (Sep 11)

Read about [Introduction: callbacks](https://javascript.info/callbacks), [Promise](https://javascript.info/promise-basics), [Promises chaining](https://javascript.info/promise-chaining), [Error handling with promises](https://javascript.info/promise-error-handling), [Promisification](https://javascript.info/promisify), [Microtasks](https://javascript.info/microtask-queue), [Event loop: microtasks and macrotasks](https://javascript.info/event-loophttps://javascript.info/event-loop) and [Async/await](https://javascript.info/async-await).

- `const promise = new Promise((reslove, reject) => {...})`:
  - We call `resolve(value)` if the job finished successfully and `reject(error)` if an error had occured.
  - The returned `promise` object has a `state` property (which can be `"pending"`, `"fulfilled"` or `"rejected"`) and a `result` property (initially undefined, then changes to either `value` or `error` based on `resolve` or `reject` was called), both of which are internal.
  - The executor should call only one `resolve` or one `reject`. Any state change is final.
  - `promise.then((result) => {...}, (error) => {...} )`
  - For errors only: `promise.catch((error) => {...})`
  - `promise.finally(f)` is similar to `promise.then(f, f)`, but the `finally` handler has no arguments and it passes through the result or error to the next suitable handler.
  - The return value of a `finally` handler is ignored.
  - If the `finally` handler throws an error, then it goes to the next handler.
  - Every call to `.then` returns a new promise.
  - When a promise rejects, the control jumps to the closest rejection handler.
  - Inside a promise executor and handler, `throw new Error(...)` works the same as `reject(new Error(...))`.
- Promise API:
  - `Promise.all`: It resolves when all listed promises are resolved, and the array of their results becomes its result. \
  If any of the promises is rejected, the promise returned by `Promise.all` immediately rejects with that error and the other promises are ignored.
  - `Promise.allSettled`: It just waits for all promises to settle, regardless of the result. The resulting array has:
    - `{ status: "fulfilled", value: result }` for successful responses.
    - `{ status: "rejected", reason: error }` for errors.
  - `Promise.race`: It waits only for the first settled promise and gets its result (or error).
  - `Promise.any`: It waits only for the first fulfilled promise and gets its result. \
    If all of the given promises are rejected, then the returned promise is rejected with `AggregateError` – a special error object that stores all promise errors in its `errors` property.
  - `Promise.resolve(value)` is same as `new Promise(resolve => resolve(value))`
  - `Promise.reject(error)` is same as `new Promise((resolve, reject) => reject(error))`
- The microtask queue is first-in-first-out and execution of a task is initiated only when nothing else is running.
- There’s an in-browser minimal delay of 4ms for many nested `setTimeout` calls.
- Immediately after every macrotask, the engine executes all tasks from microtask queue, prior to running any other macrotasks or rendering or anything else.
- To schedule a new macrotask, use zero delayed `setTimeout(f)`.
- To schedule a new microtask, use `queueMicrotask(f)`. Also promise handlers go through the microtask queue.
- An `async` function always returns a promise, other values are wrapped into one automatically.
- `await` only works inside `async` functions. It makes the execution wait until that promise settles and returns its result.
- Modern browsers allow top-level `await` in modules.
- `await` accepts “thenables”

## Day 21 (Sep 10)

Read about [Class basic syntax](https://javascript.info/class) and [Error handling, "try...catch"](https://javascript.info/try-catch) \
Read: [JavaScript Closure: The Beginner's Friendly Guide](https://dmitripavlutin.com/javascript-closure/), [Gentle Explanation of "this" in JavaScript](https://dmitripavlutin.com/gentle-explanation-of-this-in-javascript/) and [5 Differences Between Arrow and Regular Functions](https://dmitripavlutin.com/differences-between-arrow-and-regular-functions/).

- `class User {...}`:

  ```js
  class User {
    constructor(name) { this.name = name; }
    func() { console.log(this.name); }
  }

  console.log(typeof User); // 'function'
  console.log(User === User.prototype.constructor); // true
  console.log(User.prototype.func); // [Function: func]
  console.log(Object.getOwnPropertyNames(User.prototype)); // [ 'constructor', 'func' ]
  ```

## Day 20 (Sep 9)

Read about [Property flags and descriptors](https://javascript.info/property-descriptors), [Property getters and setters](https://javascript.info/property-accessors), [Prototypal inheritance](https://javascript.info/prototype-inheritance), [F.prototype](https://javascript.info/function-prototype), [Native prototypes](https://javascript.info/native-prototypes) and [Prototype methods, objects without \_\_proto__](https://javascript.info/prototype-methods).

- Property flags: `writable`, `enumerable` and `configurable`
- `const descriptor = Object.getOwnPropertyDescriptor(obj, propertyName)`
- `Object.defineProperty(obj, propertyName, descriptor)`:
  - If a flag is not supplied, it is assumed `false`
  - We can change writable from `true` to `false` for a non-configurable property, but not the other way around
- `Object.defineProperties( obj, {prop1: descriptor1, prop2: descriptor2,  ... })`
- `Object.getOwnPropertyDescriptors(obj)`: returns all property descriptors, including symbolic and non-enumerable properties.
- `const clone = Object.defineProperties({}, Object.getOwnPropertyDescriptors(obj))`
- Getter and setter:
  
  ```js
  let const = {
    get propName() {
      // executed on obj.propName
    },

    set propName(value) {
      // executed on obj.propName = value
    }
  };
  ```

- For the accessor properties, it's descriptor has: `get`, `set`, `enumerable` and `configurable`.
- `__proto__` is a getter/setter for `[[Prototype]]`\
  The `__proto__` reference cannot be cycling and it can only be either an object or `null`.
- The prototype is only used for reading properties, write/delete operations work directly with the object. \
  Accessor properties are an exception, as assignment is handled by a setter function.
- `this` is not affected by prototypes at all, it is always the object before the dot.
- The `for..in` loop iterates over inherited properties too.
- `obj.hasOwnProperty(key)`: Checks if `obj` has its own (not inherited) property named `key`.
- When calling `new F()`, if `F.prototype` is an object, then the `new` operator uses it to set `[[Prototype]]` for the new object.
- The default `prototype` is an object with the only property `constructor` that points back to the function itself. \
  So for `function F() {}`, `F.prototype = { constructor: F }` exists by default.
- `obj.__proto__ === Object.prototype`, `arr.__proto__ === Array.prototype`, etc.
- Method borrowing:
  
  ```js
  function hash() {
    return [].join.call(arguments);
  }
  ```

  ```js
  const obj = {
    0: "Hello",
    1: "world!",
    length: 2,
  };

  obj.join = Array.prototype.join;
  console.log(obj.join(",")); // Hello,world!
  ```

- The modern methods to get/set a prototype are `Object.getPrototypeOf(obj)` and `Object.setPrototypeOf(obj, proto)`.
- `Object.create(proto[, descriptors])`: creates an empty object with given proto as `[[Prototype]]` and optional property descriptors
- Cloning an object: \
  `const clone = Object.create(Object.getPrototypeOf(obj), Object.getOwnPropertyDescriptors(obj))`
- Prototype-less objects: `obj = Object.create(null)` or `obj = { __proto__: null }`

## Day 19 (Sep 8)

Read about [The old "var"](https://javascript.info/var), [Global object](https://javascript.info/global-object), [Function object, NFE](https://javascript.info/function-object), [The "new Function" syntax](https://javascript.info/new-function), [Scheduling: setTimeout and setInterval](https://javascript.info/settimeout-setinterval), [Decorators and forwarding, call/apply](https://javascript.info/call-apply-decorators), [Function binding](https://javascript.info/bind), and [Arrow functions revisited](https://javascript.info/arrow-functions).

- [Global Object Summary](https://javascript.info/global-object#summary)
- A function’s name is accessible as the `name` property and the number of parameters is accessible via the `length` property (but rest parameters are not counted). We can also add properties of our own.
- Named function expression: `const func = function namedFunc() {...}` \
  It allows the function to reference itself and it is not visible outside.
- "new Function" syntax: `const func = new Function ([arg1, arg2, ...argN], functionBody)` \
  For example: \
  `const sum = new Function('a', 'b', 'return a + b')` \
  It's lexical environment is the global one.
- `let id = setTimeout|setInterval(func|code, [delay], [arg1], [arg2], ...)`
- `func.call(context, arg1, arg2, ...)` and `func.apply(context, args)` (args must be array-like)
- `func.bind(context, [arg1], [arg2], ...)`: A function cannot be re-bound.
- The arrow function doesn't have `this` and `arguments` in the current lexical environment.

## Day 18 (Sep 7)

Read about [WeakMap and WeakSet](https://javascript.info/weakmap-weakset), [Object.keys, values, entries](https://javascript.info/keys-values-entries), [Destructuring assignment](https://javascript.info/destructuring-assignment), [Date and time](https://javascript.info/date), [JSON methods, toJSON](https://javascript.info/json), [Rest parameters and spread syntax](https://javascript.info/rest-parameters-spread) and [Variable scope, closure](https://javascript.info/closure).

- `WeakMap`:
  - `WeakMap` keys must be objects
  - `weakMap.set(key, value)`
  - `weakMap.get(key)`
  - `weakMap.delete(key)`
  - `weakMap.has(key)`
  - Use case: caching
- `Object.keys(obj)`: returns an array of keys.
- `Object.values(obj)`: returns an array of values.
- `Object.entries(obj)`: returns an array of `[key, value]` pairs.
- `map.keys()` returns an iterable, while `Object.keys(obj)` returns an array.
- `Object.keys/values/entries` ignore symbolic properties.
- Destructuring:
  - `const [a, b] = [1, 2]`
  - `const [a, , c] = "abc";`
  - `for (const [key, value] of Object.entries(user)) {...}`
  - `[a, b] = [b, a]`
  - `const [a, b, ...c] = [1, 2, 3, 4, 5]`
  - Absent values are considered `undefined`.
  - `const [a = 1, b = 2] = [3]`
  - `const { var1, var2 } = { var1:..., var2:... }` \
    The order does not matter.
  - `const {prop : varName = defaultValue, ...rest} = object`
  - `const { height: a, width: b, title } = { title: "Menu", height: 10, width: 20 }`
  - `const { title, ...rest } = options`
  - `({a, b} = {a: 1, b: 2})`
  - `function({ incomingProperty: varName = defaultValue, ... } = {})`
- `Date`:
  - `new Date()`: current
  - `new Date(milliseconds)`: milliseconds passed after Jan 1st of 1970 UTC+0
  - `new Date("07-09-20")`
  - `new Date(year, month, date, hours, minutes, seconds, ms)`: Only first two arguments are required.
  - `Date.now()` returns the current timestamp.
  - `Date.parse(str)` reads a date from a string.
- For JSON, property names must be in quotes and all quotes must be double quotes.
- `JSON.stringify(value[, replacer, space])`:
  - It supports objects, arrays, stings, numbers, boolean and null.
  - There must be no circular references.
  - `replacer`: Array of properties to encode or a mapping function `function(key, value)`.
  - One can provide a `toJSON` method to override conversion via `JSON.stringify`.
- `JSON.parse(str[, reviver])`.
- Rest parameters:

  ```js
  function sum(...args) {
    return args.reduce((acc, val) => acc + val, 0);
  }
  ```

- `arguments` array-like and iterable object is a built-in, local variable, avalable inside all non-arrow functions.
- Spread syntax:
  - `Math.max(1, ...arr1, 2, ...arr2, 25)`
  - `const merged = [0, ...arr, 2, ...arr2]`
  - `Array.from` operates on both array-likes and iterables, but the spread syntax works only with iterables.

## Day 17 (Sep 4)

Read about [Iterables](https://javascript.info/iterable) and [Map and Set](https://javascript.info/map-set).

- Iterable example:

  ```js
  const range = {
    from: 1,
    to: 5,

    [Symbol.iterator]() {
      return {
        current: this.from,
        last: this.to,

        next() {
          if (this.current <= this.last) {
            return {
              done: false,
              value: this.current++
            };
          }

          return { done: true };
        }
      };
    }
  };
  ```

  or a shorter version:

  ```js
  const range = {
    from: 1,
    to: 5,

    [Symbol.iterator]() {
      this.current = this.from;
      return this;
    },

    next() {
      if (this.current <= this.to) {
        return { done: false, value: this.current++ };
      } else {
        return { done: true };
      }
    }
  };
  ```

- To be considered array-like, an object must fulfill two specific rules:
  1. It must have a non-negative `length` property.
  2. It must have indexed elements starting from `0` up to `length - 1`.
- `Array.from(obj[, mapFn, thisArg])` takes an iterable or an array-like and returns an `Array` object from it.
- `Map`:
  - `new Map()`
  - `map.set(key, value)`: returns the map itself
  - `map.get(key)`: returns `undefined` if `key` doesn't exist
  - `map.has(key)`
  - `map.delete(key)`
  - `map.clear()`
  - It uses `SameValueZero` for comparison.
  - `map.keys()`, `map.values()`, `map.entries()` all return iterables.
  - `Map` preserves insertion order.
  - `map.forEach(value, key, map)`
  - Map initialization:
  
    ```js
    const map = new Map([
      ["a", 1], ["b", 2], ["c", 3]
    ]);
    ```

  - `Object.entries(obj)`: Map from Object
  - `Object.fromEntries([[key, value], ...])`: Object from array of [`key`, `value`] pairs
- `Set`:
  - `new Set([iterable])`
  - `set.add(value)`: returns the set itself
  - `set.delete(value)`: returns whether the value existed when deleting
  - `set.has(value)`
  - `set.clear()`
  - `set.size`
  - We can loop over a set either with `for..of` or using `forEach`: `set.forEach((value, valueAgain, set) => {...})`
  - `set.keys()`, `set.values()` (same as `set.keys()`) and `set.entries()`(`[value, value]` pair)

## Day 16 (Sep 3)

Read [Object to primitive conversion](https://javascript.info/object-toprimitive), [Methods of primitives](https://javascript.info/primitives-methods), [Numbers](https://javascript.info/number), [Strings](https://javascript.info/string), [Arrays](https://javascript.info/array) and [Array methods](https://javascript.info/array-methods).

- `num.toString(base)` returns a string representation of `num` in the numeral system with the given `base`. For example: `123456..toString(36)`
- `Math.floor`, `Math.ceil`, `Math.round`, `Math.trunc`
- `.toFixed(n)` rounds the number to `n` digits and returns a string.
- `isNan` tests for `NaN`.
- `isFinite` returns `false` when the argument is one of `NaN`, `Infinity` or `-Infinity`, otherwise it returns `true`
- `Number.isNaN(value)` and `Number.isFinite(value)` also check if the argument belong to the number type.
- `NaN === NaN` is `false` but `Object.is(NaN, NaN)` is `true`. \
  `+0 === -0` is `true` but `Object.is(0, -0)` is `false`. \
  For all other cases `Object.is` behaves the same as `===`.
- `parseInt`/`parseFloat` "read" a number from a string until they cannot.
- `Math.random()` returns a random number in `[0, 1)`
- `Math.max(a, b, c...)` and `Math.min(a, b, c...)`
- `Math.pow(n, power)`
- `str.at(pos)` method alows negative position.
- Strings are immutable.
- `str.toUpperCase()` and `str.toLowerCase()`
- `str.indexOf(substr, pos)`: Returns the index of `substr` in `str` or `-1` if not found.
- `str.lastIndexOf(substr, pos)`
- `str.includes(substr, pos)` returns `true`/`false` depending on whether `str` contains `substr` within.
- `str.startsWith`, `str.endsWith`
- Substring:
  - `str.slice(start [, end])`: Negative indices are allowed.
  - `str.substring(start [, end])`: `start` can be greater than `end`
  - `str.substr(start [, length])`
- `str.codePointAt(pos)` and `String.fromCodePoint(code)`
- Array declaration:

  ```js
  const arr = new Array(n);
  const arr = [];
  ```

- `arr.at(i)` allow negative indices.
- Array methods:
  - `pop()`: Extracts the last element of the array and returns it.
  - `push(...items)`: Append the element to the end of the array.
  - `shift()`: Extracts the first element of the array and returns it.
  - `unshift(...items)`: Add the element to the beginning of the array.
  - Methods `push` and `unshift` can add multiple elements at once.
  - Methods `push`/`pop` run fast, while `shift`/`unshift` are slow.
  - `arr.splice(start[, deleteCount, elem1, ..., elemN])`: From index `start` remove `deleteCount` elements and insert `elem1, ..., elemN` at their place. \
    It returns the array of removed elements. \
    Negative indices are allowed.
  - `arr.slice([start], [end])`: It returns a new array copying to it all items from index `start` to `end` (not including `end`). \
    Negative indices are allowed.
  - `arr.concat(arg1, arg2...)`: It accepts either arrays or values. \
    If an object has `Symbol.isConcatSpreadable` property then it is treated as an array by `concat`.
  - `arr.forEach((item, index, array) => {...})`
  - `arr.indexOf(item, from)`, `arr.lastIndexOf(item, from)` and `arr.includes(item, from)`.
  - `arr.indexOf` uses `===` equality check, while `arr.includes` uses `SameValueZero`.
  - `arr.find((item, index, array) => {...})`: If the function returns `true`, the search is stopped, the `item` is returned.
  - `arr.findIndex` and `arr.findLastIndex` have the same syntax but they return the index of the element.
  - `arr.filter((item, index, array) => {...})`
  - `arr.map((item, index, array) => {...})`
  - Sorting: `arr.sort(fn)` \
    The comparison function can return a positive number to say greater and a negative number to say lesser. `[4, 3, 1].sort((a, b) => a - b)`
  - `arr.reverse()`
  - `str.split(delim)`: It splits the string into an array by the given delimiter `delim`.
  - `arr.join(glue)`: It creates a string of `arr` items joined by `glue` between them.
  - `arr.reduce` and `arr.reduceRight`:

    ```js
    let value = arr.reduce(function(acc, item, index, array) {
      // ...
    }, [initial]);
    ```

    For example: `[1, 2, 3].reduce((sum, current) => sum + current, 0);` \
    If `initial` is not provided, then it takes the first element as initial value.
  - `arr.some(fn)` and `arr.every(fn)`
  - `arr.fill(value, start, end)`
  - `arr.copyWithin(target, start, end)` – copies its elements from position `start` till position `end` into itself, at position `target` (overwrites existing).
  - `arr.flat(depth)`/`arr.flatMap(fn)` create a new flat array from a multidimensional array.

- Use `for..of` loops for arrays.
- The `length` property is writable.
- Array's `toString` method returns a comman-separated list of its element.
- `Array.isArray` to check if an object is an array.
- Almost all array methods that call functions – like `find`, `filter`, `map`, with a notable exception of `sort`, accept an optional additional parameter `thisArg`.

## Day 15 (Sep 2)

Read about [Debugging in the browser](https://javascript.info/debugging-chrome), [Polyfills and Transpilers](https://javascript.info/polyfills), [Garbage Collection](https://javascript.info/garbage-collection), [Constructor, operator "new"](https://javascript.info/constructor-new#constructor-mode-test-new-target), [Optional chaining '?.'](https://javascript.info/optional-chaining) and [Symbol type](https://javascript.info/symbol).

- `this` is not bound and arrow functions have no `this`.
- Constructor and `new` operator:
  
  ```js
  function User(name) {
    this.name = name;
    this.isAdmin = false;
  }

  let user = new User("Jack");
  ```

- `new.target` is a special property which is undefined for regular calls and equals the function if called with `new`.
- Return from constructors:
  - If `return` is called with an object, then the object is returned instead of `this`.
  - If `return` is called with a primitive, it’s ignored.
- The optional chaining `?.` stops the evaluation if the value before `?.` is `undefined` or `null` and returns `undefined`.
- `?.()` is used to call a function that may not exist.
- `object?.[key]` is also possible.
- Also we can use `?.` with `delete`.
- Symbol: `let id = Symbol("id");`
- To show a symbol, call `.toString()`, to obtain it's description, use the `.description` property.
- Symbolic properties do not participate in `for..in` loop. `Object.keys(user)` also ignores them. But `Object.assign` copies both string and symbol properties.
- Global symbols:
  - `Symbol.for(key)`: Returns a symbol by name (creates one if absent).
  - `Symbol.keyFor(sym)`: Returns a name by global symbol.

## Day 14 (Sep 1)

Read about [Javascript fundamentals](https://javascript.info/first-steps): [Comparisons](http://javascript.info/comparison), [Conditional branching: if, '?'](https://javascript.info/ifelse), [Logical operators](https://javascript.info/logical-operators), [Nullish coalescing operator '??'](https://javascript.info/nullish-coalescing-operator), [Loops: while and for](https://javascript.info/while-for), [The "switch" statement](https://javascript.info/switch), [Functions](https://javascript.info/function-basics), [Function expressions](https://javascript.info/function-expressions) and [Arrow functions, the basics](https://javascript.info/arrow-functions-basics). \
Also read about [Objects: the basics](https://javascript.info/object-basics): [Objects](https://javascript.info/object) and [Object references and copying](https://javascript.info/object-copy).

- String comparison is done lexicographically.
- When comparing values of different types, JavaScript converts the values to numbers.
- The strict equality operator `===` and the strict non-equality operator `!==` checks the equality without type conversion.
- The values `null` and `undefined` are equal `==` to themselves and each other, but do not equal any other value.
- The `if (…)` statement evaluates the expression in its parentheses and converts the result to a boolean.
- OR `||` finds the first truthy value from left to right. If none was found, then it returns the last value.
- AND `&&` finds the first falsy value.
- A double NOT `!!` is sometimes used for converting a value to boolean type.
- The nullish coalescing operator `??` returns the first argument if it’s not `null`/`undefined`. Otherwise, the second one.
- `!!=` operator assign if the current value is null or undefined. `||=` and `&&=` work similarly.
- [Labels for break/continue](https://chatgpt.com/s/t_6a96a620e8cc8191bfb055be37e5c6d3)
- `switch` statement uses strict eqality check.
- If a function is called, but an argument is not provided, then the corresponding value becomes `undefined`.
- A Function Expression is created when the execution reaches it and is usable only from that moment but a Function Declaration can be called earlier than it is defined.
- The `delete` keyword can be used to remove a property from an object.
- Computed properties:

  ```js
  const key = "name";

  const user = {
    [key]: "John"
  };
  ```

- Property value shorthand:

  ```js
    let user = {
      name,  // same as name:name
      age: 30
    };
  ```

- Property names can be any strings or symbols, there is no limitation. (except `__proto__`)
- Reading a non-existing property just returns `undefined`.
- `in` operator: `"key" in object` \
  In most cases comparison with `undefined` works fine, but it fails when an object property exists, but stores `undefined`.
- To walk over all keys of an object we can use the `for..in` loop: `for (key in object) {...}`
- [`Object.assign`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign#syntax): Can do shallow cloning
- [`structuredClone`](https://developer.mozilla.org/en-US/docs/Web/API/Window/structuredClone#description): Can perform deep cloning but methods are not supported.

## Day 13 (Aug 31)

Started reading [javascript.info](https://javascript.info/). \
Read about [Javascript fundamentals](https://javascript.info/first-steps): [Variables](https://javascript.info/variables), [Data Types](https://javascript.info/types), [Type Conversions](https://javascript.info/type-conversions) and [Basic Operators, Maths](https://javascript.info/operators).

- the dollar sign `$` can also be used in variable names.
- `NaN ** 0` is `1` (🤔, shouldn't have been?, [discussion](https://stackoverflow.com/questions/17863619/why-does-nan0-1), [wiki](https://en.wikipedia.org/wiki/NaN#Function_definition), [article](https://grouper.ieee.org/groups/msc/ANSI_IEEE-Std-754-2019/background/power.txt))
- Primitive types: `Number`, `BigInt`, `String`, `Boolean`, `null`, `undefined` and `Symbol`.
- The `typeof` operator returns the type of the operand.
- `typeof null` is `"object"` and `typeof alert` is `"function"`
- String conversion: `String(value)`
- Numeric conversion: `Number(value)` \
  `undefined` becomes `NaN` and `null` becomes `0`.
- Boolean conversion: `Boolean(value)` \
  `0`, `""`, `null`, `undefined` and `NaN` becomes `false`, other values become `true`.
- Binary `+` operator concatenates strings:

  ```js
  "my" + "string" === "mystring"
  "1" + 2 === "12"
  2 + "1" === "21"
  2 + 2 + "1" === "41"
  "1" + 2 + 2 === "122"
  6 - "2" === 4
  "6" / "2" === 3
  ```

- Unary `+x` is equivalent to `Number(x)`.
- [Operator Precedence Table](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_precedence#table)
- Assignment `=` is an operator and it returns a value.
- We can chain assignments: `a = b = c = 1;`
- Bitwise operators: Bitwise operators treat arguments as 32-bit integer numbers.
The list of operators:
- AND: `&`
- OR: `|`
- XOR: `^`
- NOT: `~`
- LEFT SHIFT: `<<`
- SIGNED RIGHT SHIFT: `>>`
- UNSIGNED RIGHT SHIFT: `>>>`

## Day 12 (Aug 28)

Read [Use Cases For Flexbox](https://www.smashingmagazine.com/2018/10/flexbox-use-cases/), [An Interactive Guide to CSS Grid](https://www.joshwcomeau.com/css/interactive-guide-to-grid/) and [A Complete CSS Grid Layout Guide](https://css-tricks.com/complete-guide-css-grid-layout/). \
Read about CSS variables and grid.

- Enabled with `display: grid`
- `grid-template-columns` property is used to specify width and number of columns.
- The `fr` unit is availabe to use with grids, it stands for fraction.
- Percentage-based columns are rigid while `fr`-based columns are flexible, it distrubutes the extra space.
- `gap` property adds a fixed amount of space between all of the columns and rows.
- By defining both `grid-template-rows` and `grid-template-columns` one can create an explicit grid.
- `repeat` function: `grid-template-columns: repeat(7, 1fr)`
- `grid-row: <grid-row-start> / <grid-row-end>`, similarly `grid-column` exists. \
  The numbers provided are line indices, not cell indices. \
  Negative numbers are also allowed.
- `grid-column: span n`
- `grid-template-area` and `grid-area`:
  
  ```css
  .parent {
    display: grid;
    grid-template-columns: 2fr 5fr;
    grid-template-rows: 50px 1fr;
    grid-template-areas:
      'sidebar header'
      'sidebar main';
  }
  .child {
    grid-area: main;
  }
  ```

- `justify-content: [start|center|end|space-between|space-around|space-evenly]`: It controls the distribution of columns
- `justify-items: stretch|start|center|end`: It aligns the items within their columns.
- While `justify-items` is set on the grid parent, `justify-self` is set on the child.
- `align-content` is like `justify-content` and `align-items` is like `justify-items` but they affects rows instead of columns.
- `place-content: center` is shorthand for:

  ```css
  justify-content: center;
  align-content: center;
  ```

## Day 11 (Aug 27)

Read about [`overflow` property](https://css-tricks.com/almanac/properties/o/overflow/) and [A Complete CSS Flexbox Layout Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).

- `overflow: visible | hidden | scroll | auto | inherit`:
  - `visible`: Default. Content is not clipped when it proceeds outside its box. Even though the content is visible outside of the box, that content does not affect the flow of the page.
  - `hidden`: Overflowing content will be hidden and inaccessible.
  - `scroll`: Overflowing content will be hidden and but accessible via scrolling.
  - `auto`: The scrollbars will only show up if there is content that actually breaks out of the element.
- Properties for flex container:
  - `display: flex`: enables flexbox.
  - `flex-direction: row | row-reverse | column | column-reverse`
  - `flex-wrap: nowrap | wrap | wrap-reverse`
  - `flex-flow: [flex-direction] [flex-wrap]`
  - `justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly | start | end | left | right ... + safe | unsafe`
    - `justify-content` defines the alignment along the main axis.
    - `safe` keeps the overflowing content accessible on the readable/scrollable side by changing an overflow alignment like `center` into a `start` alignment.
    - `unsafe` strictly enforces your chosen alignment, which can push parts of the content completely off-screen into an unscrollable area.
    <!-- markdownlint-disable-next-line MD033 -->
    <div style="text-align: center;"><img src="https://css-tricks.com/wp-content/uploads/2018/10/justify-content.svg" alt="justify-content illustration" width="50%"></div>
  - `align-items: stretch | flex-start | flex-end | center | baseline | first baseline | last baseline | start | end | self-start | self-end + ... safe | unsafe`
    - `align-items` defines the default behavior for how flex items are laid out along the cross axis on the current line.
    - `flex-start`: Flex container's cross-axis start
    - `start`: Flex container's writing mode
    - `self-start`: Individual flex own writing mode
    <!-- markdownlint-disable-next-line MD033 -->
      <div style="text-align: center;"><img src="https://css-tricks.com/wp-content/uploads/2018/10/align-items.svg" alt="align-items illustration" width="50%"></div>
  - `align-content: flex-start | flex-end | center | space-between | space-around | space-evenly | stretch | start | end + ... safe | unsafe`
    - `align-content` aligns a flex container’s lines within when there is extra space in the cross-axis.
    - This property only takes effect on multi-line flexible containers, where `flex-wrap` is set to either `wrap` or `wrap-reverse`.
      <!-- markdownlint-disable-next-line MD033 -->
      <div style="text-align: center;"><img src="https://css-tricks.com/wp-content/uploads/2018/10/align-content.svg" alt="align-content illustration" width="50%"></div>
  - `gap`, `row-gap` and `column-gap`:
    - `gap: [row and column gap]`
    - `gap: [row gap] [column gap]`
- Properties for flex items:
  - `order`: It controls the order in which they appear in the flex container. \
    Default is zero. \
    Items with the same `order` revert to source order.
  - `flex-grow`: Default is 0. It dictates what amount of the available space inside the flex container the item should take up as a proportion.
  - `flex-shrink`: Similar to `flex-grow` but for the case of shrinking.
  - `flex-basis`: It sets the initial size of a flex item along the main axis before the remaining space is distributed.
  - `align-self`: This allows the default alignment (or the one specified by `align-items`) to be overridden for individual flex items.
  - `flex: [grow] [shrink] [basis]`:
    - `flex: initial` -> `flex: 0 1 auto`
    - `flex: auto` -> `flex 1 1 auto`
    - `flex: none` -> `flex 0 0 auto`
    - `flex: 1` -> `flex 1 1 0%`
    - `flex: 2 100px` -> `flex 2 1 100px`

## Day 10 (Aug 26)

Read about the [`display` property](https://css-tricks.com/almanac/properties/d/display/) and [media queries](https://css-tricks.com/a-complete-guide-to-css-media-queries/). \
Read the [An Interactive Guide to Flexbox](https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/). \
Finished the [Flexbox Froggy](https://flexboxfroggy.com/) game.

- An `inline` element will accept `margin` and `padding` but it will only push other elements horizontally away, not vertically. It will ignore `height` and `width`.
- `inline-block` will respect `height` and `width`.
- Anatomy of a media query: ![Anatomy of a media query](https://i0.wp.com/css-tricks.com/wp-content/uploads/2020/09/media-query-anatomy.jpg)
- Flexbox Diagram:
  <!-- markdownlint-disable-next-line MD033 -->
  <div style="text-align: center;"><img src="https://css-tricks.com/wp-content/uploads/2018/11/00-basic-terminology.svg" alt="Flexbox Diagram" width="80%"></div>

## Day 9 (Aug 25)

Read about CSS: psuedo-elements, [`position` property](https://css-tricks.com/almanac/properties/p/position/) and [units](https://yurilee.hashnode.dev/css-units-are-confusing-af).

- Psuedo-elements:
  - `::before`: Adds something before the element's content.

    ```css
    .hello::before {
      content: "👋 ";
    }
    ```

  - `::after`: Adds something after the element's content.
  - `::first-letter`: Styles the first letter of text.
  - `::first-line`: Styles the first line of a paragraph.
  - `::selection`: Controls how text looks when the user highlights it.
- `!important` is a keyword flag used to force a specific style declaration to override any conflicting styles.
- `:is()` and `:where()` are CSS pseudo-class function that lets you group multiple selectors without repeating the common part. \
  For example:

  ```css
  h1:hover, h2:hover, h3:hover {
    color: red;
  }
  ```
  
  Can be written as:

  ```css
  :is(h1, h2, h3):hover {
    color: red;
  }
  ```

- `:is()` keeps the specificity of its most specific argument while `:where()` always has zero specificity.
- Units cheatsheet:
  ![CSS Units](https://yurilee.hashnode.dev/_next/image?url=https%3A%2F%2Fcdn.hashnode.com%2Fres%2Fhashnode%2Fimage%2Fupload%2Fv1626960364359%2FRITHUchJLk.png&w=3840&q=100)
- `position` property can take the following values:
  - `static`: Default. Element sticks to the normal page flow. `left`/`right`/`top`/`bottom`/`z-index` have no effect.
  - `relative`: Same as `static` but the positional properties move the element from the original position in that direction.
  - `absolute`: The element is removed from the flow of the document and other elements will behave as if it’s not even there. \
  The positioning origin is the padding edge of its nearest positioned ancestor (an ancestor element whose position is anything other than `static`).
  - `fixed`: The element is fixed to the viewport.
  - `sticky`: The element is treated like a `relative` value until the scroll location of the viewport reaches a specified threshold, at which point the element takes a `fixed` position where it is told to stick.
  - `inherit`: It inherits the positioning value from its parent.

## Day 8 (Aug 24)

Finished the [CSS Diner](https://flukeout.github.io/) minigame.\
Read about CSS: psuedo-classes and flexbox. \
Re-read CSS layout, box model and sticky.

- Psuedo-classes:
  - `:first-child`: Select a first child element inside of another element.
  - `:only-child`: Select an element that are the only element inside of another one.
  - `:last-child`: Select the last element inside of another element.
  - `:nth-child(n)`: Select an element by its order in another element.
  - `:nth-last-child(n)`: Select an element by its order in another element, counting from the back.
  - `:first-of-type`: Select the first element of a specific type.
  - `:nth-of-type(n)`: Selects a specific element based on its type and order in another element - or even or odd instances of that element.
  - `:nth-of-type(an+b)`: The nth-of-type formula selects every ath element, starting the count at a specific instance (bth) of that element.
  - `:only-of-type`: Select elements that are the only ones of their type within of their parent element
  - `:last-of-type`: Select the last element of a specific type.
  - `:empty`: Select elements that don't have children.
- Negation Pseudo-class: `:not(X)`

- Flexbox is enabled with `display: flex`
- `flex-direction: row|column` determines the primary and cross axis.
- We can change how children are distributed along the primary axis using the `justify-content` property and for the cross axis we use the `align-items` property.
- `justify-content: flex-start|center|flex-end|space-around|space-between|space-evenly`
- `align-items: flex-start|center|flex-end|stretch|baseline`
- `align-self` is applied to the child element, not the container. It allows us to change the alignment of a specific child along the cross axis.
- `align-self` has all the same values as `align-items`.
- Definitions:
  - `justify` — to position something along the primary axis.
  - `align` — to position something along the cross axis.
  - `content` — a group of “stuff” that can be distributed.
  - `items` — single items that can be positioned individually.
- Box model illustration:
  <!-- markdownlint-disable-next-line MD033 -->
  <div style="text-align: center;"><img src="https://web.dev/static/learn/css/box-model/image/a-diagram-showing-four-m-af72960a9e79a.svg" alt="Box model illustration" width="80%"></div>
- `box-sizing: content-box` is the default, width and height apply only to the content. \
  In `box-sizing: border-box` width and height include the content, padding, and border.
  
- To set the box sizing model to border-box for every element and every pseudo-element:
  
  ```css
  *, *::before, *::after {
    box-sizing: border-box;
  }```
- To make an element sticky, you must pair `position: sticky`; with at least one threshold inset property, such as `top`, `bottom`, `left`, or `right`.

## Day 7 (Aug 21)

Read about HTML forms and CSS Selectors.

- To explicitly associate a form control with a `<label>`, include the `for` attribute on the `<label>`, the value being the `id` of the form control it is associated with:
  
  ```html
  <form method="GET">
    <label for="student">Pick a student:</label>
    <select name="student" id="student">
      <option value="hoover">Hoover Sukhdeep</option>
      <option>Blendan Smooth</option>
      <option value="toasty">Toasty McToastface</option>
    </select>
    <input type="submit" value="Submit Form">
  </form>
  ```

- To provide implicit labels, include the form control between the opening and closing `<label>` tags.

- While individual input, select, and text areas are labeled with `<label>`, groups of form controls are labeled by the contents of the `<legend>` of the `<fieldset>` that groups them.
- The `method` attribute on the `<form>` tag defines the HTTP protocol of the request.
- With `GET`, the form data is sent as a parameter string of `name=value` pairs, appended to the action's URL.
- With `POST`, the data is appended to the body of the HTTP request.
- Radio button group:
  
  ```html
  <input type="radio" name="student" value="blendan"> Blendan
  <input type="radio" name="student" value="hoover"> Hoover
  <input type="radio" name="student" value="toasty"> Toasty
  ```

  The `name` attribute should be unique to the group.

- The file input type `<input type="file">` enables uploading files via forms.
- One cannot start a class (or an ID) with a number.
- CSS Selectors:
  - Universal selector - `*`
  - Type selector - `section`
  - Class selector - `.my-class`
  - ID selector - `#rad`
  - Attribute selector - `[data-type]`, `[data-type='primary']`
  - Compound selectors - `a.my-class`
- You can use case-sensitive attribute selectors by adding an `s` operator to your attribute selector: `[data-type='primary' s]`
- Attribute matcing:
  - `[href*='example.com']`: A href that contains "example.com"
  - `[href^='https']`: A href that starts with https
  - `[href$='.com']`: A href that ends with .com
- Combinators:
  - Descendant (`div p`): It targets any `p` inside the `div`.
  - Child (`div > p`): `<p>` must sit exactly one level below the `div`.
  - Subsequent sibling (`h1 ~ p`): Targets all `p` elements that follow the `h1`.
  - Next sibling (`h1 + p`): Targets only the very next sibling.
  - Comma Combinator (`h1, p`): Targets both `h1` and `p`.
- Examples:
  - `.top * + *`: Any element inside `.top` that immediately follows another element.
  - `.top > * + *::before`: The `::before` of any direct child of `.top` that immediately follows another direct child.
- [A tool that translates CSS selectors into plain-english explainers](https://kittygiraudel.github.io/selectors-explained/?)

## Day 6 (Aug 20)

Finished the remote section of [learngitbranching.js.org](https://learngitbranching.js.org/) tutorial. \
Read about HTML: `<image>` and `<table>`.

- `srcset` attribute:

  ```html
  <img src="images/eve.png" alt="Eve"
    srcset="images/eve.png 400w, images/eve-xl.jpg 800w"
    sizes="(max-width: 800px) 400px, 800px" />
  ```

- `<picture>` and `<source>` tags (!?):

  ```html
  <picture>
    <source
      srcset="images/eve.png 400w, images/eve-xl.jpg 800w"
      sizes="(max-width: 800px) 400px, 800px">
    <img src="images/eve.png" alt="Eve">
  </picture>
  ```

- At a minimum, each foreground image should include `src` and `alt` attributes.
- Lazy loading: `<img src="switch.svg" alt="light switch" loading="lazy" />`
- The preferred method of naming a table is the semantic element, `<caption>`.
- Table sectioning:
  
  ```html
  <table>
    <caption></caption>
    <thead></thead>
    <tbody></tbody>
    <tfoot></tfoot>
  </table>
  ```

- To join multiple cells into a single cell, use `colspan` and `rowspan` attributes.
- Only use a table for data.

## Day 5 (Aug 19)

Read about HTML: lists and navigation (table of content and page breadcrumbs). \
Finished the main section of [learngitbranching.js.org](https://learngitbranching.js.org/) tutorial.

- `menu` tag acts as a semantic alternative to the `ul` tag.
- Description list, i.e., `dl` tag:

  ```html
  <dl>
    <dt>Description Term 1</dt>
    <dd>Description Detail 1</dd>
    <dt>Description Term 2</dt>
    <dd>Description Detail 2</dd>
  </dl>
  ```

- "Skip to content" link:
  
  ```html
  <a href="#main" class="skip-link button">Skip to content</a>
  <main id="main">
    Content
  </main>
  ```

- `aria-label` and `aria-labelledby` attributes define the accessible name of an element.
- The current page could be identified with the `aria-current="page"` attribute.

## Day 4 (Aug 18)

Read about HTML document structure, semantic tags, headings and links.

- HTML template:

  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="utf-8" />
      <title>Title</title>
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    </head>
    <body>
      <!-- Body -->
    </body>
  </html>
  ```

- Favicon: `<link rel="icon" type="image/png" href="/images/favicon.png">`
- [<script src="..." async/defer>](https://javascript.info/script-async-defer)
- Some Semantic HTML Tags: `header`, `nav`, `main`, `section`, `article`, `aside` and `footer`.

  ```html
  <body>
  <header>Header</header>
  <nav>Nav</nav>
  <main>
    <article>First post</article>
    <article>Second post</article>
  </main>
  <aside>Aside</aside>
  <footer>Footer</footer>
  </body>
  ```

- [`tabindex`](https://web.dev/learn/html/attributes#tabindex) and [`contenteditable`](https://web.dev/learn/html/attributes#contenteditable) attributes

- `taget="_blank"` attribute on `a` tag open link in a new tab.

## Day 3 (Aug 17)

Read about Box model, revised git and started reading about HTML.

## Day 2 (Aug 13)

Read about `git tag`, `git log`, `git branch`, `git merge`, `git reset`, `git revert`, `git reflog` and `git rebase`.

### `git tag`

- `git tag <tagname> <commit_hash>`: Lightweight tags.
- `git tag -a <tagname>`: Annotated tags store extra meta data such as: the tagger name, email, and date.
- `git tag -l <wildcard>`: List tags with wildcard
- In the event that you must update an existing tag, the `-f FORCE` option must be used.
- `git push --tags`: 👍

### `git checkout`

- `git checkout -b ＜new-branch＞ ＜existing-branch＞`

### `git revert`

- It will create a new commit with the inverse of the last commit.

## Day 1 (Aug 12)

Read about `git init`, `git clone`, `git config`, `git alias`, `git add`, `git commit`, `.gitignore`, `git fetch`, `git pull` and `git push`.

### `git init`

- `git init --bare <directory>`: Initialize an empty Git repository, but omit the working directory.
- `git init <directory> --template=<template directory>`: Initialize a new Git repository and copy files from the  `＜template_directory＞` into the repository.
- `git init --quiet`
- `git init --separate-git-dir=<dir>`

### `git clone`

- `git clone <repo> <directory>`
- `git clone <repo> --branch <tag>`
- `git clone --depth 1`: shallow clone
- `git clone --bare` and `git clone --mirror` (?)

### `git config`

- `git config --[local/global/system] user.[name/email] <value>`

### `git add`

- `git add -p`: Begin an interactive staging session that lets you choose portions of a file to add to the next commit.

### `git commit`

- `git commit -a`: Commit a snapshot of all changes in the working directory. This only includes modifications to tracked files.

### `git stash`

- `git stash` and `git stash [pop/apply]`
- `git stash` will not stash new files in your working copy that have not yet been staged and files that have been ignored.
- `git stash save "message"`
- `git stash list`
- `git stash pop stash@{2}`
- `git stash drop stash@{1}` and `git stash clear`

### `.gitignore`

- [Git Ignore Patterns](https://www.atlassian.com/git/tutorials/saving-changes/gitignore)
- Ignoring a previously committed file:
    1. `echo debug.log >> .gitignore`
    2. `git rm --cached debug.log`
    3. `git commit -m "Start ignoring debug.log"`
- Committing an ignored file: `git add -f debug.log`
- Debugging `.gitignore` files: `git check-ignore -v debug.log`
  
  The output shows:
  `<file containing the pattern>:<line number of the pattern>:<pattern>  <file name>`

### `git fetch`

- `git fetch <remote>`: Fetch all of the branches from the repository. This also downloads all of the required commits and files from the other repository.
- `git fetch <remote> <branch>`: Only fetch the specified branch.
- `git fetch --all`: Fetches all registered remotes and their branches.
- `git fetch --dry-run`: It will output examples of actions it will take during the fetch but not apply them.

### `git pull`

- `git pull` = `git fetch` + `git merge`
- `git pull --rebase`
- `git pull --no-commit`: Unlike `git fetch`, it modifies the local working branch, but does not create an automatic commit.

### `git push`

- `git push <remote> --force`: 😱
- `git push <remote> --tags`: This flag sends all of your local tags to the remote repository as tags are not automatically pushed.
- Deleting a remote branch or tag: `git branch -D branch_name` followed by `git push origin :branch_name`
