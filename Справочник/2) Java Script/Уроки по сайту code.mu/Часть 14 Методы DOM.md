# Методы DOM
---

Метод `getAttribute` считывает значение указанного атрибута у тега.

```js
<input id="elem" value="abcde">
let elem = document.querySelector('#elem');
let value = elem.getAttribute('value');

console.log(value); // abcde
```

>Атрибут, полученный через getAttribute, хранит исходное значение даже после того, как пользователь заполнил поле и свойство изменилось.
>value можем получить и таким способом
>`alert(elem.value);` // Получили свойство
>`elem.value = 'new';` // Поменяли свойство
>`elem.getAttribute('value');` // Свойство не поменялось
>`elem.setAttribute('value', 'new');` // Это уже точно поменяет


----

Метод `setAttribute` позволяет изменить значение заданного атрибута какого-либо тега.

```js
<input id="elem" value="abcde">

let elem = document.querySelector('#elem');
elem.setAttribute('value', '!!!');

// HTML код станет выглядеть так: <input id="elem" value="!!!">
```

---

Метод `removeAttribute` удаляет заданный атрибут у какого-либо тега.

```js
elem.removeAttribute('value');

// HTML код будет выглядить так <input id="elem">
```

----

Метод `hasAttribute` проверяет наличие заданного атрибута у элемента. 
Если атрибут есть - выведет `true`, если нет - выведет `false`.

---

##### Манипулирование CSS классами

Свойство `classList` содержит псевдомассив CSS классов элемента, а также позволяет добавлять и удалять классы элемента, проверять наличие определенного класса среди классов элемента.

```js
<p id="elem" class="www ggg zzz"></p>

let elem = document.querySelector('#elem');
let classNames = elem.classList; // Получаем в переменную классы: www ggg zzz 
```

---

Метод `add` объекта `classList` позволяет добавлять CSS классы элементу.

```js
elem.classList.add('kkk');

//Результат: 
<p id="elem" class="www ggg zzz kkk"></p>
```

----

Метод `remove` объекта `classList` удаляет заданный CSS класс элемента.

```js
elem.classList.remove('ggg');

//Результат:
<p id="elem" class="www zzz"></p>
```

----

Метод `contains` объекта `classList` проверяет наличие CSS класса элемента.

```js
let contains = elem.classList.contains('ggg');
console.log(contains); // true
```

----

Метод `toggle` объекта `classList` чередует заданный CSS класс элемента: добавляет класс, если его нет и удаляет, если есть.

```js
<p id="elem" class="www ggg zzz"></p>

let elem = document.querySelector('#elem');
elem.classList.toggle('zzz');

//Результат:
<p id="elem" class="www ggg"></p>
```

> Можно сделать слушатель события по клику добовлять или убирать класс.

---

Свойство `firstElementChild` содержит первый дочерний элемент. 
Свойство `lastElementChild` хранит в себе последний дочерний элемент. 
Свойство `children` хранит в себе псевдомассив дочерних элементов. 

>Дочерними элементами считаются все теги, которые непосредственно расположены внутри блока.

```js
<div id="parent">
	<p>1</p>
	<p>2</p>
</div>

let parent = document.querySelector('#parent');
let text = parent.firstElementChild.innerHTML;

console.log(text);
```

----

Свойство `parentElement` содержит родительский элемент.

```js
<div id="parent">
	<p id="elem"></p>
</div>

let elem = document.querySelector('#elem');
let id = elem.parentElement.id;

console.log(id); //'parent'
```

----

Метод `closest` ищет ближайший родительский элемент, подходящий под указанный CSS селектор, при этом сам элемент тоже включается в поиск.

```js
<div class="www" id="parent2">
	<div class="ggg" id="parent1">
		<p class="zzz" id="child"></p>
	</div>
</div>

let elem = document.querySelector('#child');
let parent = elem.closest('.www');
console.log(parent.id); //'parent2'
```

----

Свойство `previousElementSibling` содержит предыдущий элемент, находящийся в этом же родителе. Если такого элемента нет - возвращается `null`.
Свойство `nextElementSibling` содержит следующий элемент, находящийся в этом же родителе. Если такого элемента нет - возвращается `null`.

```js
<p>sibling</p>
<p id="elem">elem</p>
let elem = document.querySelector('#elem');
let text = elem.previousElementSibling.innerHTML;

console.log(text); //'sibling'
```

----

Позволяют принудительно установить фокус в инпут или убрать его оттуда
`elem.focus();`

---

Свойство `selectedIndex` хранит в себе номер выбранного `select`

```js
select.selectedIndex = 2; // выберет 'три'

//Получение выбранного оптиона
let select = document.querySelector('#select');
console.log(select[select.selectedIndex]);
```

