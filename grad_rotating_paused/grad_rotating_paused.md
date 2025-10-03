
# Situación:

* Leer texto sobre imágenes que mezclan claro/oscuro no siempre es fácil
* Usar `background` y degradados como alternativa a complicarse con pseudo-elementos `::` para crear un overlay
* Animación del botón

## styles00.css

![[./_images/00.png]]

```html
<!DOCTYPE html>
<head>
	<link rel="stylesheet" href="./styles00.css">
</head>
<body>
	<main>
	<h1>Single color gradients are useful!</h1>
	<p>It might seem strange, considering gradients are all about transitions between colors, but single color gradients can be super useful in CSS.</p>
	<button type="button">Tutorial</button>
	</main>
</body>
```

```css
/* styles00.css */

main {
	position: relative;
	border-radius: 12px;
	padding: 3rem;
	background-size: cover;
	background-position: center;
	background-image:
		url("./aurora_borealis.jpg");
		
	&::after {
		content: "";
		position: absolute;
		z-index: -1;
		inset: 4rem;
		bottom: 0;
		filter: blur(2rem);
		background-image: linear-gradient(
			90deg in oklch,
			hsl(148, 61%, 31%),
			hsl(125, 75%, 79%),
			hsl(148, 61%, 31%),
			hsl(125, 75%, 79%)
		);
	}
}

button {
	text-decoration: none;
	font: inherit;
	color: black;
	padding: 0.5em 1.25em;
	border-radius: 4px;
	
	border: none;
	background: white;
}

button:hover,
button:focus-visible {
	animation: rotate 3s linear infinite;
}

@layer general-styling {
	html {
		color-scheme: dark light;
		font-family: system-ui;
		line-height: 1.6;
	}
	
	body {
		font-size: 1.125rem;
		margin: 1rem;
	}
}
```


## styles01.css

* Como las los gradientes son imágenes, podemos ubicarlos dentro del `background-image`
* Declaramos un primer `linear-gradient` en `background-image` que al por estar encima de la imagen la taparía

```css
main {
	...
	background-image:
		linear-gradient(#ff0066),               /*  <--  */
		url("./aurora_borealis.jpg");
}
```

![[./_images/01.png]]

Cambiamos a _hsl_ para ponerle transparencia, e inicio y fin del gradiente:

`hsl(0 0% 0% / .5)

```css
main {
	...
	background-image:
		linear-gradient(hsl(0 0% 0% / .5)),    /*  <--  */
		url("./aurora_borealis.jpg");
}
```

### Compatibilidad styles02.css

Como el `linear-gradient`en `background-image` es relativamente nuevo (2025), podemos agregar `0 0` para no determinar inicio ni final de la transición. 

O Ponemos `0 100%`  para que no inicien y así maximizar la compatibilidad entre navegadores.

```css
main {
	...
	background-image:
		linear-gradient(hsl(0 0% 0% / .25) 0 0),
		url("./aurora_borealis.jpg");
}
```

**¿Qué hace `0 0`?**

```css
main {
	...
	background-image:
		linear-gradient(red, hsl(0 0% 0% / .25) 20% 50%, red),
		url("./aurora_borealis.jpg");
}
```

![[./_images/02.png]]
*Empieza en red, pasa a hsl transparencia 0.25 entre el 20% y el 50% de la imagen y vuelve a red.*


## Gradient Borders

Vamos al elemento botón:


```css
button {
	text-decoration: none;
	font: inherit;
	color: black;
	padding: 0.5em 1.25em;
	border-radius: 4px;
	
	border: none;    /*  <--  */
	background: white;
}
```

El truco es agregar un borde **transparente** (de 5px solid para hacerlo exagerado) y usar `background` como shorthand en lugar de _~~`background-color`~~_ porque vamos a usar otras propiedades luego:

`border: 5px solid transparent`
`background: white`





