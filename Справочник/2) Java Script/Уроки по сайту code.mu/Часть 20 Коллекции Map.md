# Коллекции Map
---

>Map – это коллекция ключ/значение, как и `Object`. Но основное отличие в том, что `Map` позволяет использовать ключи любого типа.

- Создаем коллекцию `let map = new Map;`
- Создаем в качестве ключа массив `let arr1 = [1, 2];`
- Добавляем элемент `map.set(arr1, 'data1');` -`arr1` это ключ `'data1'` это значение
- Получаем наш элемент `map.get(arr1)`

---

##### Полезные свойства и методы.

Свойство `size` - содержит размер коллекции: `map.size`

Метод `has` - проверяет наличие ключа: `map.has(arr1)`
Метод `delete` - удаляет элемент из коллекции: `map.delete(arr1)`
Метод `clear` - очищает всю коллекцию: `map.clear()`
Метод `values` - получаем значения: `let values = map.values()`
Метод `keys` - получаем ключи: `let keys = map.keys()`
Метод `entries` - возвращает набор пар ключ-значение: `let entries = map.entries()`

---

Перебор коллекций Map циклом:
```js
let map = new Map;

let arr1 = [1, 2];
let arr2 = [3, 4];

map.set(arr1, 'data1');
map.set(arr2, 'data2');

for (let elem of map) {
	console.log(elem); // сначала [[1, 2], 'data1'], потом [[3, 4], 'data2']
}

//Можно отделить ключи и значения с помощью деструктуризации:
for (let [key, elem] of map) {
	console.log(key);
	console.log(elem);
}
```

---

Пример использования.

По клику на каждый абзац ему в конец записывался его порядковый номер в списке абзацев:
```js
<p>aaa</p>
<p>bbb</p>
<p>ccc</p>
<p>ddd</p>
<p>eee</p>

let elems = document.querySelectorAll('p');

let map = new Map;

//Заполним нашу коллекцию так, чтобы ключами были наши абзацы, а их значениями - порядковые номера:
let i = 1;
for (let elem of elems) {
	map.set(elem, i++);
}

//Давайте теперь по клику будем добавлять порядковый номер в конец текста абзаца. При этом будем получать этот номер из нашей коллекции:
for (let elem of elems) {
	elem.addEventListener('click', function() {
		this.textContent = this.textContent + map.get(this);
	});
}
```