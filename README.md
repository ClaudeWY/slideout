# Slideout.js [![NPM version][npm-image]][npm-link] [![Build status][travis-image]][travis-link] [![devDependency status][devdeps-image]][devdeps-link]

> 为你的移动 Web 应用准备的触摸式导航菜单

## 特性

- 自由使用
- 标记简单
- 原生滚动
- 易于定制
- CSS 转换和过渡
- 只有 2 Kb！（min & gzip）

## Demo

[点击查看 demo](http://slideout.getmaterialize.com/)（在你的移动设备上或在你的浏览器上模拟触摸）

<img src="https://i.imgur.com/AWgwlVW.gif" alt="Slideout.js demo">

## 安装

Slideout 在 cdnjs 中可用

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/slideout/0.1.9/slideout.min.js"></script>
```

你也可以使用一个包管理器

    $ npm install slideout

    $ spm install slideout

    $ bower install slideout.js

    $ component install mango/slideout

## 如何使用

在你的项目中使用 Slideout.js 非常容易。

首先，你需要创建你的标记。在你的网页中应该有一个菜单（`#menu`）和主要内容（`#panel`）。

```html
<nav id="menu">
  <header>
    <h2>Menu</h2>
  </header>
</nav>

<main id="panel">
  <header>
    <h2>Panel</h2>
  </header>
</main>
```

在你的 Web 应用中添加 Slideout.js 的样式（index.css）。

```css
body {
  width: 100%;
  height: 100%;
}

.slideout-menu {
  position: fixed;
  left: 0;
  top: 0;
  bottom: 0;
  right: 0;
  z-index: 0;
  width: 256px;
  overflow-y: auto;
  -webkit-overflow-scrolling: touch;
  display: none;
}

.slideout-panel {
  position:relative;
  z-index: 1;
}

.slideout-open,
.slideout-open body,
.slideout-open .slideout-panel {
  overflow: hidden;
}

.slideout-open .slideout-menu {
  display: block;
}
```

然后你就要引入 Slideout.js 并通过一些选项来创建一个新的实例：

```html
<script src="dist/slideout.min.js"></script>
<script>
  var slideout = new Slideout({
    'panel': document.getElementById('panel'),
    'menu': document.getElementById('menu'),
    'padding': 256,
    'tolerance': 70
  });
</script>
```

#### 完整示例

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Slideout Demo</title>
    <meta http-equiv="cleartype" content="on">
    <meta name="MobileOptimized" content="320">
    <meta name="HandheldFriendly" content="True">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <style>
      body {
        width: 100%;
        height: 100%;
      }

      .slideout-menu {
        position: fixed;
        left: 0;
        top: 0;
        bottom: 0;
        right: 0;
        z-index: 0;
        width: 256px;
        overflow-y: auto;
        -webkit-overflow-scrolling: touch;
        display: none;
      }

      .slideout-panel {
        position:relative;
        z-index: 1;
      }

      .slideout-open,
      .slideout-open body,
      .slideout-open .slideout-panel {
        overflow: hidden;
      }

      .slideout-open .slideout-menu {
        display: block;
      }
    </style>
  </head>
  <body>

    <nav id="menu">
      <h2>Menu</h2>
    </nav>

    <main id="panel">
      <header>
        <button class="toggle-button">☰</button>
        <h2>Panel</h2>
      </header>
    </main>

    <script src="dist/slideout.min.js"></script>
    <script>
      var slideout = new Slideout({
        'panel': document.getElementById('panel'),
        'menu': document.getElementById('menu'),
        'padding': 256,
        'tolerance': 70
      });

      // Toggle button
      document.querySelector('.toggle-button').addEventListener('click', function() {
        slideout.toggle();
      });
    </script>

  </body>
</html>
```

## 浏览器支持

- Chrome (IOS, Android, desktop)
- Firefox (Android, desktop)
- Safari (IOS, Android, desktop)
- Opera (desktop)
- IE 10+ (desktop)

## API

### Slideout(options)
创建一个新的 `Slideout` 实例。

- `options` (对象) - 一个使用自定义选项的 Slideout 实例。
- `options.panel` (HTML 元素) - 程序中包含 `.slideout-panel` 的 DOM 元素。
- `options.menu` (HTML 元素) - 程序中包含 `.slideout-menu` 的 DOM 元素。
- `[options.duration]` (数字) - 打开/关闭 slideout 的时间（毫秒）。默认：`300`
- `[options.fx]` (字符串) - 使用动画开启和关闭 slideout 时的 CSS 效果。默认：`ease`
- `[options.padding]` (数字) - 默认：`256`
- `[options.tolerance]` (数字) - 默认：`70`
- `[options.touch]` (布尔值) - 设置此项为 false 可以禁用 Slideout 的触摸事件。默认：`true`
- `[options.side]` (字符串) - 设置 slideout 从左侧或右侧打开 (`left` 或 `right`)。默认：`left`

```js
var slideout = new Slideout({
  'panel': document.getElementById('main'),
  'menu': document.getElementById('menu'),
  'padding': 256,
  'tolerance': 70
});
```

### Slideout.open();
打开 slideout 菜单。它发出 `beforeopen` 和 `open` 事件。

```js
slideout.open();
```

### Slideout.close();
关闭 slideout 菜单。它发出 `beforeclose` 和 `close` 事件。

```js
slideout.close();
```

### Slideout.toggle();
切换 slideout 菜单（打开/关闭状态）。

```js
slideout.toggle();
```

### Slideout.isOpen();
当 slideout 处于打开状态时返回 `true`，当处于关闭状态时返回 `false`。

```js
slideout.isOpen(); // true or false
```

### Slideout.destroy();
清理其他的 slideout 实例使其可以在同一区域再次创建。

```js
slideout.destroy();
```

### Slideout.enableTouch();
开启通过触摸事件打开 slideout。

```js
slideout.enableTouch();
```

### Slideout.disableTouch();
禁止通过触摸事件打开 slideout。

```js
slideout.disableTouch();
```

### Slideout.on(event, listener);
```js
slideout.on('open', function() { ... });
```

### Slideout.once(event, listener);
```js
slideout.once('open', function() { ... });
```

### Slideout.off(event, listener);
```js
slideout.off('open', listener);
```

### Slideout.emit(event, ...data);
```js
slideout.emit('open');
```

## 事件

一个 Slideout 实例可以发出以下事件：

- `beforeclose`
- `close`
- `beforeopen`
- `open`
- `translate`

只有当通过触摸事件将它打开/关闭时，slideout 会发出 `translate` 事件。

```js
slideout.on('translate', function(translated) {
  console.log(translated); // 120 in px
});
```

## npm-scripts
```
$ npm run build
```

```
$ npm run dist
```

```
$ npm test
```

```
$ npm run hint
```

## FAQ

### 如何添加一个切换按钮

```js
// vanilla js
document.querySelector('.toggle-button').addEventListener('click', function() {
  slideout.toggle();
});

// jQuery
$('.toggle-button').on('click', function() {
    slideout.toggle();
});
```

### 如何从右边打开 slideout

你应该为 `.slideout-menu` 类设置 `left: auto`。
```css
.slideout-menu {
  left: auto;
}
```

然后，设置 `side` 选项的值为 `right`。
```js
var slideout = new Slideout({
  'panel': document.getElementById('content'),
  'menu': document.getElementById('menu'),
  'side': 'right'
});
```

## With ❤ by
- Guille Paz (Front-end developer | Web standards lover)
- E-mail: [guille87paz@gmail.com](mailto:guille87paz@gmail.com)
- Twitter: [@pazguille](http://twitter.com/pazguille)
- Web: [http://pazguille.me](http://pazguille.me)

## License
MIT license. Copyright © 2015 [Mango](http://getmango.com).

[npm-image]: https://img.shields.io/npm/v/slideout.svg?style=flat
[npm-link]: https://npmjs.org/package/slideout
[travis-image]: https://img.shields.io/travis/Mango/slideout.svg?style=flat
[travis-link]: https://travis-ci.org/Mango/slideout
[devdeps-image]: https://img.shields.io/david/dev/mango/slideout.svg?style=flat
[devdeps-link]: https://david-dm.org/mango/slideout#info=peerDependencies
