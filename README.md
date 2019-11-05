#Typscript Conventions
###General Types

- Không được sử dụng: `Number`, `String`, `Boolean`, `Symbol` and `Object`. Hãy sử dụng: `number`, `string`, `boolean`, and `symbol`.

  > Vì: `Number`, `String`, `Boolean`, `Symbol` and `Object` là kiểu dữ liệu của javascript, `number`, `string`, `boolean`, and `symbol` kiểu dữ liệu của Typescript.

  ```ts
  //bad
  const lastName: String;

  //good
  const lastName: string;
  ```

###Variable and Function

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

## Quotes

- Hãy sử dụng nháy đơn `'` thay vì nháy đôi `"`

  ```ts
  //bad
  const test = "test";

  //good
  const test = "test";
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

### Sử dụng dấu chấm `;`

- Hãy sử dụng `;` cho phân biệt Variables

  ```ts
  // bad
  const luke = {};
  const leia = {};

  // good
  const luke = {};
  const leia = {};
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

- Sử dụng toán tử tăng/giảm một cách hợp lý

  ```ts
  //bad
  count++;
  count--;

  //bad
  ++count;
  --count;
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
