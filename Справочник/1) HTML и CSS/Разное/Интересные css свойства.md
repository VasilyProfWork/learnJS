### Интересные css свойства
---

У мобилок ховер не работает:
```html
<a href="#">Try hovering over me!</a>
```

```scss
@media (any-hover: hover) {
  a:hover {
    background: yellow;
  }
}
```

---

Взаимодействие через обьект:
```scss
pointer-events: none;
```

---

Выравнивание блока по вертикали:
```scss
margin: auto 0;
// или
margin-top: auto;
```

---

Прижимаем `footer` к низу страницы:
```scss
.main{
    min-height: calc(100vh - 80px);
}
```

>80px это высота футера.