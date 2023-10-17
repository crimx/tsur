# [tsur](https://github.com/crimx/tsur)

<p align="center">
  <img width="200" src="https://raw.githubusercontent.com/crimx/tsur/main/assets/tsur.svg">
</p>

[![Docs](https://img.shields.io/badge/Docs-read-%23fdf9f5)](https://crimx.github.io/tsur)
[![Build Status](https://img.shields.io/github/actions/workflow/status/crimx/tsur/build.yml)](https://github.com/crimx/tsur/actions/workflows/build.yml)
[![npm-version](https://img.shields.io/npm/v/tsur.svg)](https://www.npmjs.com/package/tsur)
[![Coverage Status](https://img.shields.io/coveralls/github/crimx/tsur/main)](https://coveralls.io/github/crimx/tsur?branch=main)

TypeScript goodies inspired by Rust.

## Install

```
npm add tsur
```

## Usage

### Option

```ts
import { Option, Some, None } from "tsur";

const maybeNumber = Option.Some(42);

if (maybeNumber.isSome()) {
  console.log(maybeNumber.unwrap()); // 42
} else {
  console.log("There is no number");
}

const maybeString = Option.None;

if (maybeString.isSome()) {
  console.log(maybeString.unwrap());
} else {
  console.log("There is no string"); // "There is no string"
}
```

### Result

```ts
import { Result, Ok, Err } from "tsur";

function divide(a: number, b: number): Result<number, string> {
  if (b === 0) {
    return Err("Cannot divide by zero");
  }
  return Ok(a / b);
}

const result = divide(10, 2);

if (result.isOk()) {
  console.log(result.unwrap()); // 5
} else {
  console.log(result.unwrapErr()); // "Cannot divide by zero"
}
```

### Array

Many useful array methods are added:

```ts
import { filterMap, Some, None } from "tsur";

const arr = [1, 2, 3, 4, 5];

const result = filterMap(arr, x => (x % 2 === 0 ? Some(x * 2) : None));

console.log(result); // [4, 8]
```

Or you can patch them to the native array:

```ts
import "tsur/patches/array";

const arr = [1, 2, 3, 4, 5];

const result = arr.filterMap(x => (x % 2 === 0 ? Some(x * 2) : None));

console.log(result); // [4, 8]
```

See [docs](https://crimx.github.io/tsur) for more details.

## License

MIT @ [CRIMX](https://github.com/crimx)
