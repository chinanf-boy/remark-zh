
# remark-stringify [![Build Status][build-badge]][build-status] [![Coverage Status][coverage-badge]][coverage-status] [![Chat][chat-badge]][chat]

[**unified**][unified]的[编译器][Compiler]. 将一个[**MDAST**][mdast]语法树字符串化到markdown. 提供给[**remark** processor][processor]. 可[扩展][extend]改变markdown的编译方式. 

## 安装

[npm][]: 

```sh
npm install remark-stringify
```

## 用法

```js
var unified = require('unified');
var createStream = require('unified-stream');
var parse = require('remark-parse');
var toc = require('remark-toc');
var stringify = require('remark-stringify');

var processor = unified()
  .use(parse)
  .use(toc)
  .use(stringify, {
    bullet: '*',
    fence: '~',
    fences: true,
    incrementListMarker: false
  });

process.stdin
  .pipe(createStream(processor))
  .pipe(process.stdout);
```

## 目录

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [API](#api)
  - [`processor.use(stringify[, options])`](#processorusestringify-options)
      - [`options`](#options)
        - [`options.gfm`](#optionsgfm)
        - [`options.commonmark`](#optionscommonmark)
        - [`options.pedantic`](#optionspedantic)
        - [`options.entities`](#optionsentities)
        - [`options.setext`](#optionssetext)
        - [`options.closeAtx`](#optionscloseatx)
        - [`options.looseTable`](#optionsloosetable)
        - [`options.spacedTable`](#optionsspacedtable)
        - [`options.paddedTable`](#optionspaddedtable)
        - [`options.stringLength`](#optionsstringlength)
        - [`options.fence`](#optionsfence)
        - [`options.fences`](#optionsfences)
        - [`options.bullet`](#optionsbullet)
        - [`options.listItemIndent`](#optionslistitemindent)
        - [`options.incrementListMarker`](#optionsincrementlistmarker)
        - [`options.rule`](#optionsrule)
        - [`options.ruleRepetition`](#optionsrulerepetition)
        - [`options.ruleSpaces`](#optionsrulespaces)
        - [`options.strong`](#optionsstrong)
        - [`options.emphasis`](#optionsemphasis)
  - [`stringify.Compiler`](#stringifycompiler)
- [扩展编译器](#%E6%89%A9%E5%B1%95%E7%BC%96%E8%AF%91%E5%99%A8)
  - [`Compiler#visitors`](#compilervisitors)
  - [`function visitor(node[, parent])`](#function-visitornode-parent)
        - [参数](#%E5%8F%82%E6%95%B0)
        - [Returns](#returns)
- [执照](#%E6%89%A7%E7%85%A7)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

> 产物 为 `Entities`, 应该是作者称 生成的字符 作为 这样的名称

## API

### `processor.use(stringify[, options])`

配置`processor`将[**MDAST**][mdast]语法树 字符串化到markdown. 

##### `options`

选项直接传递,或稍后[`processor.data()`][data]传递. 

###### `options.gfm`

使用GFM兼容markdown所需的转义进行字符串化 (`boolean`,默认: `true`) . 

-   过滤管 (`|`,对于表格) 
-   过滤冒号 (`:`,对于文字网址) 
-   过滤波浪 (`~`,用于删除) 

###### `options.commonmark`

CommonMark兼容markdown字符串化 (`boolean`,默认: `false`) . 

-   分别编译相邻的块引用
-   使用斜杠而不是产物来逃避更多字符

###### `options.pedantic`

pedantic 兼容 markdown 的字符串化 (`boolean`,默认: `false`) . 

-   过滤下划线

###### `options.entities`

如何字符串化产物 (`string`或`boolean`,默认: `false`) : 

-   `true`- 为特殊HTML字符生成产物 (`&`>`&amp;`) 和非ASCII字符 (`©`>`&copy;`) . 如果未广泛支持命名产物,则使用编号字符引用 (`’`>`&#x2019;`) 
-   `'numbers'`- 生成编号产物 (`&`>`&#x26;`) 用于特殊HTML字符和非ASCII字符
-   `'escape'`- 编码特殊HTML字符 (`&`>`&amp;`,`’`>`&#x2019;`) ,非ASCII字符不能 (ö持续存在) 

###### `options.setext`

尽可能以Setext风格编译标题 (`boolean`,默认: `false`) . 用`=`给一级标题和`-`给二级标题. 其他标题级别编译为ATX (遵循`closeAtx`) . 

###### `options.closeAtx`

使用相同数量的闭合哈希编译ATX标题,作为开启哈希值 (`boolean`,默认: `false`) . 

###### `options.looseTable`

创建没有栅栏的表: 初始和最终的`|` (`boolean`,默认: `false`) . 

###### `options.spacedTable`

在管道和内容之间创建没有间距的表格 (`boolean`,默认: `true`) . 

###### `options.paddedTable`

在每个单元格中创建带填充的表,使它们的大小相同 (`boolean`,默认: `true`) . 

###### `options.stringLength`

函数传递给[`markdown-table`][markdown-table]检测表格单元格的长度 (`Function`,默认: [`s => s.length`][string-length]) . 

###### `options.fence`

用于代码块的栅栏标记 (`'~'`或者``'`'``,默认: ``'`'``) . 

###### `options.fences`

使用代码块,对没有语言的代码块进行字符串化 (`boolean`,默认: `false`) . 

> 最好为`true`

###### `options.bullet`

用于无序列表项的子标记 (`'-'`,`'*'`, 或者`'+'`,默认: `'-'`) . 

###### `options.listItemIndent`

如何缩进列表项中的内容 (`'tab'`,`'mixed'`或者`'1'`,默认: `'tab'`) . 

-   `'tab'`: 使用制表位 (4个空格) 
-   `'1'`: 使用一个空格
-   `'mixed'`:  自动使用`1`和`tab`,紧/松的列表项

###### `options.incrementListMarker`

是否增加有序列表项的项目符号 (`boolean`,默认: `true`) . 

###### `options.rule`

标记用于 空行 规则 (`'-'`,`'*'`, 或者`'_'`,默认: `'*'`) . 

###### `options.ruleRepetition`

用于 空行 规则 的标记数量 (`number`,默认: `3`) . 应该`3`或者更多. 

###### `options.ruleSpaces`

是否用空格填充 空行 标记 (`boolean`,默认`true`) . 

###### `options.strong`

标记用于 粗体 (`'_'`或者`'*'`,默认`'*'`) . 

###### `options.emphasis`

标记用于 斜体 (`'_'`或者`'*'`,默认`'_'`) . 

### `stringify.Compiler`

访问原始[编译器][comiler],如果你需要它. 

## 扩展编译器

如果使用此插件,则会添加一个[`Compiler`][compiler]构造函数到`processor`. 其他插件可以更改,并在编译器原型上添加访问者,可以更改markdown的字符串化方式. 

下面的插件修改了一个[访问][visitor],在二级标题之前添加一个额外的空白行. 

```js
module.exports = gap;

function gap() {
  var Compiler = this.Compiler;
  var visitors = Compiler.prototype.visitors;
  var original = visitors.heading;

  visitors.heading = function heading(node) {
    return (node.depth === 2 ? '\n' : '') + original.apply(this, arguments);
  }
}
```

### `Compiler#visitors`

一个对象将[节点][node]类型 映射 到[`visitor`][visitor]们. 

### `function visitor(node[, parent])`

字符串化`node`. 

###### 参数

-   `node` ([`Node`][node])  - 要编译的节点
-   `parent` ([`Node`][node],可选)  - 父母`node`

###### Returns

`string`,编译给出`node`. 

## 执照

[MIT][license]©[Titus Wormer][author]

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

[unified]: https://github.com/unifiedjs/unified

[processor]: https://github.com/remarkjs/remark

[data]: https://github.com/unifiedjs/unified#processordatakey-value

[compiler]: https://github.com/unifiedjs/unified#processorcompiler

[mdast]: https://github.com/syntax-tree/mdast

[node]: https://github.com/syntax-tree/unist#node

[extend]: #extending-the-compiler

[visitor]: #function-visitornode-parent

[markdown-table]: https://github.com/wooorm/markdown-table

[string-length]: https://github.com/wooorm/markdown-table#stringlengthcell
