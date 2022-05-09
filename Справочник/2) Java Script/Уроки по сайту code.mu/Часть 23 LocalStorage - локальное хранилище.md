# LocalStorage - локальное хранилище
----

>LocalStorage - позволяет хранить данные между заходами пользователя на ваш сайт (5-10 мегабайт информации). Данные хранятся в специальном месте браузера под названием локальное хранилище.

>Доступ к данным производится по ключу: вы сохраняете данные с каким-то ключом, а затем можете получить их по этому ключу или удалить.
>При этом разрешено сохранять только строки.

---

Методы работы с данными.

- Метод `setItem` предназначен для сохранения данных. 

Первым параметром он принимает ключ, а вторым - значение:
```js
localStorage.setItem('key', 'hello'); // сохраняем с ключом 'key'
```

- Метод `getItem` предназначен для получения данных.

```js
let str = localStorage.getItem('key'); // получаем данные по ключу
console.log(str); // выведет 'hello'
```

-   `removeItem(key)` – удалить данные с ключом `key`.
-   `clear()` – удалить всё.
-   `key(index)` – получить ключ на заданной позиции.
-   `length` – количество элементов в хранилище.

----

Однократное сохранение.

>Если данные не записаны, то будет null.

Запишем в локальное хранилище момент первого захода пользователя на сайт:
```js
let time = localStorage.getItem('time');

if (time === null) {
	let now = ( new Date() ).getTime();
	localStorage.setItem('time', now);
}
```

----

Перезаписывание данных.

```js
localStorage.setItem('key', 1);
let value = localStorage.getItem('key');
console.log(value); // выведет 1

localStorage.setItem('key', 2);
let value = localStorage.getItem('key');
console.log(value); // выведет 2

localStorage.setItem('key', 3);
let value = localStorage.getItem('key');
console.log(value); // выведет 3
```

----

Хранение массивов и объектов в локальном хранилище (только строки поэтому переводим в формат JSON):
```js
//Сохраним массив
let arr = [1, 2, 3, 4, 5];
localStorage.setItem('arr', JSON.stringify(arr));

//А теперь получим его обратно
let str = localStorage.getItem('arr');
let res = JSON.parse(str);
```

----

