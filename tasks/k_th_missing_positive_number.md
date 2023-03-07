Source: https://leetcode.com/problems/kth-missing-positive-number/

My solution:
```ts
function findKthPositive(arr: number[], k: number): number {
    const last_item = arr[arr.length - 1];
    
    const a = [];
    
    for(let i = 0; i < last_item; i++) {
        const item = i + 1;
        
        if (!arr.includes(item)) {
            a.push(item);
        }
    }

    return a.length >= k ? a[k -1] : last_item + k - a.length
};
```

In my opinion, the best [solution](https://leetcode.com/problems/kth-missing-positive-number/solutions/2113768/javascript-4-methods-set-array-bucket-binary-search/):
```ts
function findKthPositive (arr, k) {
 let l = 0, r = arr.length;
 
 while (l<r) {
   let mid = l + Math.floor((r-l)/2);
        
   if(arr[mid]-mid-1 < k) { l = mid+1 }
   else { r = mid };
 }

 return k+l;  // arr[l-1]+k-(arr[l-1]-(l-1)-1)
};
```
