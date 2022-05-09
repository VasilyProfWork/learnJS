# Контекст this
---

> `this` указывает на элемент в котором произошло событие

При каждом нажатие на кнопку, `this` будет содержать ссылку кнопки, в которой произошло событие:
```js
<input id="button1" type="submit" value="text1">
<input id="button2" type="submit" value="text2">
<input id="button3" type="submit" value="text3">

let button1 = document.querySelector('#button1');
let button2 = document.querySelector('#button2');
let button3 = document.querySelector('#button3');

button1.addEventListener('click', func);
button2.addEventListener('click', func);
button3.addEventListener('click', func);

function func() {
    console.log(this.value = '!!!');
}
```

----

Метод `call`

Принудительное привязывание контекста через метод `call`, без `addEventListener`:
```js
let elem = document.querySelector('#elem');

function func(param1, param2) {
	console.log(this.value + param1 + param2);
}
func.call(elem, param1, param2); // Привязываем к elem с определенными параметрами
```

---

Метод `apply`

>Он работает практически так же, как и метод `call`. Разница заключается в том, что в `apply` параметры передаются в виде массива, а не перечисляются через запятую. 

Привязывание контекста через метод `apply`:
```js
func.apply(elem, [param1, param2]);
```

---

Метод `bind`

>Позволяет навсегда привязать контекст к функции. Своим результатом этот метод возвращает новую функцию, внутри которой `this` будет иметь жестко заданное значение. `func = func.bind(elem);`

```js
let elem = document.getElementById('elem');

function func(param1, param2) {
	console.log(this.value + param1 + param2);
}

let newFunc = func.bind(elem);
newFunc('1', '2'); // выведет 'text12'
```

----

Примерчик

Сделаем так, чтобы по клику на любой абзац алертом выводился текст этого абзаца:
```js
<p>text1</p>
<p>text2</p>
<p>text3</p>

let elems = document.querySelectorAll('p');
for (let elem of elems) {
	elem.addEventListener('click', function() {
		alert(this.innerHTML);
	});
}
```