
# 此言-字符串化[![Build Status][build-badge]][build-status] [![Coverage Status][coverage-badge]][coverage-status] [![Chat][chat-badge]][chat]

[编译器][]对于[**统一**][unified]. 字符串化[**MDAST**][mdast]markdown的语法树. 用于[**remark**处理器][processor]. 可[扩展][extend]改变markdown的编译方式. 

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

-   [API](#api)
    -   [processor.use (字符串化\[,选项\]) ](#processorusestringify-options)
    -   [stringify.Compiler](#stringifycompiler)
-   [扩展编译器](#extending-the-compiler)
    -   [编译器#游客](#compilervisitors)
    -   [功能访客 (节点\[,父母\]) ](#function-visitornode-parent)
-   [执照](#license)

## API

### `processor.use (stringify [,options]) `

配置`处理器`字符串化[**MDAST**][mdast]markdown的语法树. 

##### `选项`

选项直接传递,或稍后传递[`processor.data () `][data]. 

###### `options.gfm`

使用GFM兼容markdown所需的转义进行字符串化 (`布尔`,默认: `真正`) . 

-   逃生管 (`|`,对于表格) 
-   逃生冒号 (`: `,对于文字网址) 
-   逃脱波浪 (`〜`,用于删除) 

###### `options.commonmark`

Stringify for CommonMark兼容markdown (`布尔`,默认: `假`) . 

-   分别编译相邻的块引用
-   使用斜杠而不是实体来逃避更多字符

###### `options.pedantic`

Stringify for pedantic compatible markdown (`布尔`,默认: `假`) . 

-   用语言来逃避下划线

###### `options.entities`

如何字串化实体 (`串`要么`布尔`,默认: `假`) : 

-   `真正`- 为特殊HTML字符生成实体 (`&`>`&安培;`) 和非ASCII字符 (`©`>`&复制;`) . 如果未广泛支持命名实体,则使用编号字符引用 (`"`>`&#x2019的;`) 
-   `"数字"`- 生成编号实体 (`&`>`&#X26;`) 用于特殊HTML字符和非ASCII字符
-   `'逃逸'`- 编码特殊HTML字符 (`&`>`&安培;`,`"`>`&#x2019的;`) ,非ASCII字符不 (ö持续存在) 

###### `options.setext`

尽可能以Setext风格编译标题 (`布尔`,默认: `假`) . 用途`=`一级标题和`-`二级标题. 其他标题级别编译为ATX (尊重`closeAtx`) . 

###### `options.closeAtx`

使用相同数量的闭合哈希编译ATX标题作为开启哈希值 (`布尔`,默认: `假`) . 

###### `options.looseTable`

创建没有栅栏的表: 初始和最终管道 (`布尔`,默认: `假`) . 

###### `options.spacedTable`

在管道和内容之间创建没有间距的表格 (`布尔`,默认: `真正`) . 

###### `options.paddedTable`

在每个单元格中创建带填充的表,使它们的大小相同 (`布尔`,默认: `真正`) . 

###### `options.stringLength`

函数传递给[`markdown表`][markdown-table]检测表格单元格的长度 (`功能`,默认: [`s => s.length`][string-length]) . 

###### `options.fence`

用于代码块的栅栏标记 (`'〜'`要么`"'"`,默认: `"'"`) . 

###### `options.fences`

使用围栏对没有语言的代码块进行字符串化 (`布尔`,默认: `假`) . 

###### `options.bullet`

用于无序列表项的子标记 (`' - '`,`'*'`, 要么`'+'`,默认: `' - '`) . 

###### `options.listItemIndent`

如何缩进列表项中的内容 (`'标签'`,`"混合"`要么`'1'`,默认: `'标签'`) . 

-   `'标签'`: 使用制表位 (4个空格) 
-   `'1'`: 使用一个空格
-   `"混合"`:  使用`1`紧张和`标签`对于松散列表项

###### `options.incrementListMarker`

是否增加有序列表项目项目符号 (`布尔`,默认: `真正`) . 

###### `options.rule`

标记用于主题中断/横向规则 (`' - '`,`'*'`, 要么`'_'`,默认: `'*'`) . 

###### `options.ruleRepetition`

用于主题中断/水平规则的标记数量 (`数`,默认: `3`) . 应该`3`或者更多. 

###### `options.ruleSpaces`

是否用空格填充主题中断 (水平规则) 标记 (`布尔`,默认`真正`) . 

###### `options.strong`

标记用于重要性 (`'_'`要么`'*'`,默认`'*'`) . 

###### `options.emphasis`

标记用于强调 (`'_'`要么`'*'`,默认`'_'`) . 

### `stringify.Compiler`

访问原始[编译器][],如果你需要它. 

## 扩展编译器

如果使用此插件,则会添加一个[`编译器`][compiler]构造函数`处理器`. 其他插件可以更改并在编译器原型上添加访问者,以更改markdown的字符串化方式. 

下面的插件修改了一个[游客][]在二级标题之前添加一个额外的空白行. 

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

### `编译器#游客`

对象映射[节点][]类型[`游客`][visitor]秒. 

### `函数访问者 (node [,parent]) `

字符串化`节点`. 

###### 参数

-   `节点` ([`节点`][node])  - 要编译的节点
-   `亲` ([`节点`][node],可选)  - 父母`节点`

###### 返回

`串`,编译给出`节点`. 

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
