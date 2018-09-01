# remark[![Build Status][build-badge]][build-status] [![Coverage Status][coverage-badge]][coverage-status] [![Chat][chat-badge]][chat]

该[`remark`][remark]处理器是由降压处理器驱动的[插件][].

- 接口[`统一`][unified]
- [**MDAST**][mdast]语法树
- 解析树的 markdown[`此言-解析`][parse]
- [插件][]改造树
- 使用将树编译为 markdown[`此言-字符串化`][stringify]

不需要解析器?还是编译器?[没关系][unified-usage].

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

###### 通过数据设置

这个例子美化了 markdown 和配置[`此言-解析`][parse]和[`此言-字符串化`][stringify]通过[数据][].

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

###### 通过预设进行设置

这个例子美化了 markdown 和配置[`此言-解析`][parse]和[`此言-字符串化`][stringify]通过[预置][].

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
