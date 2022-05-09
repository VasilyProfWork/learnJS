# Введение в DOM
---

##### Получение элемента

Метод `querySelector` - всегда получает только один элемент - первый, попавший под указанный селектор.
Метод `querySelectorAll` получает все элементы в виде массива.

```js
<input class="elem" id="elemId">
let elem = document.querySelector('.elem'); //Получаем элемент input по классу
let elemTwo = document.querySelector('#elemId'); // Получаем элемент по id
let elemThree = document.querySelector('input'); // Получаем элемент по тегу
```

Другие полезные методы поиска:
```js
let elem = document.getElementsByClassName('elem'); //Поиск по классу
let elemTwo = document.getElementById('elemId'); // поиск по id
let elemThree = document.getElementsByTagName('input'); //поиск по тегу
```

---

##### Обработичики события

>Специальный метод `addEventListener`, первым параметром принимающий название события (клик на кнопку имеет название `click`), а вторым параметром - функцию-коллбэк, выполняющуюся при возникновении этого события.

>Названия события:
>- `click` - нажатие на элемент
>- `mouseover` - наведение курсора на элемент
>- `mouseout` - уход курсора с элемента
>- `focus` - ловим момент получения фокуса в инпуте
>- `blur` - ловим момент при потери фокуса
>- `change` - возникает в полях ввода при их изменениях
>- `input` - возникает каждый раз при вводе нового символа в инпут или textarea

Пример:
```js
let buttons = document.querySelectorAll('.button');

buttons.addEventListener('click', function() {
	alert('!!!');
});
```

К одному элементу можно привязать сразу несколько функций:
```js
buttons.addEventListener('click', func1);
buttons.addEventListener('click', func2);

function func() {
	alert('!!!');
}
function func2() {
	alert('!!!');
}
```

----

##### Отвязывание событий через `removeEventListener`

Этот метод первым параметром принимает тип события, а вторым - ссылку на именную функцию, которую нужно отвязать:
```js
let button = document.querySelector('#button');
button.addEventListener('click', func);

function func() {
	alert('!!!');
	this.removeEventListener('click', func);
}
```

---

##### Разное

Cвойство innerHTML - прочитываем текст элемента
```js
buttons.addEventListener('click', function() {
	elem.innerHTML = '!!!'; // у переменной elem текст заменится на !!!
	elem.innerHTML = elem.innerHTML + '!'; // а так просто добавит !!! без замены
});
```

Свойство `textContent` - извлекает текст из элемента.

---

Управляем атрибутами через свойства елементов:
```js
<button class="btn elem" id="button" type="submit" value="keys">

buttons.addEventListener('click', function() {
	alert(button.id);   // выведет 'button'
	alert(button.type); // выведет 'submit'
	buttons.type = 'text'; // присвоим новое значение атрибуту type
	
	alert(buttons.className); // Получим все классы btn и elem
	alert(elem.value); // Выведет 'keys'
	elem.value = 'new'; // поменяли свойство
});
```

----

Пользовательские атрибуты.

>В HTML разрешено добавлять свои, пользовательские атрибуты тегам. Такие атрибуты должны начинаться с `data-`, а затем должно идти любое название атрибута, которое удобно.

```js
<div id="elem" data-my-test="1000"></div>

let elem = document.querySelector('#elem');
alert(elem.dataset.myTest); // выведет 1000
elem.dataset.myTest = 123; // Присваиваем другое значение
```

>При обращении к атрибутам следует использовать camelCase

Можно обратиться через метод `getAttribute` в этом случае следует писать полное название атрибута:
```js
<div id="elem" data-num="1000" data-my-num="2000"></div>

let elem = document.querySelector('#elem');
alert(elem.getAttribute('data-num'));    // выведет 1000
alert(elem.getAttribute('data-my-num')); // выведет 2000
```

----

Стилизация элементов через атрибут `style`.

```js
let elem = document.querySelector('#elem');
elem.style.color = 'red';
```

>Свойства, которые записываются через дефис, например font-size, преобразуются в camelCase.

----

Поиск элементов внутри другого элемента:

```js
let parent = document.querySelector('#parent');
let elems = parent.querySelectorAll('.child');

//или так
let elems = document.querySelectorAll('#parent .child');
```

----

Атрибут `disabled` блокирует доступ и изменение поля формы.
`
```js
<input id="elem" disabled>

let elem = document.querySelector('#elem');
console.log(elem.disabled); // выведет true
elem.disabled = false; // Отключаем
```

----

Атрибут `checked` делает чекбокс отмеченным: `elem.checked`

----


