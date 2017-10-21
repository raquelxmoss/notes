# DEV273x Introduction to TypeScript 2

## Module 1

- Introduction and set up. Seemed a bit like an ad for how great Typescript is. Says it solves _all_ the problems with Javascript (lol). Mostly no new information for me here, as I have already used Typescript.

## Module 2

Declaring variables: 

```typescript
let thing : string = "hello";
const age : number = 27;
```

 In JavaScript, the type of the variable is given from the value the variable holds. If the value changes, the type of the variable also changes to fit the new value. It is therefore considered a *dynamic type*

In TypeScript, if a variable is not explicitly assigned a type when it is defined, then the type is inferred from the first assignment or the initialization of the variable and then it is then considered a strongly typed variable with the inferred type. For example:

```typescript
let y = 10; // it is inferred that y is a number
y = "hello" // compiler error! You cannot assign a string to a number.
```

⚠️[ `let` is scoped to your block, while `var` is not](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let). E.g.

```typescript
function varTest() {
  var x = 1;
  if (true) {
    var x = 2;  // same variable!
    console.log(x);  // 2
  }
  console.log(x);  // 2
}

function letTest() {
  let x = 1;
  if (true) {
    let x = 2;  // different variable
    console.log(x);  // 2
  }
  console.log(x);  // 1
}
```



### Basic/Primitive Types (as at Typescript 2.3)

- boolean

- number

  - can be a decimal, hex, binary, or octal

- string

  - includes template strings

- array

  - ```typescript
    let list: number[] = [1, 2, 3];
    or
    let list: Array<number> = [1, 2, 3];
    ```

- tuple

  - A tuple is an array where it has a fixed number of elements, and you know what the types will be for them.

  - ```typescript
    // Declare a tuple type
    let x: [string, number];
    // Initialize it
    x = ["hello", 10]; // OK
    // Initialize it incorrectly
    x = [10, "hello"]; // Error
    ```

- enum

  - An enum is a nice way to kind of have an array (e.g. positions are important), but with the items also being named.

  - You can manually set the values of an enum, or they are inferred from their positions

  - ```typescript
    enum Fruits { Oranges, Apples, Bananas }
    let dessert : Fruit = Fruits.Apples
    OR
    let dessert : Fruit = Fruits[1]

    // manually set values
    enum Fruits { Oranges = 1, Apples = 2, Bananas = 3 }
    ```

- null

- undefined

- any

- void

### Complex Types (as at Typescript 2.3)

- class
- interface

### Type assertions

This is when you tell the compiler "Hey, I know what the type of this is, okay?". Useful when you have `any` lying around. It's sometimes known as typecasting. When you're working with JSX, you can only use the `as` style.

```typescript
let myThing : any = "string";

let myThingLength : number = (<string>myThing).length
OR
let myThingLength : number = (myThing as string).length
```

### Interfaces

Interfaces allow us to Duck Type in Typescript — they give a name to a set of values/attributes, and define contracts.

⚠️ In the example below, we can pass an object with more key/value pairs, but the compiler only checks that we satisfy the _at least_ requirement defined in the function

```typescript
function printLabel(labelledObj : { label: string }) {
    console.log(labelledObj.label);
}

let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```

Now we can re-write this, but using an interface to describe the required properties

```typescript
interface LabelledThing = {
    label : string;
}

function printLabel(labelledObj : LabelledThing) {
    console.log(labelledObj.label);
}
```

You can denote **optional** properties with a `?`

```typescript
interface TShirt = {
    color? : string;
  	size? : string;
}
```

Make **readonly** properties happen with a `readonly`. These properties can only be set once, and not changed.

```typescript
interface Point = {
  readonly x : number;
  readonly y : number;
}

let point_1 : Point = { x: 10, y: 10 }
point_1.x = 5; // this errors!
```

You can make a readonly array! `ReadonlyArray<T>` — works the same as `Array<T>`, but now your array is not modifiable…unless you typecast it.



### Class Types

Implementing an interface

```typescript
interface Yak {
  shaved: Boolean;
  shave(tool: string);
}

class HairyYak implements Yak {
  shaved: Boolean;
  shave(tool: string) {
    this.shaved = true;
  }
  constructor(shaved: Boolean) {}
}
```



### Function Types

```typescript
interface ReducerFunction {
  (state: AppState) : AppState
}

// using it
const countReducer : ReducerFunction = function (state) {
  return { count: state.count + 1 }
}
// You don't need to annotate the types, because they'll already be checked by the interface
```



### Indexable Types

TODO: I don't really know what this is about, needs further explanation. The course didn't do a good job of explaining it to me, so I'll need to seek out more examples.

```typescript
interface ArrayOfStrings {
  [index: nuber]: string;
}

const fruits : ArrayOfStrings = ["apples", "bananas"];
const favourites : string = fruits[1];
```



### Classes

- methods are public by default, but you can mark it as explicit with a `public`

  ```typescript
  class Phone {
    public color: string;
    public ring(ringtone: string) {
      return `${ringtone}`;
    }
  }
  ```

- Similarly, you can mark things as private.

  ```typescript
  class House {
    private cost : number;
  }
  ```

- Protected members can be accessed by instances of the _deriving_ class (subclass)

  ```typescript
  class Person {
    protected name : string;
    constructor(name: string) { this.name = name; }
  }

  class Celebrity extends Person {
    private irdNumer : number;

    constructor(name: string, irdNumber: string) {
      super(name);
  	this.irdNumber = irdNumber;
    }
  }
  ```

  ​

