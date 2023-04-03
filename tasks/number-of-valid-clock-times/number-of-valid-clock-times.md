You are given a string of length `5` called `time`, representing the current time on a digital clock in the format `"hh:mm"`. The earliest possible time is `"00:00"` and the latest possible time is `"23:59"`.

In the string `time`, the digits represented by the `?` symbol are unknown, and must be replaced with a digit from `0` to `9`.

Return an integer `answer`, the number of valid clock times that can be created by replacing every `?` with a digit from `0` to `9`.

My solution:
```ts
function countTime([h1, h2, , m1, m2]: string): number {
  m1 = m1 === '?' ? '6' : '1'
  m2 = m2 === '?' ? '10' : '1'
  
  if (h2 === '?') {
    if (h1 === '?') {
      return 24 * +m1 * +m2;
    } else {
      if (+h1 === 2) {
        return 4 * +m1 * +m2;
      } else {
       return 10 * +m1 * +m2;
      }
    }
  } else if (h1 === '?') {
    if (+h2 > 3) {
      return 2 * +m1 * +m2;
    } else {
      return 3 * +m1 * +m2;
    }
  }

  return +m1 * +m2;
};
```