----

Метод `createElement` следует передавать имя тега, который должен быть создан.
Метод `appendChild` позволяет размещать один новосозданный элемент в конец.
Метод `append` позволяет вставить в конец какого-либо элемента много других.
Метод `prepend` позволяет вставить в начало какого-либо элемента другой элемент.
Метод `insertBefore` позволяет вставить элемент перед другим элементом.


```js
<div id="parent">
	<p>1</p>
	<p>2</p>
	<p>3</p>
</div>

let parent = document.querySelector('#parent');

let p = document.createElement('p');
p.innerHTML = '!';

parent.appendChild(p);
//или так
parent.append(p);

//Результат выполнения кода:
<div id="parent">
	<p>1</p>
	<p>2</p>
	<p>3</p>
	<p>!</p>
</div>
```

----

Метод `insertAdjacentElement` 
Метод `insertAdjacentHTML` - отличие от предыдущего метода заключается в том, 
что код получаеться меньше и не нужно создавать переменную. (Смотри пример)

>Можно сделать вставку перед опорным элементом (способ вставки beforeBegin), после него (способ вставки afterEnd), а также в начало (способ вставки afterBegin) или в конец (способ вставки beforeEnd) опорного элемента. 
>`опорный элемент.insertAdjacentElement(способ вставки, код для вставки)`
>`опорный элемент.insertAdjacentHTML(способ вставки, код для вставки)`

>Из MDN: innerHTML устанавливает или получает синтаксис HTML, описывающий потомки элемента. 
>При записи на innerHTML он перезапишет его содержимое исходного элемента. Это означает, что HTML должен быть загружен и повторно обработан. Это не очень эффективно, особенно при использовании внутренних петель.

>node.appendChild
>Из MDN: Добавляет node в конец списка дочерних элементов указанного родителя node. Если node уже существует, он удаляется из текущего родителя node, а затем добавляется в новый родительский node.
>Этот метод поддерживается всеми браузерами и является более чистым способом вставки узлов, текста, данных и т.д. в DOM.

>element.insertAdjacentHTML
>Из MDN: анализирует указанный текст как HTML или XML и вставляет результирующие узлы в дерево DOM в указанной позиции.
>Этот метод также поддерживается всеми браузерами.

Пример:
```js
Способ beforeBegin
<div id="target">
	<p>elem</p>
</div>

let p = document.createElement('p');
p.innerHTML = '!';
let target = document.querySelector('#target');
target.insertAdjacentElement('beforeBegin', p);
//или так 
target.insertAdjacentHTML('beforeBegin', '<p>!</p>');

//Результат выполнения кода
<p>!</p>
<div id="target">
	<p>elem</p>
</div>


//Способ afterEnd
target.insertAdjacentElement('afterEnd', p);

//Результат выполнения кода
<div id="target">
	<p>elem</p>
</div>
<p>!</p>

//Способ afterBegin
target.insertAdjacentElement('afterBegin', p);

//Результат выполнения кода
<div id="target">
	<p>!</p>
	<p>elem</p>
</div>

//Способ beforeEnd
target.insertAdjacentElement('beforeEnd', p);

//Результат выполнения кода
<div id="target">
	<p>elem</p>
	<p>!</p>
</div>
```

---

Метод `cloneNode` -  клонирует элемент.

>Если передан true, то элемент клонируется полностью, вместе со всем атрибутами и дочерними элементами, а если false - только сам элемент.

```js
<div id="parent">
	<div class="elem">
		<p>первый абзац</p>
		<p>второй абзац</p>
	</div>
</div>

let parent = document.querySelector('#parent');
let elem = parent.querySelector('.elem');

let clone = elem.cloneNode(true);
parent.appendChild(clone);

//Результат выполнения кода
<div id="parent">
	<div class="elem">
		<p>первый абзац</p>
		<p>второй абзац</p>
	</div>
	<div class="elem">
		<p>первый абзац</p>
		<p>второй абзац</p>
	</div>
</div>
```

----

Метод `matches` позволяет проверить, удовлетворяет ли элемент указанному CSS селектору. `элемент.matches('селектор');`
```js
<p id="elem" class="www"></p>
let elem = document.querySelector('#elem');
console.log(elem.matches('p.www')); //true
```

----

Метод `contains` позволяет проверить, содержит ли один элемент внутри себя другой. `родитель.contains(элемент)`
```js
<div id="parent">
	<p id="child"></p>
</div>
let parent = document.querySelector('#parent');
let child = document.querySelector('#child');

let contains = parent.contains(child);
console.log(contains); //true
```

----

