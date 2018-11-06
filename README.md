# really-lang

> The Really Programming Language

The general purpose programming language you will ever need to learn and use. Heavily inspired by C, JavaScript, Rust, Kotlin, Dart, and any other programming languages you might use these days.

## Features

1. No `Null`, use `Option` type for better error handling.
2. Everything is immutable by default, use `mut` keyword for mutable variables.
3. Statically typed programming language.
4. Single threaded by default.

## TO-DO

1. To support compilation to Web Assembly.
2. To support multithreading.

## Syntax

### Comments

```ts
/**
 * Multi-line
 * comments
 */

/** Single line comment only */
```

### Variables

```ts
/** Type inferred */
let typeInferred = '100'; /** string */

/** Unknown type */
let unknownType; /** unknown */
unknownType = '100'; /** unknown -> str */

/** Compile Error! Unknown type should be temporary. */
let unknownType; /** unknown */

/** Declaration with defined type */
let definedType: str = '100';
```

1. Mutable
   
   ```rs
   /** Mutable variable */
   let mut mutableVar = '100';
   mutableVar = '2';

   /** Mutable variable is mutable by value, not by type */
   let mut mutableVar = '100'; /** str */
   mutableVar = 10; /** Compile error! */
   ```

2. Immutable

    ```ts
    /** All variables are immutable by default */
    let immutableByDefault = '10'; /** immutable string */
    immutableByDefault = '1'; /** Compile error! */
    ```

3. Reference or borrowing

    ```rs
    let val = '10';
    let borrowVal = &val; /** &str */
    let mut mutableBorrow = &mut val; /** &mut str */

    borrowVal = '1'; /** Compile error! */
    mutableBorrow = '1'; /** `val` is now of value `1` */
    ```

4. Dereferencing

    ```rs
    let val = '10';
    let borrowVal = &val; /** `borrowVal` is just a reference to `val` */
    let derefBorrowVal = *borrowVal; /** De-ref borrowed `val` */
    ```

### Primitives

1. Arrays
   
   ```ts
   let array: Array<num> = [1, 1, 1];
   let mixedTypeArray: Array<num|str> = [1, '1', 0];
   let inferredTypeArray: [1, '1', true]; /** Array<str|num|bool> */
   ```

2. Objects

    ```ts
    let object = { haha: 1, lol: 'haha' };
    ```

3. Strings

    ```ts
    let characterString = '1';
    let longString = 'Hello, World!';
    let emojiString: str = '👍';
    ```

4. Boolean

    ```ts
    let boolean: bool = true;
    let numberBoolean: bool = 0;
    ```

5. Numbers

    ```ts
    let integer: num = 1;
    let float: num = 1.1;
    ```

6. Options

    ```rs
    let option: Option<string> = Some('1');
    let none: Option<string> = None; /** `None` is an option type */
    let inferredOption = Some(1);
    ```

7. Symbols

    ```ts
    let symbol: Symbol = Symbol('1');
    let inferredSymbol = Symbol(1);

    Symbol(1) != Symbol(1) /** Symbol is always unique */
    ```

8. Unknown

    ```ts
    let unknownVar; /** Unknown type variable is temporary */
    unknownVar = '1'; /** `unknownVar` is now of type `str` */

    let permanentUnknown; /** Compile Error! */
    ```

### Regex

```ts
let regexp = /[a-z]/gi;
let regexp2: RegExp = /[a-z0-9]/;
```

### Ranges

```py
let exclusiveRange = [0..2]; /** [0, 1] */
let inclusiveRange = [0...2]; /** [0, 1, 2] */

for (let i in 0...2) {
  print(i);
}

/**
 * Output:
 * 0
 * 1
 * 2
 */
```

### Collections

1. Map

    ```ts
    let map = Map { '1'=>1, '2'=>2 };

    let map: Map<str, num>;
    map.set('1', 1);
    map.del('1');
    map.has('1');
    map.keys(); /** Iterable<num> */
    map.vals(); /** Iterable<num> */
    ```

