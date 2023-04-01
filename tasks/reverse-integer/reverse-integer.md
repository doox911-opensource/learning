Given a signed `32-bit` integer `x`, return `x` with its digits reversed. If reversing `x` causes the value to go outside the signed `32-bit` integer range `[-2^31, 2^31-1]`, then return `0`.

**Assume the environment does not allow you to store 64-bit integers (signed or unsigned).**

My solution:
```ts
function reverse(x: number): number {
  const n = x < 0 
    ? -`${Math.abs(x)}`.split('').reverse().join('')
    : +`${x}`.split('').reverse().join('');

  return n > 2147483647 || n < -2147483647 ? 0 : n;
};

// or

function reverse(x: number): number {
  const is_minus = x < 0
  
  const n = +`${Math.abs(x)}`.split('').reverse().join('');

  return n > 2147483647 ? 0 : is_minus ? -n : n;
};
```

ChatGPT 3  solution:
```ts
function reverse(x: number): number {
  let n = 0;

  const sign = x < 0 ? -1 : 1;
  
  x = Math.abs(x);

  while (x > 0) {
    n = n * 10 + (x % 10);
    x = Math.floor(x / 10);
  }

  if (n > 0x7fffffff) {
    return 0;
  }

  return n * sign;
}
```
