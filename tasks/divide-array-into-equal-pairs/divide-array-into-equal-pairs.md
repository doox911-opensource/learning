Divide Array Into Equal Pairs

You are given an integer array `nums` consisting of `2 * n` integers.

You need to divide nums into `n` pairs such that:

- Each element belongs to exactly one pair.
- The elements present in a pair are equal.

Return `true` if nums can be divided into `n` pairs, otherwise return `false`.

My solution: 

```ts
function divideArray(nums: number[]): boolean {
  if (nums.length % 2 > 0) {
    return false;
  }

  const hash = {};

  let start = 0;
  let end = nums.length - 1;

  while(start < end) {
    hash[nums[start]] = hash[nums[start]] === undefined ? 1 : hash[nums[start]] + 1
    hash[nums[end]]  = hash[nums[end]] === undefined ? 1 : hash[nums[end]] + 1

    start++;
    end--;
  }

  const keys = Object.keys(hash);

  start = 0;
  end = keys.length - 1;

  while(start < end) {
    if (hash[keys[start]] % 2 > 0 || hash[keys[end]] % 2 > 0) {
      return false;
    }

    start++;
    end--;
  }

  return true;
};
```
Another:
```ts
function divideArray(nums: number[]): boolean {
  let len = nums.length;

  if (len % 2 > 0) {
    return false;
  }

  len /= 2;

  const hash = Object.create(null);

  while(nums.length) {
    const e = nums[nums.length - 1];

    hash[e] = hash[e] === undefined ? 1 : hash[e] + 1;

    nums.length--;
  }

  const keys = Object.keys(hash);
  
  if (keys.length > len) return false;

  while(keys.length) {
    const e  = keys[keys.length - 1];

    if (hash[e] % 2 === 1) {
      return false;
    }
    
    keys.length--;
  }

  return true;
};
```
