# Конструкция try-catch
---

Синтаксис:
```js
try {
	// код
} catch (error) {
	// обработка ошибки
}
```

>В блоке try следует размещать код, который может содержать исключение. Если вдруг при выполнении этого кода возникнет исключительная ситуация, то наш скрипт не рухнет с ошибкой в консоли, а начнет выполнятся код блока catch.

```js
try {
	let data = JSON.parse('{1,2,3,4,5}');
} catch (error) {
	alert('невозможно выполнить операцию разбора JSON');
}

//--------------------------------------------------------------

try {
	saveData('[1,2,3,4,5]');
} catch (error) {
	if (error.name == 'QuotaExceededError') {
		alert('закончилось место в хранилище');
	}
	
	if (error.name == 'SyntaxError') {
		alert('некорректный JSON');
	}
}

//--------------------------------------------------------------

function saveData(json) {
	try {
		let arr = JSON.parse(json);
		
		for (let i = 0; i < arr.length; i++) {
			try {
				localStorage.setItem(i, arr[i]);
			} catch (error) {
				alert('закончилось место в хранилище');
			}
		}
	} catch (error) {
		alert('некорректный JSON');
	}
}
```

----

Пользовательские исключения с помощью `throw new Error('ошибка деления');`.

```js
function div(a, b) {
	if (b !== 0) {
		return a / b;
	} else {
		throw new Error('ошибка деления на ноль');
	}
}

// Перехватываем ошибку
try {
	alert( div(3, 0) );
} catch (error) {
	alert('вы пытаетесь делить на 0, что запрещено');
}
```

>Можно выбрасывать исключения не только типа Error, но и любого встроенного в JavaScript типа ошибки, например, TypeError, SyntaxError, RangeError.

```js
try {
	throw new SyntaxError('текст исключения');
} catch (error) {
	console.log(error.name); // 'SyntaxError'
	console.log(error.message); // 'текст исключения'
}
```

----

Свои типы исключений - в throw передаем объект с ключами name и message

```js
try {
	throw {name: 'MyError', message: 'текст исключения'};
} catch (error) {
	console.log(error.name); // 'MyError'
	console.log(error.message); // 'текст исключения'
}
```

----

Интересный пример.

Пусть при загрузке страницы сервер создает HTML код, в котором хранится название, цена и количество купленного продукта:
```js
<div id="product" data-product="яблоко" data-price="1000" data-amount="5"></div>
```

Давайте сделаем функцию, которая будет принимать ссылку на элемент с продуктом и находить полную стоимость товара (цену умножать на количество):
```js
function getCost(elem) {
	return elem.dataset.price * elem.dataset.amount;
}
```

Найдем стоимость нашего продукта:
```js
let product = document.querySelector('#product');
let cost = getCost(product);

alert(cost);
```

Предположим теперь следующую ситуацию: из-за какого-то сбоя на сервере он прислал нам товар, в котором отсутствует цена или количество (или оба сразу), например, вот так:
```js
<div id="product" data-product="яблоко" data-price="1000"></div>
```

Если теперь попробовать посчитать стоимость товара, то результате на экран выведется NaN. Согласитесь, не очень информативно.
Получается, нам нужно как-то обезопасится от того, что будут отсутствовать нужные нам атрибуты. 
Это можно сделать двумя путями. Первый путь - это сказать, что это нормальное поведение и просто поверять ифами наличие нужных нам атрибутов:
```js
function getCost(elem) {
	if (elem.dataset.price !== undefined && elem.dataset.amount !== undefined) {
		return elem.dataset.price * elem.dataset.amount;
	} else {
		return 0; // вернем что-нибудь, например, 0 или null или false
	}
}
```

Второй вариант - это сказать, что отсутствие атрибута data-price или data-amount - исключительная ситуация. 
В этом случае мы будем выбрасывать исключение:
```js
function getCost(elem) {
	if (elem.dataset.price !== undefined && elem.dataset.amount !== undefined) {
		return elem.dataset.price * elem.dataset.amount;
	} else {
		throw {
			name: 'ProductCostError',
			message: 'отсутствует цена или количество у продукта'
		};
	}
}
```

Какой из двух вариантов здесь уместнее применить - это выбор программиста. 
Он может считать проблему нормальной работой скрипта или исключительной ситуацией.
Пусть мы решили, что ситуация исключительная. 
Тогда код получения стоимости товара будет выглядеть вот так:
```js
let product = document.querySelector('#product');

try {
	let cost = getCost(product);
	alert(cost);
} catch (error) {
	// как-то реагируем на исключение
}
```

----

Пусть к нам откуда-то из внешнего мира приходит JSON с продуктом:

`let json = '{"product": "яблоко", "price": 1000, "amount": 5}'; let product = JSON.parse(json); alert(product.price * product.amount);`

Вы уже знаете, что метод JSON.parse будет выбрасывать исключение, если JSON некорректный. Давайте поймаем это исключение:

`try { let json = '{"product": "яблоко", "price": 1000, "amount": 5}'; let product = JSON.parse(json); alert(product.price * product.amount); } catch (error) { // как-то реагируем на исключение }`

Однако, может быть такое, что сам по себе JSON корректный, но не содержит нужных нам полей, например, нет поля с ценой:

`let json = '{"product": "яблоко", "amount": 5}'; // нет цены`

Давайте скажем, что это тоже исключительная ситуация и будем в таком случае выбрасывать свое пользовательское исключение:

`try { let json = '{"product": "яблоко", "amount": 5}'; let product = JSON.parse(json); if (product.price !== undefined && product.amount !== undefined) { alert(product.price * product.amount); } else { throw { name: 'ProductCostError', message: 'отсутствует цена или количество у продукта' }; } } catch (error) { // как-то реагируем на исключение }`

Теперь блок catch будет получать два типа исключений: либо JSON вообще некорректен, и тогда будет исключение типа `SyntaxError`, либо JSON корректен, но не содержит нужных нам полей, и тогда будет исключение типа `ProductCostError`.

Давайте в блоке catch будем отлавливать эти типы исключений:

`try { let json = '{"product": "яблоко", "amount": 5}'; let product = JSON.parse(json); if (product.price !== undefined && product.amount !== undefined) { alert(product.price * product.amount); } else { throw { name: 'ProductCostError', message: 'отсутствует цена или количество у продукта' }; } } catch (error) { if (error.name == 'SyntaxError') { alert('Некорректный JSON продукта'); } else if (error.name == 'ProductCostError') { alert('У продукта отсутствует цена или количество'); } }`