Необходимо написать функцию, которая первым аргументом принимает отсортированный массив, а вторым - число. Функция должна вернуть массив из двух элементов если их сумма равна второму аргументу, в противном случае функция возвращает пустой массив.

*Использовать один и тот же элемент для получения суммы - запрещено*

```ts
function findFirstSum(arr: number[], sum: number): number[] {

}
```
Тестовые наборы:

```ts
const arr_1 = [-1, 2, 5, 8];     const sum = 7; // Ответ: [-1, 8] или [2, 5]
const arr_2 = [-3, -1, 0, 2, 6]; const sum = 6; // Ответ: [0, 6]
const arr_3 = [2, 4, 5];         const sum = 8; // Ответ: []
const arr_4 = [1];               const sum = 1; // Ответ: []
const arr_5 = [];                const sum = 1; // Ответ: []
```

Самое простое решение(подходит для неотсортированного массива):
```ts
function findArray(arr: number[], sum: number): number[] {
  if (arr.length <= 1) {
    return [];
  }
   
  for(let i = 0; i < arr.length; i++) {
    let j = i + 1;

    for(; j < arr.length; j++) {
      if (arr[i] + arr[j] === sum) {
        return [
          arr[i],
          arr[j]
        ];
      }
    }
  }
  
  return [];
}
```

Самое лучшее решение(только для отсортированного массива):
```ts
function findArray(arr: number[], sum: number): number[] {
  let i = 0;
  let j = arr.length - 1;
  
  while(i < j) {
    const _ = arr[i] + arr[j];
    
    if (_ === sum) {
      return [
        arr[i],
        arr[j]
      ];
    }
    
    if (_ < sum) {
      i++;
    } else {
      j--;
    }
  }
  
  return [];
}
```
