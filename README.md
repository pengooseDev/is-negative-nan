<div align="center">
  <h2>isNegativeNan</h2>
  <div>Check if a number is negative NaN</div>
  <br />
  <a href="https://www.npmjs.com/package/is-negative-nan">
    <img src="https://img.shields.io/npm/v/is-negative-nan?style=for-the-badge" alt="npm" />
  </a>
  <a href="https://www.npmjs.com/package/is-negative-nan">
    <img src="https://img.shields.io/npm/dt/is-negative-nan?style=for-the-badge" alt="downloads" />
  </a>
</div>

## Installation

Install the package using npm:

```sh
npm install is-negative-nan
```

Or using yarn:

```sh
yarn add is-negative-nan
```

Or using pnpm:

```sh
pnpm add is-negative-nan
```

## Usage

```ts
import { isNegativeNaN } from 'is-negative-nan';

console.log(isNegativeNaN(-NaN)); // true
```

## Why is this useful?

```ts
console.log(NaN === NaN); // false
console.log(-NaN === NaN); // false

NaN; // NaN
-NaN; // NaN

String(NaN); // 'NaN'
String(-NaN); // 'NaN'

Number.isNaN(NaN); // true
Number.isNaN(-NaN); // true

Object.is(NaN, NaN); // true
Object.is(-NaN, NaN); // true
Object.is(-NaN, -NaN); // true
Object.is(NaN, -NaN); // true
```

## How it works?

isNegativeNaN converts the number to a `Float64Array` and then to a `Uint32Array`. It then checks if the number is negative by **`checking the 31st bit`** of the Uint32Array.

```ts
export function isNegativeNaN(val: number) {
  if (!Number.isNaN(val)) return false;
  const f64 = new Float64Array(1);
  f64[0] = val;
  const u32 = new Uint32Array(f64.buffer);
  const isNegative = u32[1] >>> 31 === 1;

  return isNegative;
}
```
