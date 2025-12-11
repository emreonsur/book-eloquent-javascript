# Eloquent JavaScript Fourth Edition
# by Marijn Haverbeke
# Personal Notes

**Reader:** Emre Önsür

## What is JavaScript?

Javascript was introduced in 1995 as a way to add programs to web pages in the *Netscape Navigator Browser*. It has made modern web applications possible—that is, applications with which you can interact directly without doing a page reload for every action.

Javascript has almost nothing to do with the programming language *Java*. The name was inspired by marketing considerations. When JavaScript was being introduced, Java was gaining popularity, so that someone thought it was a good idea to try to ride along on this success.

After its adoption outside of Netscape, a standart document was written to describe the way the JavaScript language should work so that the various pieces of software that claimed to support JavaScript could make sure they actually provided the same language. The Ecma International organization conducted the standardization, and this is called the **ECMAScript standart**. ECMAScript and JavaScript can be used interchangeably.

## Values

In a JavaScript environment, chunks of bits that represent pieces of information are called *values*. Some values are numbers, some values are pieces of text, some values are functions, and so on.

## The Atomic Elements of JavaScript

In JavaScript, the **atomic elements** are the smallest, indivisible pieces you use to build *everything else*.

There are two core atomic elements in JavaScript:

- **Simple (primitive) value types**
- **Operators**

### Numbers

