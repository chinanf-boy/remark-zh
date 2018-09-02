# remark [![Build Status][build-badge]][build-status] [![Coverage Status][coverage-badge]][coverage-status] [![Chat][chat-badge]][chat]

该[`remark`][remark]处理器是由[插件][plugins]驱动的 markdown 处理器.

- [`unified`][unified]定义接口
- [**MDAST**][mdast]语法树
- 解析 markdown 到树 - [`remark-parse`][parse]
- [插件][plugins]改造树
- 使用[`remark-stringify`][stringify]将树编译为 markdown

不需要解析器? 还是编译器? [没关系][unified-usage].

## 安装

[npm][]:

```sh
npm install remark
```

## 用法

###### 常见的例子

此示例提示 markdown 并将其转换为 HTML.

```js
var remark = require('remark');
var recommended = require('remark-preset-lint-recommended');
var html = require('remark-html');
var report = require('vfile-reporter');

remark()
  .use(recommended)
  .use(html)
  .process('## Hello world!', function(err, file) {
    console.error(report(err || file));
    console.log(String(file));
  });
```

输出:

```txt
1:1  warning  Missing newline character at end of file  final-newline  remark-lint

⚠ 1 warning
```

```html
<h2>Hello world!</h2>
```

###### 通过data设置

这个例子通过[data][]美化了 markdown 和配置[`remark-parse`][parse]和[`remark-stringify`][stringify].

```js
var remark = require('remark');

remark()
  .data('settings', {commonmark: true, emphasis: '*', strong: '*'})
  .process('_Emphasis_ and __importance__', function(err, file) {
    if (err) throw err;
    console.log(String(file));
  });
```

输出:

```markdown
_Emphasis_ and **importance**
```

###### 通过preset进行设置

这个例子通过[预设置][]美化了 markdown 和配置[`remark-parse`][parse]和[`remark-stringify`][stringify].

```js
var remark = require('remark');

remark()
  .use({
    settings: {commonmark: true, emphasis: '*', strong: '*'}
  })
  .process('_Emphasis_ and __importance__', function(err, file) {
    if (err) throw err;
    console.log(String(file));
  });
```

输出:

```markdown
_Emphasis_ and **importance**
```

## 执照

[MIT][license]©[泰特斯沃尔默][author]

<!-- Definitions -->

[build-badge]: https://img.shields.io/travis/remarkjs/remark.svg
[build-status]: https://travis-ci.org/remarkjs/remark
[coverage-badge]: https://img.shields.io/codecov/c/github/remarkjs/remark.svg
[coverage-status]: https://codecov.io/github/remarkjs/remark
[chat-badge]: https://img.shields.io/gitter/room/remarkjs/Lobby.svg
[chat]: https://gitter.im/remarkjs/Lobby
[license]: https://github.com/remarkjs/remark/blob/master/LICENSE
[author]: http://wooorm.com
[npm]: https://docs.npmjs.com/cli/install
[remark]: https://github.com/remarkjs/remark
[unified]: https://github.com/unifiedjs/unified
[mdast]: https://github.com/syntax-tree/mdast
[parse]: https://github.com/remarkjs/remark/blob/master/packages/remark-parse
[stringify]: https://github.com/remarkjs/remark/blob/master/packages/remark-stringify
[plugins]: https://github.com/remarkjs/remark/blob/master/doc/plugins.md
[unified-usage]: https://github.com/unifiedjs/unified#usage
[preset]: https://github.com/unifiedjs/unified#preset
[data]: https://github.com/unifiedjs/unified#processordatakey-value
