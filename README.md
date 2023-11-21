# Алгоритмы

Алгоритмом называется набор инструкций для выполнения некоторой
задачи.

## Содержание:
- [Бинарный поиск](#binarySearch)



### <a id="binarySearch"></a>Бинарный поиск ###

Представим, что у нас есть массив чисел от 0 до 100. Мы хотим найти число 50. Если начать перебор по порядку, то у нас получится 50 шагов, прежде чем найдем нужное число. Такой подход неоптимальный.

Пример линейного поиска:

``` javascript
const createArray = new Array(101).fill(0);
const array = createArray.map((value, index) => index);

for (let i = 0; i < array.length; i++) {
  console.log(`количество итераций: ${i}`); // 50 шагов
  if (array[i] === 50) break
}
```

Так как мы знаем, что в массиве числа от 0 до 100, а ищем мы 50, то более эффективным способом будет использовать бинарный поиск.


Принцип алгоритма:

* Нужно обязательно отсортировать массив, если он еще не отсортирован
* Найти средний индекс массива
* Если текущий элемент массива меньше искомого числа, то исключаем левую половину массива
* Если текущий элемент массива больше искомого числа, то исключаем правую половину массива

Пример бинарного поиска:

``` javascript
const createArray = new Array(101).fill(0);
const array = createArray.map((value, index) => index);

function binarySearch(array, target) {
  let iterations = 0; // Количество итераций
  let start = 0; // Начальный индекс
  let end = array.length; // Конечный индекс
  let mid = null; // Средний индекс

  while(start <= end) {
    iterations++
    // Находим средний индекс массива
    mid = Math.floor((start + end) / 2)
    
    if (array[mid] === target) {
      console.log('iterations:', iterations) // Найдено за 1 шаг
      return mid
    } else if (array[mid] < target) {
      // Если элемент меньше искомого числа, то исключаем левую половину массива
      start = mid + 1;
    } else if (array[mid] > target) {
      // Если элемент больше искомого числа, то исключаем правую половину массива
      end = mid - 1;
    } else {
      return 'Ничего не нашлось:('
    }
  }
}

const result = binarySearch(array, 50);
console.log(result); // 50
```