JavaScript `Number` type is stored in 64 bits and follows the [IEEE-754](https://en.wikipedia.org/wiki/IEEE_754). Consuquently, whole numbers are represented by 53 of those bits.

Therefore, the **range_ of whole numbers** that can be represented with the `Number` type is **[-9_007_199_254_740_991, +9_007_199_254_740_991]**.

A `Number` value can be written in several ways:

- As an integer: `23`
- As a fractional number using a dot: `9.81`
- Using scientific notation: `2.998e2`

> Calculations with integers that are in the aforementioned range are guaranteed to always be precise. However, calculations with fractional numbers are generally not.

```javascript
console.log(0.1 + 0.2);
```

#### Arithmetic Operators

```javascript
console.log(20 + 10);
console.log(20 - 10);
console.log(20 * 10);
console.log(20 / 10);
console.log(10 % 3);
```

#### Special Numbers

There are three special values that are considered numbers but don't behave like normal numbers:

- `Infinity`
- `-Infinity`
- `NaN` — which stands for "not a number"

For IEEE-754 64-bit floating point numbers (e.g. JS `Number`), x as a non-zero value:

- If `x > 0`, then `x / 0` is `Infinity`
- If `x < 0`, then `x / 0` is `-Infinity`
- `0 / 0` is `NaN`

For being JS-specific:

```javascript
console.log(3 / 0); // Infinity
console.log(-3 / 0); // -Infinity
console.log(3 / -0); // -Infinity
console.log(-3 / -0); // Infinity
console.log(0 / 0); // NaN
console.log(-0 / 0); // NaN
console.log(0 / -0); // NaN
console.log(-0 / -0); // NaN
console.log(Infinity + Infinity); // Infinity
console.log(Infinity - Infinity); // Nan
console.log(Infinity * Infinity); // Infinity
console.log(Infinity / Infinity); // NaN
console.log(Infinity % Infinity); // NaN
```

### Strings

> Strings are written by enclosing their content in quotes

```javascript
console.log("Hello, World!");
console.log('Hello, World!');
console.log(`Hello, World!`);
```

> Newlines can be included in a string with backticks

```javascript
console.log(`Line 1
Line 2`);
```

> Characters can be escaped inside a quoted text using a backslash (`\`).

```javascript
console.log("Line 1\nLine 2");
console.log("Line 3\nLine 4");
console.log(`Line 5\nLine 6`);
```

> Escaping backslash

```javascript
console.log('A newline can be expressed with "\\n"');
```

> `+` operator can be used to *concatenate* two strings together.

```javascript
console.log("Hello" + " " + "World!");
```

Strings written with single or double quotes behave very much the same — the only difference lies in which type of quote you need to escape inside of them.

> Single quotes (`'`) can be written directly in a double-quoted string — without escaping.

```javascript
console.log("This is a man's world.");
```

> Double quotes (`"`) can be written directly in a single-quoted string — without escaping.

```javascript
console.log('My name is "Emre"');
```

Backtick-quoted strings are usually called *template literals* and can do a few more tricks apart from being able to span newlines.

> Backtick-quoted strings can embed values.

```javascript
console.log(`Half of 100 is ${100 / 2}.`);
```

### Unary Operators

> `typeof` operator produces a string value naming the type of the value it receives as an argument.

```javascript
console.log(typeof 4.5);
console.log(typeof "Emre");
```

> Unary `-` operator produces the value of a number with the opposite sign.

```javascript
console.log(-4);
console.log(-(-4));
```

### Boolean Values

JavaScript's *Boolean* type has only two values as `true` and `false`.

#### Comparison

`<` (less than) and `>` (greater than) operators produce Boolean values.

> On numbers, these operators make simple comparisons.

```javascript
console.log(2 < 3);
console.log(2 > 3);
```

> Strings can be also compared in the same way. When two strings are compared, JavaScript goes over the characters  from left to right, comparing the Unicode codes one by one.

```javascript
console.log("A" < "a");
console.log("Anastasia" > "Natasha");
```

Other similar operators are:

- >=
- <=
- ==
- !=

> There is only one value in JavaScript that is not equal to itself, and that is the value `NaN`.

```javascript
console.log(NaN == NaN); // false
```

#### Logical Operators

JavaScript supports three logical operators:

- and (``&&`)
- or (`||`)
- not (`!`)

> The `&&` operator represents logical *and*. It is a binary operator, and its result is `true` only if both the values given to it are `true`.

```javascript
console.log(true && false); // false
console.log(true && true); // true
```

> The `||` operator denotes logical *or*. It is also a binary operator, and it produces `true` if either of the values given to it is `true`.

```javascript
console.log(false && true); // true
console.log(false && false); // false
```

> The `!` operator denotes logical *not*. It is a unary prefix operator, and it produces the logical opposite of the value given to it.
> `!true` produces `false`
> `!false` produces `true`

```javascript
console.log(!true);
console.log(!false);
```

The *conditional* operator (the ternary operator) uses the value to the left of the question mark to decide which of the two other values to produce.

```javascript
console.log(true ? 1 : 2); // 1
console.log(false ? 1 : 2); // 2
```

### Empty Values

Two special values, `null` and `undefined`, are used to denote the absence of a *meaningful* value. They are themselves values, but carry no information. They can be treated as interchangeable.

### Automatic Type Conversion

JavaScript goes out of its way to accept almost any program given to it, even programs that do odd things.

When an operator is applied to the "wrong" type of value, JavaScript will quietly convert that value to the type it needs, using a set of rules that often aren't what you want or expect. This is called *type coercion*.

> The `null` below becomes `0`.

```javascript
console.log(8 * null); // 0
```

> `"5"` below becomes `5` (from string to number).

```javascript
console.log("5" - 1); // 4
```

> `+` operator below tries string concatenation before numeric addition, so `1` becomes `"1"` (from number to string).

```javascript
console.log("5" + 1);
```

> `"five"` below is to become a number, and when something that doesn't map to a number in an obvious way (such as `"five"` or `undefined`) is converted to a number, it becomes `NaN`. Therefore, Further arithmetic operations on `NaN` keep producing `NaN`.

```javascript
console.log("five" * 2); // NaN
```

> When comparing values of different types, in most cases, JavaScript tries to convert one of the values to the other value's type.

```javascript
console.log(false == 0); // true
```

> In addition to above, however, when `null` and `undefined` occurs on either side the `==` operator, it produces `true` only if both sides are either `null` or `undefined`.

```javascript
console.log(null == undefined); // true
console.log(null == 0); // false
```

> So, recall that `null` below becomes `0` because of the `*` operator.

```javascript
console.log(8 * null); // 0
```

> But, the `null` below is not treated as `0` and the `==` operator produces `false` since when `null` or `undefined` occurs on either side of the `==` operator, it produces true only if both sides are either `null` or `undefined`.

```javascript
console.log(null == 0); // false
```

**When any automatic type conversions are not wanted to happen, there are two additional operators:**

- `===`
- `!==`

```javascript
console.log(0 == false); // true
console.log(0 === false); // false
console.log(0 != false); // false
console.log(0 !== false); // true
```

#### Short-Circuiting of Logical Operators

For non-Boolean values, the logical operators `&&` and `||` first convert the left operand to Boolean type in order to decide what to do, but depending on the operator and the result of that conversion, they return either the *original* left-hand value or the right-hand value.

> The `||` operator returns the value of the left operand when that can be converted to `true` and returns the value of the right operand otherwise.

```javascript
console.log(null || "Emre"); // Emre
console.log("Elif" || "Emre"); // Elif
```

This functionality can be used for getting a default value. If we have a value that might be empty, putting `||` with a replacement value after it produces that replacement value when the initial value is converted to `false`.

The values below count as false according to the rules for converting strings and numbers to Boolean values:

- 0
- NaN
- The empty string (`""`)

```javascript
console.log(0 || 1); // Outputs: 1
console.log(NaN || 42); // Outputs: 42
console.log("" || "default"); // Outputs: default
console.log(null || "fallback"); // Outputs: fallback
console.log(undefined || true); // Outputs: true
console.log(false || "yes"); // Outputs: yes
```

> The `??` operator resembles `||` but returns the value on the right only if the one on the left is `undefined` or `null`.

```javascript
console.log(0 ?? 1); // Outputs: 0
console.log(NaN ?? 42); // Outputs: NaN
console.log("" ?? "default"); // Outputs: ""
console.log(null ?? "fallback"); // Outputs: fallback
console.log(undefined ?? true); // Outputs: true
console.log(false ?? "yes"); // Outputs: yes
```

> The `&&` operator works similarly to the `||` but the other way around. It produces the original left-hand value when it is a *falsy* value, and otherwise it produces the value of the right operand.

```javascript
console.log(1 && 0); // -> 0
console.log(0 && 1); // -> 0
console.log(NaN && 42); // -> NaN
console.log("" && "default"); // -> "" (empty string)
console.log("Emre" && "Elif"); // -> "Elif"
console.log(null && "fallback"); // -> null
console.log(undefined && true); // -> undefined
console.log(false && "yes"); // -> false
```

## Program Structure

### Expressions and Statements

A fragment of code that produces a value is called an *expression*.

If an expression corresponds to a sentence fragment, a JavaScript *statement* corresponds to a full sentence. A program is a list of statements.

The simplest kind of statement is an expression with a semicolon after it: `1;`, `!false;`

### Bindings / Variables

`let` keyword is used to define a binding.

```javascript
let a = 5 * 5;
console.log(a + 10);
```

Accessing the value of a binding defined without a value yields the value `undefined`.

```javascript
let a;
console.log(a); // undefined
```

