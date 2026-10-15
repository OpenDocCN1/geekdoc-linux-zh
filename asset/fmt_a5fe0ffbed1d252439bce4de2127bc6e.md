
## 404 进通 CSS

```css
transform: translate3d(calc(-100% - 6vw),-30%,0)
rotate3d(0,0,1,4deg);
transition: all 0.4s;
```

```css
.marquee {
  position: absolute;
  top: 0;
  left: 0;
  width: var(--marquee-width);
  overflow: hidden;
  pointer-events: none;
  mix-blend-mode: color-burn;
}
```

```css
.marquee__inner {
  display: flex;
  position: relative;
  transform: translate3d(var(--move-initial), 0, 0);
  animation: marquee 5s linear infinite;
  animation-play-state: paused;
  opacity: 0;
  transition: opacity 0.1s;
}
```

```css
.menu__item-link:hover ~ .marquee .marquee__inner {
  animation-play-state: running;
  opacity: 1;
  transition-duration: 0.7s;
}
```

```css
.marquee span {
  text-align: center;
}
```

```css
.menu__item-link,
.marquee span {
  white-space: nowrap;
  font-size: var(--item-font-size);
  padding: 0 1vw;
  font-weight: 900;
  line-height: 1.15;
}
```

```css
.marquee span {
  font-style: italic;
}
@keyframes marquee {
  0% {
    transform: translate3d(var(--move-initial), 0);
  }
  100% {
    transform: translate3d(var(--move-final), 0);
  }
}
```

CSS MarqueeMenu 插件。

当你将此链接粘贴到 Chrome 的地址栏（`https://use.typekit.net/zhq0vyf.css`）后，你将在下方页面中获得这段代码：

```css
@import url("https://p.typekit.net/p.css?s=1&k=zhq0vyf&tkf=24537.24538.24539.24540.24547.38192.38197.38198.38199.38200&a=149256&app=typekit
```

## 406 进通 CSS

（其余的 CSS 代码遵循基于提供的上下文逻辑）

另一个示例：

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>CSS-only Marquee Menu | Codrops</title>
  <meta name="description" content="A css-only marquee hover effect" />
  <meta name="keywords" content="marquee,animation,loop,hover,navigation" />
  <link rel="shortcut icon" href="favicon.ico">
  <style>
*{box-sizing: border-box;margin: 0}
body(overflow-x: hidden);
.content{padding-left: 20px;padding-bottom: 30px}
h1{margin: 50px 0;font-family: roboto}
p(margin-bottom: 20px)
marquee {
  --pos-x: 0;
  width: 100vw;
  display: flex;
  overflow: hidden;
}
.marquee__row {
  translateX: calc(var(--pos-x) * 1px);
  flex-shrink: 0;
  min-width: 100vw;
  display: flex;
  justify-content: space-around;
  transform: translateX(var(--translateX));
}
.marquee--text {
  background-color: #89ff91;
}
marquee__item-text {
  margin: 0;
  font-size: 65px;
  margin: 2em..4em;
}
marquee--nezuko {
  background-color: pink;
}
marquee__item-nezuko {
  --height: calc(100px + 50px * ((var(--viewport-375) / 1065)));
}
```
</style>
</head>
<body>
<div class="marquee marquee-text" data-speed="25">
<div class="marquee_row marquee--text">
<p class="marquee_item marquee_item" data-clone="5"> CSS Marquee Menu Effect / </p>
</div>
</div>
</body>
<script>
const marqueeArr = document.querySelectorAll('.marquee');
marqueeArr.forEach(marquee => {
  // logic continues
});
</script>
```

## 407 CSS 插件

## 408 进通 CSS

```css
height: var(--height);
margin: calc(0.1 * var(--height)) calc(0.3 * var(--height));
}
```
