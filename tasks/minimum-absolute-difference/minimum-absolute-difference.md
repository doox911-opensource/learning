Given an array of distinct integers `arr`, find all pairs of elements with the minimum absolute difference of any two elements.

Return a list of pairs in ascending order(with respect to pairs), each pair `[a, b]` follows

- `a`, `b` are from arr
- `a` < `b`
- `b` - `a` equals to the minimum absolute difference of any two elements in arr

ChatGPT 3:

```ts
function minimumAbsDifference(arr: number[]): number[][] {
  function quickSort(arr: number[], left: number, right: number) {
    if (left < right) {
      const pivotIndex = partition(arr, left, right);

      quickSort(arr, left, pivotIndex - 1);
      quickSort(arr, pivotIndex + 1, right);
    }
  }

  function partition(arr: number[], left: number, right: number): number {
    const pivot = arr[right];

    let i = left - 1;

    for (let j = left; j < right; j++) {
      if (arr[j] < pivot) {
        i++;

        swap(arr, i, j);
      }
    }

    swap(arr, i + 1, right);

    return i + 1;
  }

  function swap(arr: number[], i: number, j: number) {
    const temp = arr[i];

    arr[i] = arr[j];
    arr[j] = temp;
  }

  quickSort(arr, 0, arr.length - 1);

  const res: number[][] = [];
  let minDiff = Infinity;
  
  const map: Map<number, number[][]> = new Map();

  for (let i = 1; i < arr.length; i++) {
    const diff = arr[i] - arr[i - 1];

    if (diff < minDiff) {
      minDiff = diff;
      
      map.clear();
      map.set(diff, [[arr[i - 1], arr[i]]]);
    } else if (diff === minDiff) {
      const pairs = map.get(diff) || [];
      
      pairs.push([arr[i - 1], arr[i]]);
      
      map.set(diff, pairs);
    }
  }

  return Array.from(map.values()).flat();
}
```

My solution:

```ts
function minimumAbsDifference(arr: number[]): number[][] {
  const hash = {};

  let min = Infinity;

  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      const diff = Math.abs(arr[i] - arr[j]);

      if (min > diff) {
        min = diff;
      }

      if (min === diff) {
        const _ = arr[i] <= arr[j]
          ? [arr[i], arr[j]]
          : [arr[j], arr[i]];

        hash[diff]
          ? hash[diff].push(_)
          : hash[diff] = [_];
      }
    }
  }

  return hash[min].sort((a, b) => a[0] + a[1] >= b[0] + b[1] ? 1 : -1);
}
```
