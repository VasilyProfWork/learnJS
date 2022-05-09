# scss
----

Переменные:
```scss
$fz: 80px; Запоминает значение
$color_1: #fff;

.block{
	font-size: $fz;
}
.text{
	font-size: $fz;
	color: $color_1;
}
```

Импорт - `@import "nullstyle.scss";`

Шаблоны:
```scss
%tplborder{
	border-bottom: 5px solid #fff;
	color: red;
	margin-bottom: 1.5rem
}

Для того чтобы использовать этот шаблон нужно прописать 
	@extend %tplborder;
```

Миксины:
```scss
@mixin fontz($f,$c){
	font-size: $f;
	color: $c; 	
}

//Для подключения миксина 
@include fontz(50px, green);
```