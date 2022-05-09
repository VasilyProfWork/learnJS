# Коллекции Set
---

>Объект `Set` – это особый вид коллекции: «множество» значений (без ключей), где каждое значение может появляться только один раз.

>Позволяет создать массив без дублей.

Основная фишка:
```js
let set = new Set([1, 2, 3, 3, 4, 4, 5]);
console.log(set); // будет [1, 2, 3, 4, 5]
```

----

Свойство `size` - содержит размер коллекции: `set.size`

Метод `has` - проверяет наличие ключа: `set.has(1)`
Метод `delete` - удаляет элемент из коллекции: `set.delete(1)`
Метод `clear` - очищает всю коллекцию: `set.clear()`

---

Перебор коллекций Set циклом:
```js
let set = new Set;

set.add(1);
set.add(2);
set.add(3);

for (let elem of set) {
	console.log(elem);
}
```

---

Преобразование коллекций Set:
```js
let set = new Set([1, 2, 3]);

//Можно преобразовать ее в массив, используя прием с деструктуриацией:
let arr = [...set];

//А можно воспользоваться методом Array.from:
let arr = Array.from(set);
```

---

Преобразование массива в Set: 
```js
let arr = [1, 2, 3];
let set = new Set(arr);
```

---

Быстрое удаление дублей:
```js
let arr = [1, 2, 3, 1, 3, 4];
let res = [...new Set(arr)];

console.log(res); // выведет [1, 2, 3, 4]
```

----

Получение дом элементов без дублей:
```js
<p>aaa</p>
<p>bbb</p>
<p>ccc</p>
<p>ddd</p>
<p>eee</p>

<button>click me</button>

let button = document.querySelector('button');
let elems  = document.querySelectorAll('p');

let set = new Set;

//Давайте теперь по клику на абзац будем добавлять этот абзац в коллекцию:
for (let elem of elems) {
	elem.addEventListener('click', function() {
		set.add(this);
	});
}

//Давайте теперь по клику на кнопку переберем содержимое нашей коллекции и каждому абзацу в конец добавим восклицательный знак:
button.addEventListener('click', function() {
	for (let elem of set) {
		elem.textContent = elem.textContent + '!';
	}
});
```
