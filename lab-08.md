# Lab 8: Animations

In this lab session we will look at ways to animate your content.

First, we need to put some content in the page.

Create a basic template site with `index.html` and `styles.css` connected as usual.
Don't forget to add the viewport `meta` tag into your `head` element.


### index.html

Now add some content.

```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
	<head>
		<meta charset="utf-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<title>Animations</title>
		<link rel="stylesheet" href="css/lab.css">
	</head>
	<body>
		<header>
			<h1>CTEC3905: Front-end web development</h1>
			<img src="https://ctec3905-2020-21.github.io/splash/images/html.svg" alt="html logo">
			<img src="https://ctec3905-2020-21.github.io/splash/images/css.svg" alt="css logo">
			<img src="https://ctec3905-2020-21.github.io/splash/images/js.svg" alt="js logo">
		</header>
	</body>
</html>
```

### styles.css

Now we can add some styles.

```css
/* body {
	overflow: hidden;
} */
header {
	text-align: center;
	font-family: sans-serif;
}
header img {
	width: 12em;
	animation: appear 5s forwards ease-out;
	transition: 0.4s;
}
header img:hover {
	filter: invert();
}
header img:nth-of-type(1) {
	transform: translateX(-5vw) scale(0.4);
}
header img:nth-of-type(2) {
	transform: translateY(5vw) scale(0.4);
}
header img:nth-of-type(3) {
	transform: translateX(5vw) scale(0.4);
}

@keyframes appear {
	10% {
		transform: translateY(-1vw) scale(1.1)
	}
	90% {
		transform: none;
	}
	100% {
		transform: rotateY(1turn);
	}
}

```

Study the code and make your own changes.

Now add a `<main>` element and create an animation of your own.

Try using CSS to draw a simple picture e.g. a tree and animate it.

> Hint: simplify shapes to squares, rectangles and circles where possible.

Include some animation in your assignment code.

## More challenges

Use the [example code](https://ctec3905-2020-21.github.io/animations) ([source](https://github.com/CTEC3905-2020-21/animations)) as a reference.

If you feel confident to do so, try animating with JavaScript.
Take the example code and make some changes.

Try removing gravity and have the ball bounce off all the edges.

Try increasing the size of the ball.

Try using your own SVG images.

Add code to stop the animation after 20 seconds.

How would you add a second ball to the animation?