2. Set

    ```ts
    let set = Set { 1, 2 };

    let set: Set<num>;
    set.add(1);
    set.add(2);
    set.del(2);
    set.has(1);
    set.keys(); /** Iterable<num> */
    set.vals(); /** Iterable<num> */
    ```

### Operators

1. Arithmetic

    ```ts
    a + a
    a - b
    a * b
    a / b
    a % b
    ```

2. Bitwise

    ```ts
    a & b
    a | b
    a ^ b
    ~a
    a >> b
    a >>> b
    a << b
    a <<< b
    ```

3. Logical

    ```ts
    a && b
    a || b
    !a
    ```

### Comparison

```ts
a == b
a != b
a > b
a < b
a >= b
a <= b
a is b
is a
not b
```

### If-Else

```ts
let a = if (true) {
  'b'
} else {
  'c'
};

if (true) {
  'a'
} else if (a > b) {
  'b'
} else {
  'c'
}
```

### Destructuring

```ts
let [a, b] = [1, '1'];
let { a, b } = { a: 1, b: '1' };
```

### Try-Catch-Finally

```ts
try {
  ...
} catch (e is Option) {
  ...
} finally {
  ...
}
```

### Functions/ Closures

```ts
fn a() {
  ...
}

async fn b() { ... }

let a = () => { ... };
let a = () => {
  'a'
};

let b = '1';
let c = () => {
  b
};
```

### Futures

1. Future

    ```ts
    let a = Future('1');
    let a: Future<bool> = Future(true);

    a.then(...).catch(...);
    ```

2. Async-Await

    ```ts
    let a = async () => { ... };
    let a: Future<bool> = async () => { await ... };

    async () => { await a; };
    ```

### Loops

1. While

    ```ts
    while (true) {
      ...
    }
    ```

2. Do-While

    ```ts
    do {
      ...
    } while (true);
    ```

### Iterators

```ts
let a = [1, 2, 3];
for (let i of a) {
  ...
}

let a = [Future(1), Future(2), Future(true)];
for await (let i of a) {
  ...
}
```

### Pattern Matching

```ts
let a = Some(1);
match (a) {
  Some(n) => { ... },
  None => { ... },
}

let b = true;
match (b) {
  is Future<n> => { ... },
  is str => { ... },
  not bool => { ... },
  Some(n) => { ... },
  _ => { ... }
}

let c = match (b) {
  ...
};
```

### Modules

1. Import

    ```ts
    /** Only public fields, methods can be imported */
    import a from 'a.rl';
    import a, b, c from 'b.rl';

    import a as b from 'a.rl';
    import a as b, b as c from 'a.rl';

    import 'a.rl';
    import 'a.rl', 'b.rl';
    ```

2. Export

    ```ts
    /** Fields, methods are private by default, unless being exported */
    fn a() { ... }
    fn b() { ... }

    export a;
    ```

    ```ts
    /** Exported fields and methods are public by default */
    fn a() { ... }
    fn b() { ... }

    export a, b;
    ```

### Optional chaining

```ts
let a = {
  a: [
    {
      b: [1, true]
    }
  ]
};

a?.b?.c?.0
a?.c?[0]?.['c']
```

## Type Syntax

### Basic Types

1. Boolean `bool`
2. String `str`
3. Number `num`
4. RegExp `RegExp`
5. Symbol `Symbol`
6. Array<T> `Array<num|bool>`
7. Object `{}`
8. Iterable<T> `Iterable<num>`
9.  Map<T, U> `Map<str, num>`
10. Set<T> `Set<num>`
11. Option<T> `Option<str>`
12. Future<T> `Future<bool>`
13. Unknown `unknown`

### Optional Types

```ts
let a?: string;

a is None;
```

### Function Types

```ts
interface FnA {
  (): bool;
}

fn a(): FnA {
  true
}
```

### Generics

```ts
interface Result<T, U> {
  data?: T;
  error?: U;
}

let a: Result<str, str>;
```

### Unions

```ts
type TypeA = str | num;
interface IB<T> {
  data: T;
}

let a: IB<TypeA>;
```