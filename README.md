# Javascript Style Guide

*A mostly reasonable approach to TypeScript based off of [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)*

## Table of Contents

  1. [Types](#types)
  2. [References](#references)
  3. [Objects](#objects)
  4. [Arrays](#arrays)
  5. [Destructuring](#destructuring)
  6. [Strings](#strings)
  7. [Functions](#functions)
  8. [Arrow Functions](#arrow-functions)
  9. [Constructors](#constructors)
  10. [Modules](#modules)
  11. [Iterators and Generators](#iterators-and-generators)
  12. [Properties](#properties)
  13. [Variables](#variables)
  14. [Hoisting](#hoisting)
  15. [Comparison Operators & Equality](#comparison-operators--equality)
  16. [Blocks](#blocks)
  17. [Comments](#comments)
  18. [Whitespace](#whitespace)
  19. [Commas](#commas)
  20. [Semicolons](#semicolons)
  21. [Type Casting & Coercion](#type-casting--coercion)
  22. [Naming Conventions](#naming-conventions)
  23. [Accessors](#accessors)
  24. [Events](#events)
  25. [jQuery](#jquery)
  26. [Type Annotations](#type-annotations)
  27. [Interfaces](#interfaces)
  28. [Organization](#organization)
  29. [ECMAScript 5 Compatibility](#ecmascript-5-compatibility)
  30. [ECMAScript 6 Styles](#ecmascript-6-styles)
  31. [Typescript 1.5 Styles](#typescript-1.5-styles)
  32. [License](#license)

## Types

  - [1.1](#1.1) <a name='1.1'></a> **Primitives**: When you access a primitive type you work directly on its value.

    + `string`
    + `number`
    + `boolean`
    + `null`
    + `undefined`

    ```javascript
    const foo = 1;
    let bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```
  - [1.2](#1.2) <a name='1.2'></a> **Complex**: When you access a complex type you work on a reference to its value.

    + `object`
    + `array`
    + `function`

    ```javascript
    const foo = [1, 2];
    const bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```

**[⬆ back to top](#table-of-contents)**

## References

  - [2.1](#2.1) <a name='2.1'></a> Use `const` for all of your references; avoid using `var`.

  > Why? This ensures that you can't reassign your references (mutation), which can lead to bugs and difficult to comprehend code.

    ```javascript
    // bad
    var a = 1;
    var b = 2;

    // good
    const a = 1;
    const b = 2;
    ```

  - [2.2](#2.2) <a name='2.2'></a> If you must mutate references, use `let` instead of `var`.

  > Why? `let` is block-scoped rather than function-scoped like `var`.

    ```javascript
    // bad
    var count = 1;
    if (true) {

      count += 1;

    }

    // good, use the let.
    let count = 1;
    if (true) {

      count += 1;

    }
    ```

  - [2.3](#2.3) <a name='2.3'></a> Note that both `let` and `const` are block-scoped.

    ```javascript
    // const and let only exist in the blocks they are defined in.
    {
      let a = 1;
      const b = 1;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
    ```

**[⬆ back to top](#table-of-contents)**

## Objects

  - [3.1](#3.1) <a name='3.1'></a> Use the literal syntax for object creation.

    ```javascript
    // bad
    const item = new Object();

    // good
    const item = {};
    ```

  - [3.2](#3.2) <a name='3.2'></a> Don't use [reserved words](http://es5.github.io/#x7.6.1) as keys. It won't work in IE8. [More info](https://github.com/airbnb/javascript/issues/61).

    ```javascript
    // bad
    const superman = {
      default: { clark: 'kent' },
      private: true,
    };

    // good
    const superman = {
      defaults: { clark: 'kent' },
      hidden: true,
    };
    ```

  - [3.3](#3.3) <a name='3.3'></a> Use readable synonyms in place of reserved words.

    ```javascript
    // bad
    const superman = {
      class: 'alien',
    };

    // bad
    const superman = {
      klass: 'alien',
    };

    // good
    const superman = {
      type: 'alien',
    };
    ```

  <a name="es6-computed-properties"></a>
  - [3.4](#3.4) <a name='3.4'></a> Use computed property names when creating objects with dynamic property names.

  > Why? They allow you to define all the properties of an object in one place.

    ```javascript

    const getKey = function(k) {

      return `a key named ${k}`;

    }

    // bad
    const obj = {
      id: 5,
      name: 'San Francisco',
    };
    obj[getKey('enabled')] = true;

    // good
    const obj = {
      id: 5,
      name: 'San Francisco',
      [getKey('enabled')]: true,
    };
    ```

  <a name="es6-object-shorthand"></a>
  - [3.5](#3.5) <a name='3.5'></a> Use arrow functions for object methods instead of shorthand properties or an anonymous function.

    ```javascript
    // bad
    const atom = {
      value: 1,
      addValue: function (value) {
        return atom.value + value;
      },
    };

    // bad
    const atom = {
      value: 1,
      addValue(value) {
        return atom.value + value;
      },
    };

    // good
    const atom = {
      value: 1,
      addValue: (value) => atom.value + value
    };
    ```

  <a name="es6-object-concise"></a>
  - [3.6](#3.6) <a name='3.6'></a> Use property value shorthand.

  > Why? It is shorter to write and descriptive.

    ```javascript
    const lukeSkywalker = 'Luke Skywalker';

    // bad
    const obj = {
      lukeSkywalker: lukeSkywalker,
    };

    // good
    const obj = {
      lukeSkywalker,
    };
    ```

  - [3.7](#3.7) <a name='3.7'></a> Group your shorthand properties at the beginning of your object declaration.

  > Why? It's easier to tell which properties are using the shorthand.

    ```javascript
    const anakinSkywalker = 'Anakin Skywalker';
    const lukeSkywalker = 'Luke Skywalker';

    // bad
    const obj = {
      episodeOne: 1,
      twoJedisWalkIntoACantina: 2,
      lukeSkywalker,
      episodeThree: 3,
      mayTheFourth: 4,
      anakinSkywalker,
    };

    // good
    const obj = {
      lukeSkywalker,
      anakinSkywalker,
      episodeOne: 1,
      twoJedisWalkIntoACantina: 2,
      episodeThree: 3,
      mayTheFourth: 4,
    };
    ```

**[⬆ back to top](#table-of-contents)**

## Arrays

  - [4.1](#4.1) <a name='4.1'></a> Use the literal syntax for array creation.

    ```javascript
    // bad
    const items = new Array();

    // good
    const items = [];
    ```

  - [4.2](#4.2) <a name='4.2'></a> Use Array#push instead of direct assignment to add items to an array.

    ```javascript
    const someStack = [];


    // bad
    someStack[someStack.length] = 'abracadabra';

    // good
    someStack.push('abracadabra');
    ```

  <a name="es6-array-spreads"></a>
  - [4.3](#4.3) <a name='4.3'></a> Use array spreads `...` to copy arrays.

    ```javascript
    // bad
    const len = items.length;
    const itemsCopy = [];
    let i;

    for (i = 0; i < len; i++) {
      itemsCopy[i] = items[i];
    }

    // good
    const itemsCopy = [...items];
    ```
  - [4.4](#4.4) <a name='4.4'></a> To convert an array-like object to an array, use Array#from.

    ```javascript
    const foo = document.querySelectorAll('.foo');
    const nodes = Array.from(foo);
    ```

**[⬆ back to top](#table-of-contents)**

## Destructuring

  - [5.1](#5.1) <a name='5.1'></a> Use object destructuring when accessing and using multiple properties of an object.

  > Why? Destructuring saves you from creating temporary references for those properties.

    ```javascript
    // bad
    const getFullName = function(user) {

      const firstName = user.firstName;
      const lastName = user.lastName;

      return `${firstName} ${lastName}`;

    }

    // good
    const getFullName = function(obj) {

      const { firstName, lastName } = obj;
      return `${firstName} ${lastName}`;

    }

    // best
    const getFullName = function({ firstName, lastName }) {

      return `${firstName} ${lastName}`;

    }
    ```

  - [5.2](#5.2) <a name='5.2'></a> Use array destructuring.

    ```javascript
    const arr = [1, 2, 3, 4];

    // bad
    const first = arr[0];
    const second = arr[1];

    // good
    const [first, second] = arr;
    ```

  - [5.3](#5.3) <a name='5.3'></a> Use object destructuring for multiple return values, not array destructuring.

  > Why? You can add new properties over time or change the order of things without breaking call sites.

    ```javascript
    // bad
    const processInput = function(input) {
      // then a miracle occurs
      return [left, right, top, bottom];

    }

    // the caller needs to think about the order of return data
    const [left, __, top] = processInput(input);

    // good
    const processInput = function(input) {
      // then a miracle occurs
      return { left, right, top, bottom };

    }

    // the caller selects only the data they need
    const { left, right } = processInput(input);
    ```


**[⬆ back to top](#table-of-contents)**

## Strings

  - [6.1](#6.1) <a name='6.1'></a> Use single quotes `''` for strings.

    ```javascript
    // bad
    const name = "Capt. Janeway";

    // good
    const name = 'Capt. Janeway';
    ```

  - [6.2](#6.2) <a name='6.2'></a> Strings longer than 80 characters should be written across multiple lines using string concatenation.
  - [6.3](#6.3) <a name='6.3'></a> Note: If overused, long strings with concatenation could impact performance. [jsPerf](http://jsperf.com/ya-string-concat) & [Discussion](https://github.com/airbnb/javascript/issues/40).

    ```javascript
    // bad
    const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    const errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // good
    const errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';
    ```

  <a name="es6-template-literals"></a>
  - [6.4](#6.4) <a name='6.4'></a> When programmatically building up strings, use template strings instead of concatenation.

  > Why? Template strings give you a readable, concise syntax with proper newlines and string interpolation features.

    ```javascript
    // bad
    const sayHi = function(name) {

      return 'How are you, ' + name + '?';

    }

    // bad
    const sayHi = function(name) {

      return ['How are you, ', name, '?'].join();

    }

    // good
    const sayHi = function(name) {

      return `How are you, ${name}?`;

    }
    ```

**[⬆ back to top](#table-of-contents)**


## Functions

  - [7.1](#7.1) <a name='7.1'></a> Use function expressions instead of function declarations.

  > Why? Badly placed Function Declarations are misleading and there are few (if any) situations where you can’t use a Function Expression assigned to a variable instead. See [function-declarations-vs-function-expressions](https://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/).

    ```javascript
    // bad
    function foo() {
    }

    // good
    const foo = function() {
    };

    // good
    const foo = () => {
    };
    ```

  - [7.2](#7.2) <a name='7.2'></a> Function expressions:

    ```javascript
    // immediately-invoked function expression (IIFE)
    (() => {
      console.log('Welcome to the Internet. Please follow me.');
    })();
    ```

  - [7.3](#7.3) <a name='7.3'></a> Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad news bears.
  - [7.4](#7.4) <a name='7.4'></a> **Note:** ECMA-262 defines a `block` as a list of statements. A function declaration is not a statement. [Read ECMA-262's note on this issue](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97).

    ```javascript
    // bad
    if (currentUser) {

      const test = function() {

        console.log('Nope.');

      }

    }

    // good
    let test;
    if (currentUser) {

      test = () => {

        console.log('Yup.');

      };

    }
    ```

  - [7.5](#7.5) <a name='7.5'></a> Never name a parameter `arguments`. This will take precedence over the `arguments` object that is given to every function scope.

    ```javascript
    // bad
    const nope = function(name, options, arguments) {
      // ...stuff...
    }

    // good
    const yup = function(name, options, args) {
      // ...stuff...
    }
    ```

  <a name="es6-rest"></a>
  - [7.6](#7.6) <a name='7.6'></a> Never use `arguments`, opt to use rest syntax `...` instead.

  > Why? `...` is explicit about which arguments you want pulled. Plus rest arguments are a real Array and not Array-like like `arguments`.

    ```javascript
    // bad
    const concatenateAll = function() {

      const args = Array.prototype.slice.call(arguments);
      return args.join('');

    }

    // good
    const concatenateAll = function(...args) {

      return args.join('');

    }
    ```

  <a name="es6-default-parameters"></a>
  - [7.7](#7.7) <a name='7.7'></a> Use default parameter syntax rather than mutating function arguments.

    ```javascript
    // really bad
    const handleThings = function(opts) {
      // No! We shouldn't mutate function arguments.
      // Double bad: if opts is falsy it'll be set to an object which may
      // be what you want but it can introduce subtle bugs.
      opts = opts || {};
      // ...
    }

    // still bad
    const handleThings = function(opts) {

      if (opts === void 0) {

        opts = {};

      }
      // ...
    }

    // good
    const handleThings = function(opts = {}) {
      // ...
    }
    ```

  - [7.8](#7.8) <a name='7.8'></a> Avoid side effects with default parameters

  > Why? They are confusing to reason about.

  ```javascript
  var b = 1;
  // bad
  const count = function(a = b++) {

    console.log(a);

  }
  count();  // 1
  count();  // 2
  count(3); // 3
  count();  // 3
  ```


**[⬆ back to top](#table-of-contents)**

## Arrow Functions

  - [8.1](#8.1) <a name='8.1'></a> When you must use function expressions (as when passing an anonymous function), use arrow function notation.

  > Why? It creates a version of the function that executes in the context of `this`, which is usually what you want, and is a more concise syntax.

  > Why not? If you have a fairly complicated function, you might move that logic out into its own function declaration.

    ```javascript
    // bad
    [1, 2, 3].map(function (x) {

      return x * x;

    });

    // good
    [1, 2, 3].map((x) => {

      return x * x;

    });

    // good
    [1, 2, 3].map((x) => x * x;);
    ```

  - [8.2](#8.2) <a name='8.2'></a> If the function body fits on one line and there is only a single argument, feel free to omit the braces and parentheses, and use the implicit return. Otherwise, add the parentheses, braces, and use a `return` statement.

  > Why? Syntactic sugar. It reads well when multiple functions are chained together.

  > Why not? If you plan on returning an object.

    ```javascript
    // good
    [1, 2, 3].map(x => x * x);

    // good
    [1, 2, 3].reduce((total, n) => {
      return total + n;
    }, 0);
    ```

**[⬆ back to top](#table-of-contents)**


## Constructors

  - [9.1](#9.1) <a name='9.1'></a> Always use `class`. Avoid manipulating `prototype` directly.

  > Why? `class` syntax is more concise and easier to reason about.

    ```javascript
    // bad
    function Queue(contents = []) {

      this._queue = [...contents];

    }
    Queue.prototype.pop = function() {

      const value = this._queue[0];
      this._queue.splice(0, 1);
      return value;

    }


    // good
    class Queue {

      constructor(contents = []) {

        this._queue = [...contents];

      }

      pop() {

        const value = this._queue[0];
        this._queue.splice(0, 1);
        return value;

      }

    }
    ```

  - [9.2](#9.2) <a name='9.2'></a> Use `extends` for inheritance.

  > Why? It is a built-in way to inherit prototype functionality without breaking `instanceof`.

    ```javascript
    // bad
    const inherits = require('inherits');
    function PeekableQueue(contents) {

      Queue.apply(this, contents);

    }
    inherits(PeekableQueue, Queue);
    PeekableQueue.prototype.peek = function() {

      return this._queue[0];

    }

    // good
    class PeekableQueue extends Queue {

      peek() {

        return this._queue[0];

      }

    }
    ```

  - [9.3](#9.3) <a name='9.3'></a> Methods can return `this` to help with method chaining.

    ```javascript
    // bad
    Jedi.prototype.jump = function() {

      this.jumping = true;
      return true;

    };

    Jedi.prototype.setHeight = function(height) {

      this.height = height;

    };

    const luke = new Jedi();
    luke.jump(); // => true
    luke.setHeight(20); // => undefined

    // good
    class Jedi {

      jump() {

        this.jumping = true;
        return this;

      }

      setHeight(height) {

        this.height = height;
        return this;

      }

    }

    const luke = new Jedi();

    luke.jump()
      .setHeight(20);
    ```


  - [9.4](#9.4) <a name='9.4'></a> It's okay to write a custom toString() method, just make sure it works successfully and causes no side effects.

    ```javascript
    class Jedi {

      contructor(options = {}) {

        this.name = options.name || 'no name';

      }

      getName() {

        return this.name;

      }

      toString() {

        return `Jedi - ${this.getName()}`;

      }

    }
    ```

<a name="ts-classes"></a>
  - [9.5](#9.5) <a name='9.5'></a> Typescript classes placeholder.

**[⬆ back to top](#table-of-contents)**


## Modules

  - [10.1](#10.1) <a name='10.1'></a> Use modules (`import`/`export`) over a non-standard module system.

  > Why? Modules are the future, let's start using the future now.

    ```javascript
    // bad
    const AirbnbStyleGuide = require('./AirbnbStyleGuide');
    module.exports = AirbnbStyleGuide.es6;

    // ok
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    export default AirbnbStyleGuide.es6;

    // best
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  - [10.2](#10.2) <a name='10.2'></a>And do not export directly from an import.

  > Why? Although the one-liner is concise, having one clear way to import and one clear way to export makes things consistent.

    ```javascript
    // bad
    // filename es6.js
    export { es6 as default } from './airbnbStyleGuide';

    // good
    // filename es6.js
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  - [10.3](#10.3) <a name='10.3'></a>Use TypeScript module import for non-ES6 libraries with type definitions. Check [DefinitelyTyped](https://github.com/borisyankov/DefinitelyTyped) for available type definition files.

  > Why? This provides type information from external modules when available

    ```javascript
    // bad
    /// <reference path="lodash/lodash.d.ts" />
    var lodash = require('lodash')

    // good
    /// <reference path="lodash/lodash.d.ts" />
    import lodash = require('lodash')
    ```

  - [10.4](#10.4) <a name='10.4'></a>Group module imports by type and then alphabetic by variable name. Follow these rules for ordering your module imports:
    + External libraries with type definitions
    + Internal typescript modules with wildcard imports
    + Internal typescript modules without wildcard imports
    + External libraries without type definitions


  > Why? This makes your import section consistent across all modules.

    ```javascript
    // bad
    /// <reference path="../typings/tsd.d.ts" />
    import * as Api from './api';
    import _ = require('lodash');
    var Distillery = require('distillery-js');
    import Partner from './partner';
    import * as Util from './util';
    import Q = require('Q');
    var request = require('request');
    import Customer from './customer';

    // good
    /// <reference path="../typings/tsd.d.ts" />
    import _ = require('lodash');
    import Q = require('Q');
    import * as Api from './api';
    import * as Util from './util';
    import Customer from './customer';
    import Partner from './partner';
    var Distillery = require('distillery-js');
    var request = require('request');
    ```

**[⬆ back to top](#table-of-contents)**

## Iterators and Generators

  - [11.1](#11.1) <a name='11.1'></a> Don't use iterators. Prefer JavaScript's higher-order functions like `map()` and `reduce()` instead of loops like `for-of`.

  > Why? This enforces our immutable rule. Dealing with pure functions that return values is easier to reason about than side-effects.

    ```javascript
    const numbers = [1, 2, 3, 4, 5];

    // bad
    let sum = 0;
    for (let num of numbers) {

      sum += num;

    }

    sum === 15;

    // good
    let sum = 0;
    numbers.forEach((num) => sum += num);
    sum === 15;

    // best (use the functional force)
    const sum = numbers.reduce((total, num) => total + num, 0);
    sum === 15;
    ```

  - [11.2](#11.2) <a name='11.2'></a> Don't use generators for now.

  > Why? They don't transpile well to ES5.

**[⬆ back to top](#table-of-contents)**


## Properties

  - [12.1](#12.1) <a name='12.1'></a> Use dot notation when accessing properties.

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    // bad
    const isJedi = luke['jedi'];

    // good
    const isJedi = luke.jedi;
    ```

  - [12.2](#12.2) <a name='12.2'></a> Use subscript notation `[]` when accessing properties with a variable.

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    const getProp = function(prop) {

      return luke[prop];

    }

    const isJedi = getProp('jedi');
    ```

**[⬆ back to top](#table-of-contents)**


## Variables

  - [13.1](#13.1) <a name='13.1'></a> Always use `const` to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace. Captain Planet warned us of that.

    ```javascript
    // bad
    superPower = new SuperPower();

    // good
    const superPower = new SuperPower();
    ```

  - [13.2](#13.2) <a name='13.2'></a> Use one `const` declaration per variable.

    > Why? It's easier to add new variable declarations this way, and you never have to worry about swapping out a `;` for a `,` or introducing punctuation-only diffs.

    ```javascript
    // bad
    const items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';

    // bad
    // (compare to above, and try to spot the mistake)
    const items = getItems(),
        goSportsTeam = true;
        dragonball = 'z';

    // good
    const items = getItems();
    const goSportsTeam = true;
    const dragonball = 'z';
    ```

  - [13.3](#13.3) <a name='13.3'></a> Group all your `const`s and then group all your `let`s.

  > Why? This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

    ```javascript
    // bad
    let i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // bad
    let i;
    const items = getItems();
    let dragonball;
    const goSportsTeam = true;
    let len;

    // good
    const goSportsTeam = true;
    const items = getItems();
    let dragonball;
    let i;
    let length;
    ```

  - [13.4](#13.4) <a name='13.4'></a> Assign variables where you need them, but place them in a reasonable place.

  > Why? `let` and `const` are block scoped and not function scoped.

    ```javascript
    // good
    function() {

      test();
      console.log('doing stuff..');

      //..other stuff..

      const name = getName();

      if (name === 'test') {

        return false;

      }

      return name;

    }

    // bad - unnessary function call
    function(hasName) {

      const name = getName();

      if (!hasName) {

        return false;

      }

      this.setFirstName(name);

      return true;

    }

    // good
    function(hasName) {

      if (!hasName) {

        return false;

      }

      const name = getName();
      this.setFirstName(name);

      return true;

    }
    ```

**[⬆ back to top](#table-of-contents)**


## Hoisting

  - [14.1](#14.1) <a name='14.1'></a> `var` declarations get hoisted to the top of their scope, their assignment does not. `const` and `let` declarations are blessed with a new concept called [Temporal Dead Zones (TDZ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_dead_zone_and_errors_with_let). It's important to know why [typeof is no longer safe](http://es-discourse.com/t/why-typeof-is-no-longer-safe/15).

    ```javascript
    // we know this wouldn't work (assuming there
    // is no notDefined global variable)
    function example() {

      console.log(notDefined); // => throws a ReferenceError

    }

    // creating a variable declaration after you
    // reference the variable will work due to
    // variable hoisting. Note: the assignment
    // value of `true` is not hoisted.
    function example() {

      console.log(declaredButNotAssigned); // => undefined
      var declaredButNotAssigned = true;

    }

    // The interpreter is hoisting the variable
    // declaration to the top of the scope,
    // which means our example could be rewritten as:
    function example() {

      let declaredButNotAssigned;
      console.log(declaredButNotAssigned); // => undefined
      declaredButNotAssigned = true;

    }

    // using const and let
    function example() {

      console.log(declaredButNotAssigned); // => throws a ReferenceError
      console.log(typeof declaredButNotAssigned); // => throws a ReferenceError
      const declaredButNotAssigned = true;

    }
    ```

  - [14.2](#14.2) <a name='14.2'></a> Anonymous function expressions hoist their variable name, but not the function assignment.

    ```javascript
    function example() {

      console.log(anonymous); // => undefined

      anonymous(); // => TypeError anonymous is not a function

      var anonymous = function() {

        console.log('anonymous function expression');

      };

    }
    ```

  - [14.3](#14.3) <a name='14.3'></a> Named function expressions hoist the variable name, not the function name or the function body.

    ```javascript
    function example() {

      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      superPower(); // => ReferenceError superPower is not defined

      var named = function superPower() {

        console.log('Flying');

      };

    }

    // the same is true when the function name
    // is the same as the variable name.
    function example() {

      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      var named = function named() {

        console.log('named');

      }

    }
    ```

  - [14.4](#14.4) <a name='14.4'></a> Function declarations hoist their name and the function body.

    ```javascript
    function example() {

      superPower(); // => Flying

      function superPower() {

        console.log('Flying');

      }

    }
    ```

  - For more information refer to [JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting) by [Ben Cherry](http://www.adequatelygood.com/).

**[⬆ back to top](#table-of-contents)**


## Comparison Operators & Equality

  - [15.1](#15.1) <a name='15.1'></a> Use `===` and `!==` over `==` and `!=`.
  - [15.2](#15.2) <a name='15.2'></a> Conditional statements such as the `if` statement evaulate their expression using coercion with the `ToBoolean` abstract method and always follow these simple rules:

    + **Objects** evaluate to **true**
    + **Undefined** evaluates to **false**
    + **Null** evaluates to **false**
    + **Booleans** evaluate to **the value of the boolean**
    + **Numbers** evaluate to **false** if **+0, -0, or NaN**, otherwise **true**
    + **Strings** evaluate to **false** if an empty string `''`, otherwise **true**

    ```javascript
    if ([0]) {
      // true
      // An array is an object, objects evaluate to true
    }
    ```

  - [15.3](#15.3) <a name='15.3'></a> Use shortcuts.

    ```javascript
    // bad
    if (name !== '') {
      // ...stuff...
    }

    // good
    if (name) {
      // ...stuff...
    }

    // bad
    if (collection.length > 0) {
      // ...stuff...
    }

    // good
    if (collection.length) {
      // ...stuff...
    }
    ```

  - [15.4](#15.4) <a name='15.4'></a> For more information see [Truth Equality and JavaScript](http://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) by Angus Croll.

**[⬆ back to top](#table-of-contents)**


## Blocks

  - [16.1](#16.1) <a name='16.1'></a> Use braces with multi-line blocks or omit braces for two line blocks.

    ```javascript
    // bad
    if (test) return false;

    // ok
    if (test)
      return false;

    // good
    if (test) {

      return false;

    }

    // bad
    function() { return false; }

    // good
    function() {

      return false;

    }
    ```

  - [16.2](#16.2) <a name='16.2'></a> If you're using multi-line blocks with `if` and `else`, put `else` on the same line as your
    `if` block's closing brace.

    ```javascript
    // bad
    if (test) {
      thing1();
      thing2();
    }
    else {
      thing3();
    }

    // good
    if (test) {
      thing1();
      thing2();
    } else {
      thing3();
    }
    ```

    - [16.3](#16.3) <a name='16.3'></a> If you're using multi-line blocks with `if` and `else`, do not omit curly braces.

    > Why? Omitting curly braces in multi-line blocks can easily cause unexpected behavior.

      ```javascript
      // bad
      if (test)
        thing1();
        thing2();
      else
        thing3();

      // good
      if (test) {
        thing1();
        thing2();
      } else {
        thing3();
      }
      ```


**[⬆ back to top](#table-of-contents)**


## Comments

  - [17.1](#17.1) <a name='17.1'></a> Use `/** ... */` for multi-line comments. Include a description, specify types and values for all parameters and return values.

    ```javascript
    // bad
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param {String} tag
    // @return {Element} element
    const make = function(tag) {

      // ...stuff...

      return element;

    }

    // good
    /**
     * make() returns a new element
     * based on the passed in tag name
     *
     * @param {String} tag
     * @return {Element} element
     */
    const make = function(tag) {

      // ...stuff...

      return element;

    }
    ```

  - [17.2](#17.2) <a name='17.2'></a> Use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment.

    ```javascript
    // bad
    const active = true;  // is current tab

    // good
    // is current tab
    const active = true;

    // bad
    const getType = function() {

      console.log('fetching type...');
      // set the default type to 'no type'
      const type = this._type || 'no type';

      return type;

    }

    // good
    const getType = function() {

      console.log('fetching type...');

      // set the default type to 'no type'
      const type = this._type || 'no type';

      return type;

    }
    ```

  - [17.3](#17.3) <a name='17.3'></a> Prefixing your comments with `FIXME` or `TODO` helps other developers quickly understand if you're pointing out a problem that needs to be revisited, or if you're suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. The actions are `FIXME -- need to figure this out` or `TODO -- need to implement`.

  - [17.4](#17.4) <a name='17.4'></a> Use `// FIXME:` to annotate problems.

    ```javascript
    class Calculator {

      constructor() {
        // FIXME: shouldn't use a global here
        total = 0;
      }

    }
    ```

  - [17.5](#17.5) <a name='17.5'></a> Use `// TODO:` to annotate solutions to problems.

    ```javascript
    class Calculator {

      constructor() {
        // TODO: total should be configurable by an options param
        this.total = 0;
      }

    }
    ```

**[⬆ back to top](#table-of-contents)**


## Whitespace

  - [18.1](#18.1) <a name='18.1'></a> Use soft tabs set to 2 spaces.

    ```javascript
    // bad
    function() {

    ∙∙∙∙const name;

    }

    // bad
    function() {

    ∙const name;

    }

    // good
    function() {

    ∙∙const name;

    }
    ```

  - [18.2](#18.2) <a name='18.2'></a> Place 1 space before the leading brace.

    ```javascript
    // bad
    const test = function(){

      console.log('test');

    }

    // good
    const test = function() {

      console.log('test');

    }

    // bad
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });

    // good
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });
    ```

  - [18.3](#18.3) <a name='18.3'></a> Place 1 space before the opening parenthesis in control statements (`if`, `while` etc.). Place no space before the argument list in function calls and declarations.

    ```javascript
    // bad
    if(isJedi) {

      fight ();

    }

    // good
    if (isJedi) {

      fight();

    }

    // bad
    const fight = function () {

      console.log ('Swooosh!');

    }

    // good
    const fight = function() {

      console.log('Swooosh!');

    }
    ```

  - [18.4](#18.4) <a name='18.4'></a> Set off operators with spaces.

    ```javascript
    // bad
    const x=y+5;

    // good
    const x = y + 5;
    ```

  - [18.5](#18.5) <a name='18.5'></a> End files with a single newline character.

    ```javascript
    // bad
    (function(global) {
      // ...stuff...
    })(this);
    ```

    ```javascript
    // bad
    (function(global) {
      // ...stuff...
    })(this);↵
    ↵
    ```

    ```javascript
    // good
    (function(global) {
      // ...stuff...
    })(this);↵
    ```

  - [18.5](#18.5) <a name='18.5'></a> Use indentation when making long method chains. Use a leading dot, which
    emphasizes that the line is a method call, not a new statement.

    ```javascript
    // bad
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // bad
    $('#items').
      find('.selected').
        highlight().
        end().
      find('.open').
        updateCount();

    // good
    $('#items')
      .find('.selected')
        .highlight()
        .end()
      .find('.open')
        .updateCount();

    // bad
    const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').class('led', true)
        .attr('width', (radius + margin) * 2).append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(tron.led);

    // good
    const leds = stage.selectAll('.led')
        .data(data)
      .enter().append('svg:svg')
        .classed('led', true)
        .attr('width', (radius + margin) * 2)
      .append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(tron.led);
    ```

  - [18.6](#18.6) <a name='18.6'></a> Leave a blank line after the opening of a block and before the closing of a block

  ```javascript
  // bad
  if (foo) {
    return bar;
  }

  // good
  if (foo) {

    return bar;

  }

  // bad
  const baz = function(foo) {
    return bar;
  }

  // good
  const baz = function(foo) {

    return bar;

  }
  ```

  - [18.7](#18.7) <a name='18.7'></a> Leave a blank line after blocks and before the next statement.

    ```javascript
    // bad
    if (foo) {

      return bar;

    }
    return baz;

    // good
    if (foo) {

      return bar;

    }

    return baz;

    // bad
    const obj = {
      foo() {
      },
      bar() {
      },
    };
    return obj;

    // good
    const obj = {
      foo() {
      },

      bar() {
      },
    };

    return obj;
    ```


**[⬆ back to top](#table-of-contents)**

## Commas

  - [19.1](#19.1) <a name='19.1'></a> Leading commas: **Nope.**

    ```javascript
    // bad
    const story = [
        once
      , upon
      , aTime
    ];

    // good
    const story = [
      once,
      upon,
      aTime,
    ];

    // bad
    const hero = {
        firstName: 'Ada'
      , lastName: 'Lovelace'
      , birthYear: 1815
      , superPower: 'computers'
    };

    // good
    const hero = {
      firstName: 'Ada',
      lastName: 'Lovelace',
      birthYear: 1815,
      superPower: 'computers',
    };
    ```

  - [19.2](#19.2) <a name='19.2'></a> Additional trailing comma: **Yup.**

  > Why? This leads to cleaner git diffs. Also, transpilers like Babel will remove the additional trailing comma in the transpiled code which means you don't have to worry about the [trailing comma problem](es5/README.md#commas) in legacy browsers.

    ```javascript
    // bad - git diff without trailing comma
    const hero = {
         firstName: 'Florence',
    -    lastName: 'Nightingale'
    +    lastName: 'Nightingale',
    +    inventorOf: ['coxcomb graph', 'mordern nursing']
    }

    // good - git diff with trailing comma
    const hero = {
         firstName: 'Florence',
         lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'mordern nursing'],
    }

    // bad
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully'
    };

    const heroes = [
      'Batman',
      'Superman'
    ];

    // good
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully',
    };

    const heroes = [
      'Batman',
      'Superman',
    ];
    ```

**[⬆ back to top](#table-of-contents)**


## Semicolons

  - [20.1](#20.1) <a name='20.1'></a> **Yup.**

    ```javascript
    // bad
    (function() {

      const name = 'Skywalker'
      return name

    })()

    // good
    (() => {

      const name = 'Skywalker';
      return name;

    })();

    // good (guards against the function becoming an argument when two files with IIFEs are concatenated)
    ;(() => {

      const name = 'Skywalker';
      return name;

    })();
    ```

    [Read more](http://stackoverflow.com/a/7365214/1712802).

**[⬆ back to top](#table-of-contents)**


## Type Casting & Coercion

  - [21.1](#21.1) <a name='21.1'></a> Perform type coercion at the beginning of the statement.
  - [21.2](#21.2) <a name='21.2'></a> Strings:

    ```javascript
    //  => this.reviewScore = 9;

    // bad
    const totalScore = this.reviewScore + '';

    // good
    const totalScore = String(this.reviewScore);
    ```

  - [21.3](#21.3) <a name='21.3'></a> Use `parseInt` for Numbers and always with a radix for type casting.

    ```javascript
    const inputValue = '4';

    // bad
    const val = new Number(inputValue);

    // bad
    const val = +inputValue;

    // bad
    const val = inputValue >> 0;

    // bad
    const val = parseInt(inputValue);

    // good
    const val = Number(inputValue);

    // good
    const val = parseInt(inputValue, 10);
    ```

  - [21.4](#21.4) <a name='21.4'></a> If for whatever reason you are doing something wild and `parseInt` is your bottleneck and need to use Bitshift for [performance reasons](http://jsperf.com/coercion-vs-casting/3), leave a comment explaining why and what you're doing.

    ```javascript
    // good
    /**
     * parseInt was the reason my code was slow.
     * Bitshifting the String to coerce it to a
     * Number made it a lot faster.
     */
    const val = inputValue >> 0;
    ```

  - [21.5](#21.5) <a name='21.5'></a> **Note:** Be careful when using bitshift operations. Numbers are represented as [64-bit values](http://es5.github.io/#x4.3.19), but Bitshift operations always return a 32-bit integer ([source](http://es5.github.io/#x11.7)). Bitshift can lead to unexpected behavior for integer values larger than 32 bits. [Discussion](https://github.com/airbnb/javascript/issues/109). Largest signed 32-bit Int is 2,147,483,647:

    ```javascript
    2147483647 >> 0 //=> 2147483647
    2147483648 >> 0 //=> -2147483648
    2147483649 >> 0 //=> -2147483647
    ```

  - [21.6](#21.6) <a name='21.6'></a> Booleans:

    ```javascript
    const age = 0;

    // bad
    const hasAge = new Boolean(age);

    // good
    const hasAge = Boolean(age);

    // good
    const hasAge = !!age;
    ```

**[⬆ back to top](#table-of-contents)**


## Naming Conventions

  - [22.1](#22.1) <a name='22.1'></a> Avoid single letter names. Be descriptive with your naming.

    ```javascript
    // bad
    function q() {
      // ...stuff...
    }

    // good
    function query() {
      // ..stuff..
    }
    ```

  - [22.2](#22.2) <a name='22.2'></a> Use camelCase when naming objects, functions, and instances.

    ```javascript
    // bad
    const OBJEcttsssss = {};
    const this_is_my_object = {};
    const c = function() {}

    // good
    const thisIsMyObject = {};
    const thisIsMyFunction = function() {}
    ```

  - [22.3](#22.3) <a name='22.3'></a> Use PascalCase when naming constructors, classes, modules, or interfaces.

    ```javascript
    // bad
    function user(options) {

      this.name = options.name;

    }

    const bad = new user({
      name: 'nope',
    });

    // good
    module AperatureScience {

      class User {

        constructor(options) {

          this.name = options.name;

        }

      }

    }

    const good = new AperatureScience.User({
      name: 'yup',
    });
    ```

  - [22.4](#22.4) <a name='22.4'></a> Use snake_case when naming object properties.

    ```javascript
    // bad
    const panda = {
      firstName: 'Mr.',
      LastName: 'Panda'
    }

    // good
    const panda = {
      first_name: 'Mr.',
      Last_name: 'Panda'
    }
    ```

  - [22.5](#22.5) <a name='22.5'></a> Use a leading underscore `_` when naming private properties.

    ```javascript
    // bad
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';

    // good
    this._firstName = 'Panda';
    ```

  - [22.6](#22.6) <a name='22.6'></a> Don't save references to `this`. Use arrow functions or Function#bind.

    ```javascript
    // bad
    function foo() {

      const self = this;
      return function() {

        console.log(self);

      };

    }

    // bad
    function foo() {

      const that = this;
      return function() {

        console.log(that);

      };

    }

    // good
    function foo() {

      return () => {
        console.log(this);
      };

    }
    ```

  - [22.7](#22.7) <a name='22.7'></a> If your file exports a single class, your filename should be exactly the name of the class.
    ```javascript
    // file contents
    class CheckBox {
      // ...
    }
    export default CheckBox;

    // in some other file
    // bad
    import CheckBox from './checkBox';

    // bad
    import CheckBox from './check_box';

    // good
    import CheckBox from './CheckBox';
    ```

  - [22.8](#22.8) <a name='22.8'></a> Use camelCase when you export-default a function. Your filename should be identical to your function's name.

    ```javascript
    function makeStyleGuide() {
    }

    export default makeStyleGuide;
    ```

  - [22.9](#22.9) <a name='22.9'></a> Use PascalCase when you export a singleton / function library / bare object.

    ```javascript
    const AirbnbStyleGuide = {
      es6: {
      }
    };

    export default AirbnbStyleGuide;
    ```


**[⬆ back to top](#table-of-contents)**


## Accessors

  - [23.1](#23.1) <a name='23.1'></a> Accessor functions for properties are not required.
  - [23.2](#23.2) <a name='23.2'></a> If you do make accessor functions use getVal() and setVal('hello').

    ```javascript
    // bad
    dragon.age();

    // good
    dragon.getAge();

    // bad
    dragon.age(25);

    // good
    dragon.setAge(25);
    ```

  - [23.3](#23.3) <a name='23.3'></a> If the property is a boolean, use isVal() or hasVal().

    ```javascript
    // bad
    if (!dragon.age()) {
      return false;
    }

    // good
    if (!dragon.hasAge()) {
      return false;
    }
    ```

  - [23.4](#23.4) <a name='23.4'></a> It's okay to create get() and set() functions, but be consistent.

    ```javascript
    class Jedi {

      constructor(options = {}) {

        const lightsaber = options.lightsaber || 'blue';
        this.set('lightsaber', lightsaber);

      }

      set(key, val) {

        this[key] = val;

      }

      get(key) {

        return this[key];

      }

    }
    ```

**[⬆ back to top](#table-of-contents)**


## Events

  - [24.1](#24.1) <a name='24.1'></a> When attaching data payloads to events (whether DOM events or something more proprietary like Backbone events), pass a hash instead of a raw value. This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event. For example, instead of:

    ```javascript
    // bad
    $(this).trigger('listingUpdated', listing.id);

    ...

    $(this).on('listingUpdated', function(e, listingId) {
      // do something with listingId
    });
    ```

    prefer:

    ```javascript
    // good
    $(this).trigger('listingUpdated', { listingId : listing.id });

    ...

    $(this).on('listingUpdated', function(e, data) {
      // do something with data.listingId
    });
    ```

  **[⬆ back to top](#table-of-contents)**


## jQuery

  - [25.1](#25.1) <a name='25.1'></a> Prefix jQuery object variables with a `$`.

    ```javascript
    // bad
    const sidebar = $('.sidebar');

    // good
    const $sidebar = $('.sidebar');
    ```

  - [25.2](#25.2) <a name='25.2'></a> Cache jQuery lookups.

    ```javascript
    // bad
    function setSidebar() {

      $('.sidebar').hide();

      // ...stuff...

      $('.sidebar').css({
        'background-color': 'pink'
      });

    }

    // good
    function setSidebar() {

      const $sidebar = $('.sidebar');
      $sidebar.hide();

      // ...stuff...

      $sidebar.css({
        'background-color': 'pink'
      });

    }
    ```

  - [25.3](#25.3) <a name='25.3'></a> For DOM queries use Cascading `$('.sidebar ul')` or parent > child `$('.sidebar > ul')`. [jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)
  - [25.4](#25.4) <a name='25.4'></a> Use `find` with scoped jQuery object queries.

    ```javascript
    // bad
    $('ul', '.sidebar').hide();

    // bad
    $('.sidebar').find('ul').hide();

    // good
    $('.sidebar ul').hide();

    // good
    $('.sidebar > ul').hide();

    // good
    $sidebar.find('ul').hide();
    ```

**[⬆ back to top](#table-of-contents)**


## Type Annotations

<a name="ts-type-annotations"></a>
  - [26.1](#26.1) <a name='26.1'></a> Type annotations placeholder.

<a name="ts-generics"></a>
  - [26.2](#26.2) <a name='26.2'></a> Use "T" for the type variable if only one is needed.

```javascript
function identify<T>(arg: T): T {

    return arg;

}
```

  - [26.3](#26.3) <a name='26.3'></a> If more than one type variable is required, start with letter "T" and name your variable in alphabetical sequence.

```javascript
function find<T, U extends Findable>(needle: T, haystack: U): U {

  return haystack.find(needle)

}
```

  - [26.4](#26.4) <a name='26.4'></a> When possible, allow the compiler to infer type of variables.

```javascript
// bad
const output = identify<string>("myString");

// good
const output = identity("myString");
```

  - [26.5](#26.5) <a name='26.5'></a> When creating factories using generics, be sure to include the constructor function in the type.

```javascript
function create<t>(thing: {new(): T;}): T {

  return new thing();

}
```

**[⬆ back to top](#table-of-contents)**


## Interfaces

<a name="ts-interfaces"></a>
  - [27.1](#27.1) <a name='27.1'></a> Interface placeholder.

**[⬆ back to top](#table-of-contents)**


## Organization

<a name="ts-modules"></a>
  - [28.1](#28.1) <a name='28.1'></a> 1 file per logical component, and each file should be divided into logical divisions via modules.

  ```javascript
  module Automobile {

    module Honda {

    }

  }
  ```

  - [28.2](#28.2) <a name='28.2'></a> Export one main module per file so it can be required by other files.

  ```javascript
  module Automobile {

    // hidden module, will not be accessible via "require"
    Honda {

    }

    // public module, will be accessible via "require"
    export Ford {

      export function vroom() {

        console.log('vroom!');

      }

    }

  }

  export default Automobile;
  ```

- [28.3](#28.3) <a name='28.3'></a> Order your code (alphabetically) in the following order within each module:
   - var
   - export var
   - let
   - export let
   - const
   - export const
   - interface
   - export interface
   - function
   - export function
   - class
   - export class
   - module
   - export module

**[⬆ back to top](#table-of-contents)**


## ECMAScript 5 Compatibility

  - [29.1](#29.1) <a name='29.1'></a> Refer to [Kangax](https://twitter.com/kangax/)'s ES5 [compatibility table](http://kangax.github.com/es5-compat-table/).

**[⬆ back to top](#table-of-contents)**

## ECMAScript 6 Styles

  - [30.1](#30.1) <a name='30.1'></a> This is a collection of links to the various es6 features.

1. [Arrow Functions](#arrow-functions)
1. [Classes](#constructors)
1. [Object Shorthand](#es6-object-shorthand)
1. [Object Concise](#es6-object-concise)
1. [Object Computed Properties](#es6-computed-properties)
1. [Template Strings](#es6-template-literals)
1. [Destructuring](#destructuring)
1. [Default Parameters](#es6-default-parameters)
1. [Rest](#es6-rest)
1. [Array Spreads](#es6-array-spreads)
1. [Let and Const](#references)
1. [Iterators and Generators](#iterators-and-generators)
1. [Modules](#modules)

**[⬆ back to top](#table-of-contents)**

## Typescript 1.5 Styles

  - [31.1](#31.1) <a name='31.1'></a> This is a collection of links to the various es6 features.

1. [Type Annotations](#ts-type-annotations)
1. [Interfaces](#ts-interfaces)
1. [Classes](#ts-classes)
1. [Modules](#ts-modules)
1. [Generics](#ts-generics)

**[⬆ back to top](#table-of-contents)**


# Typscript Conventions

### General Types

- Không được sử dụng: `Number`, `String`, `Boolean`, `Symbol` and `Object`. Hãy sử dụng: `number`, `string`, `boolean`, and `symbol`.

  > Vì: `Number`, `String`, `Boolean`, `Symbol` and `Object` là kiểu dữ liệu của javascript, `number`, `string`, `boolean`, and `symbol` kiểu dữ liệu của Typescript.

  ```ts
  //bad
  const lastName: String;

  //good
  const lastName: string;
  ```

### Variable and Function

- Hãy sử dụng `camelCase` cho tên biến và function

  ```ts
  //bad
  const FooVar;
  function BarFunc() {}

  //good
  const fooVar;
  function barFunc() {}
  ```

### Type vs Interface

- Sử dụng thay khi bạn muốn có nhiều hơn 1 kiểu dữ liệu

  ```ts
  type Foo = number | { someProperty: number };
  ```

- Sử dụng `interface` khi bạn muốn `extends` hoặc `implements`
  ```ts
  interface Foo {
    foo: string;
  }
  interface FooBar extends Foo {
    bar: string;
  }
  class X implements FooBar {
    foo: string;
    bar: string;
  }
  ```

### Class

- Sử dụng `PascalCase` cho tên class.

  ```ts
  //bad
  class foo {}

  //good
  class Foo {}
  ```

- Sử dụng `camelCase` cho properties và method

  ```ts
  //bad
  class Foo {
    Bar: number;
    Baz() {}
  }

  //good
  class Foo {
    bar: number;
    baz() {}
  }
  ```

### Interface

- Sử dụng `PascalCase` cho name.

  ```ts
  //bad
  interface employee {}

  //good
  interface Employee {}
  ```

- Sử dụng `camelCase` cho properties và method.

  ```ts
  //bad
  interface Employee {
    empcode: number;
    empname: string;
    getsalary: (number) => number;
    getsanagername(number): string;
  }

  //good
  interface Employee {
    empCode: number;
    empName: string;
    getSalary: (number) => number;
    getManagerName(number): string;
  }
  ```

### Array

- Sử dụng foos:Foo[] thay vì foos:Array<Foo>.

  ```ts
  //bad
  const foos: Array<Foo>;
  //good
  const foos: Foo[];
  ```

## Namespace

- Sử dụng `PascalCase` cho name

  ```ts
  //bad
  namespace foo {}

  //good
  namespace Foo {}
  ```

## Enum

- Sử dụng `PascalCase` cho name

  ```ts
  //bad
  enum color {}

  //good
  enum Color {}
  ```

### Filename

- Sử dụng `camelCase` cho tên file.

  ```ts
  //bad
  mycontrol.ts;

  //good
  myControl.ts;
  ```

### Sử dụng `let` và `const`

- Sử dụng `let`, `const` thay cho `var`

  ```ts
  // bad
  var a = 1;
  var b = 2;

  // good
  const a = 1;
  let b = 2;
  ```

### Imports and exports

- Sử dụng `Modules` phải dùng `Imports\Exports`

  ```ts
  // bad
  const myModule = require("./myModule");
  module.exports = myModule.Foo;

  // ok
  import myModule from "./myModule";
  export default myModule.Foo;

  // best
  import { es6 } from "./myModule";
  export default Foo;
  ```

### Destructuring

- Sử dụng object `destructuring` để truy cập và sử dụng multiple properties của một Object.

  ```ts
  // bad
  const getFullName = user => {
    const firstName = user.firstName;
    const lastName = user.lastName;
    return `${firstName} ${lastName}`;
  };

  // good
  const getFullName = user => {
    const { firstName, lastName } = user;
    return `${firstName} ${lastName}`;
  };
  ```

### Overloaded functions

- Đừng viết các hàm overloads riêng biệt chỉ khác nhau ở trong parameter của function. Thay vào đó hãy viêt duy nhất một hàm overloads và với parameter là nhiều nhất

  ```ts
  // bad
  declare function beforeAll(action: () => void, timeout?: number): void;
  declare function beforeAll(
    action: (done: DoneFn) => void,
    timeout?: number
  ): void;

  // good
  declare function beforeAll(
    action: (done: DoneFn) => void,
    timeout?: number
  ): void;
  ```

## Null and Undefined

- Không sử dung với mục đích không rõ gàng

  ```ts
  //bad
  let foo = { x: 123, y: undefined };

  //good
  let foo: { x: number; y?: number } = { x: 123 };
  ```

- Hãy sử dung trả về `Undefined` thay vì `Null`

  ```ts
  //bad
  return null;

  //good
  return undefined;

  //best

  return {
    ...
  }
  ```

* Sử dung `== hoặc !=` để check `Null` và `Undefined` không được sử dụng `=== hoặc !==`

  ```ts
  //bad
  if(myVariable === undefined)
  if(myVariable!== undefined)

  //good
  if(myVariable == undefined)
  if(myVariable!= undefined)
  ```

## Comments

- Hãy tuân thủ `JSDOC` cho `Comments`
  ```ts
  /**
   * Represents a book.
   * @constructor
   * @param {string} title - The title of the book.
   * @param {string} author - The author of the book.
   */
  book = (title: string, author: string) => {};
  ```

### Spaces

- Sử dụng 2 `spaces`, không sử dụng `tabs`

  ```ts
  // bad
  foo = () => {
  ∙∙∙∙let name;
  }

  // bad
  bar = () => {
  ∙let name;
  }

  // good
  baz = () => {
  ∙∙let name;
  }
  ```

## Performance code

- Tối ưu phạm vi của biến

  ```ts
  //bad
  const array1 = ["a", "b", "c"];
  let isChecked = true;

  array1.map(element => {});

  //good
  const array1 = ["a", "b", "c"];
  let isChecked = true;

  array1.map(element => {});
  ```

- Tinh giản các biểu thức toán học.

  ```ts
  //bad
  const total = A * B + A * C + A * D;

  //good
  const total = A * (B + C + D);
  ```

- Sắp xếp thứ tự các điều kiện trong câu lệnh ‘if’ một cách hợp lý

  ```ts
  //bad
  if (user.isLike() === true && isAvartar === true) {
    //something
  }

  //good
  if (isAvartar === true && user.isLike() === true) {
    //something
  }
  ```

- Nên sử dụng toán tử gán kết hợp toán tử số học thay vì sử dụng toán tử toán học và toán tử gán riêng biệt

  ```ts
  let s1 = "";
  let s2 = s1 + "test";

  //good
  let s1 = ''
  let s2 += s1
  ```

- Tuyệt đối không được gọi truy vấn data trong vòng lặp, nếu có thể hãy sử dụng thư viện cho việc truy vấn.
- Example: Typorm
