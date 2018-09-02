
# remark-parse [![Build Status][build-badge]][build-status] [![Coverage Status][coverage-badge]][coverage-status] [![Chat][chat-badge]][chat]

[**unified**][unified]的[解析器][Parser]. 解析markdown到一个[**MDAST**][mdast]语法树. 用于[**remark**处理器][processor]. 可[扩展][extend]改变解析markdown的过程. 

## 安装

[npm][]: 

```sh
npm install remark-parse
```

## 用法

```js
var unified = require('unified');
var createStream = require('unified-stream');
var markdown = require('remark-parse');
var html = require('remark-html');

var processor = unified()
  .use(markdown, {commonmark: true})
  .use(html)

process.stdin
  .pipe(createStream(processor))
  .pipe(process.stdout);
```

## 目录

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [API](#api)
  - [`processor.use(parse[, options])`](#processoruseparse-options)
      - [`options`](#options)
      - [`options.gfm`](#optionsgfm)
      - [`options.commonmark`](#optionscommonmark)
      - [`options.footnotes`](#optionsfootnotes)
      - [`options.blocks`](#optionsblocks)
      - [`options.pedantic`](#optionspedantic)
  - [`parse.Parser`](#parseparser)
- [扩展解析器](#%E6%89%A9%E5%B1%95%E8%A7%A3%E6%9E%90%E5%99%A8)
  - [`Parser#blockTokenizers`](#parserblocktokenizers)
  - [`Parser#blockMethods`](#parserblockmethods)
  - [`Parser#inlineTokenizers`](#parserinlinetokenizers)
  - [`Parser#inlineMethods`](#parserinlinemethods)
  - [`function tokenizer(eat, value, silent)`](#function-tokenizereat-value-silent)
        - [类型定义](#%E7%B1%BB%E5%9E%8B%E5%AE%9A%E4%B9%89)
        - [参数](#%E5%8F%82%E6%95%B0)
        - [属性](#%E5%B1%9E%E6%80%A7)
        - [Returns](#returns)
  - [`tokenizer.locator(value, fromIndex)`](#tokenizerlocatorvalue-fromindex)
        - [参数](#%E5%8F%82%E6%95%B0-1)
        - [Returns](#returns-1)
  - [`eat(subvalue)`](#eatsubvalue)
        - [参数](#%E5%8F%82%E6%95%B0-2)
        - [Returns](#returns-2)
  - [`add(node[, parent])`](#addnode-parent)
        - [参数](#%E5%8F%82%E6%95%B0-3)
        - [Returns](#returns-3)
  - [`add.test()`](#addtest)
        - [Returns](#returns-4)
  - [`add.reset(node[, parent])`](#addresetnode-parent)
        - [参数](#%E5%8F%82%E6%95%B0-4)
        - [Returns](#returns-5)
  - [关闭标记器](#%E5%85%B3%E9%97%AD%E6%A0%87%E8%AE%B0%E5%99%A8)
- [执照](#%E6%89%A7%E7%85%A7)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## API

### `processor.use(parse[, options])`

配置`processor`,读取markdown作为输入和处理[**MDAST**][mdast]语法树. 

##### `options`

选项直接传递,或稍后由[`processor.data()`][data]传递. 

##### `options.gfm`

```md
hello ~~hi~~ world
```

GFM模式 (`boolean`,默认: `true`)  打开: 

-   [Fenced code blocks](https://help.github.com/articles/github-flavored-markdown/#fenced-code-blocks)
-   [Autolinking of URLs](https://help.github.com/articles/github-flavored-markdown/#url-autolinking)
-   [Deletions (strikethrough)](https://help.github.com/articles/github-flavored-markdown/#strikethrough)
-   [Task lists](https://help.github.com/articles/writing-on-github/#task-lists)
-   [Tables](https://help.github.com/articles/github-flavored-markdown/#tables)

##### `options.commonmark`

```md
This is a paragraph
    and this is also part of the preceding paragraph.
```

CommonMark模式 (`boolean`,默认: `false`) **允许**: 

-   用于分割块引用的空行
-   括号  (`(`和`)`) 链接和图像标题
-   任何超出[ASCII标点符号][escapes]字符
-   结束括号 (`)`) 作为有序列表标记
-   区块中的URL定义 (以及启用时的脚注) 

CommonMark模式**禁止**: 

-   直接在段落后面的代码行
-   ATX标题 (`# Hash headings`) 打开哈希后或关闭哈希值之前,没有间距
-   Setext标题 (`Underline headings\n---`) 当遵循一个段落
-   链接和图像标题中的换行符
-   链接中的空格和自动链接中的图像URL (括号中的链接,`<`和`>`) 
-   懒惰的块延续,行没有一个闭合括号 (`>`),用于列表,代码和thematicBreak

##### `options.footnotes`

```md
Something something[^or something?].

And something else[^1].

[^1]: This reference footnote contains a paragraph...

    * ...and a list
```

脚注模式 (`boolean`,默认: `false`) 启用参考脚注和内联脚注. 两者都用方括号包裹,前面有一个插入符号 (`^`) ,可以从其他脚注中引用. 

##### `options.blocks`

```md
<block>foo
</block>
```

块 (`Array.<string>`,默认: [HTML块元素][blocks]的列表) 让我们的用户定义块级HTML元素. 

##### `options.pedantic`

```md
Check out some_file_name.txt
```

pedantic模式 (`boolean`,默认: `false`)  若打开: 

-   重点{`Emphasis`}  (`_alpha_`) 和 重要性{`importance`} (`__bravo__`用下划线
-   无序列表带有不同标记 (`*`,`-`,`+`) 
-   如果`commonmark`也打开了,有序列表带有不同标记 (`.`,`)`) 
-   而 pedantic模式 删除列表项中较少的空格 (最多四个,而不是整个缩进) 

### `parse.Parser`

访问[解析器][Parser],如果你需要它. 

## 扩展解析器

大多数情况下,使用 transformers-器 来操作语法树会产生所需的输出. 有时,主要是在引入具有一定优先级的新语法实体时,需要与解析器连接. 

如果`remark-parse`插件被使用,它添加了一个[`Parser`][parser]构造函数`processor`. 其他插件可以将解析器,添加到解析器的原型中,以更改解析markdown的方式. 

下面的插件添加了一个[tokenizer][tokenizer]用于提及. 

```js
module.exports = mentions;

function mentions() {
  var Parser = this.Parser;
  var tokenizers = Parser.prototype.inlineTokenizers;
  var methods = Parser.prototype.inlineMethods;

  /* Add an inline tokenizer (defined in the following example). */
  tokenizers.mention = tokenizeMention;

  /* Run it just before `text`. */
  methods.splice(methods.indexOf('text'), 0, 'mention');
}
```

### `Parser#blockTokenizers`

一个对象将 tokenizer 的名称 映射到 [tokenizer][tokenizer]们. 这些tokenizers (例如: `fencedCode`,`table`,和`paragraph`) 会从第一个值开始 吃 到一个行结束. 

看到`#blockMethods`下面列出了默认包含的方法列表. 

### `Parser#blockMethods`

`blockTokenizers`名字数组 (`string`) ,指定了它们运行的​​顺序. 

<!--methods-block start-->

-   `newline`
-   `indentedCode`
-   `fencedCode`
-   `blockquote`
-   `atxHeading`
-   `thematicBreak`
-   `list`
-   `setextHeading`
-   `html`
-   `footnote`
-   `definition`
-   `table`
-   `paragraph`

<!--methods-block end-->

### `Parser#inlineTokenizers`

一个对象将 tokenizer的名称 映射到[tokenizer][tokenizer]们. 这些tokenizers (例如: `url`,`reference`,和`emphasis`) 从第一个值开始吃. 为了提高性能,他们依赖于[定位器][locator]们. 

看到`#inlineMethods`下面列出了默认包含的方法列表. 

### `Parser#inlineMethods`

`inlineTokenizers`名字数组 (`string`) ,指定了它们运行的​​顺序. 

<!--methods-inline start-->

-   `escape`
-   `autoLink`
-   `url`
-   `html`
-   `link`
-   `reference`
-   `strong`
-   `emphasis`
-   `deletion`
-   `code`
-   `break`
-   `text`

<!--methods-inline end-->

### `function tokenizer(eat, value, silent)`

```js
tokenizeMention.notInLink = true;
tokenizeMention.locator = locateMention;

function tokenizeMention(eat, value, silent) {
  var match = /^@(\w+)/.exec(value);

  if (match) {
    if (silent) {
      return true;
    }

    return eat(match[0])({
      type: 'link',
      url: 'https://social-network/' + match[1],
      children: [{type: 'text', value: match[0]}]
    });
  }
}
```

解析器知道两种类型的标记化器: 块级别和内联级别. 块级标记器与内联级别标记器相同,但后者必须具有[定位器][locator]. 

Tokenizers的*测试*: 文档是否以某个语法实体开头. 在*无声*模式,他们返回该测试是否通过. 在*正常*模式,他们消耗该token,这个过程被称为"吃". 定位器通过提供有关下一个实体可能发生位置的信息,使标记器能够更快地运行. 

###### 类型定义

-   `Node? = tokenizer(eat, value)`
-   `boolean? = tokenizer(eat, value, silent)`

###### 参数

-   `eat` ([`Function`][eat])  - 在适用的情况下吃一个实体
-   `value` (`string`)  - 可能启动的实体的值
-   `silent` (`boolean`,可选)  - 无声或正常模式

###### 属性

-   `locator` ([`Function`][locator])  - 内联tokenizer必需
-   `onlyAtStart` (`boolean`)  - 是否只能在文档的开头找到节点
-   `notInBlock` (`boolean`)  - 节点是否不能位于块引用,列表或脚注定义中
-   `notInList` (`boolean`)  - 节点是否不在列表中
-   `notInLink` (`boolean`)  - 节点是否不能在链接中

###### Returns

-   在*无声*模式,是否可以在开始时找到节点`value`:`Boolean`
-   在*正常*模式,一个节点,如果它可以在开始时找到`value`:`Node`

### `tokenizer.locator(value, fromIndex)`

```js
function locateMention(value, fromIndex) {
  return value.indexOf('@', fromIndex);
}
```

内联标记化需要定位器以保持过程的性能. 定位器通过提供有关下一个实体发生位置的信息,使内联tokenizer能够更快地运行. 

定位器可能是错误的,例如:如果在它们返回的索引中,实际上没有找到节点.有一点要注意:它们必须跳过任意的节点. 

###### 参数

-   `value` (`string`)  - 可能包含实体的值
-   `fromIndex` (`number`)  - 开始搜索的位置

###### Returns

实体可以开始的索引数,否则`-1`. 

### `eat(subvalue)`

```js
var add = eat('foo');
```

吃`subvalue`,这是在[tokenized][tokenizer]开头的一个字符串`value` (跟踪以确保食用正确的值) . 

###### 参数

-   `subvalue` (`string`)  - 吃的值. 

###### Returns

[`add`][add]. 

### `add(node[, parent])`

```js
var add = eat('foo');
add({type: 'text', value: 'foo'});
```

add[位置信息][location]到`node`,将其添加到`parent`. 

###### 参数

-   `node` ([`Node`][node])  - 节点的位置和插入内容
-   `parent` ([`Node`][node],可选)  - 在语法树中添加`node`的地方. 默认为当前处理的节点

###### Returns

给定的`node`. 

### `add.test()`

得到[位置信息][location],这是通过`add`修补到`node`的那个. 

###### Returns

[`Location`][location]. 

### `add.reset(node[, parent])`

`add`,但重置内部位置. 例如在列表中很有用,其中相同的内容首先用于 列表,稍后用于 列表项

###### 参数

-   `node` ([`Node`][node])  - 节点的位置和插入内容
-   `parent` ([`Node`][node],可选)  - 在语法树中添加`node`的地方. 默认为当前处理的节点

###### Returns

给定的`node`. 

### 关闭标记器

在极少数情况下,您可能需要关闭tokenizer以避免解析该语法功能. 这可以 从你`Parser`的`blockTokenizers` (或者`blockMethods`) 或者`inlineTokenizers` (或者`inlineMethods`)中删除tokenizer来完成 . 

以下示例关闭缩进的代码块: 

```js
delete remarkParse.Parser.prototype.blockTokenizers.indentedCode;
```

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

[data]: https://github.com/unifiedjs/unified#processordatakey-value

[processor]: https://github.com/remarkjs/remark/blob/master/packages/remark

[mdast]: https://github.com/syntax-tree/mdast

[escapes]: http://spec.commonmark.org/0.25/#backslash-escapes

[node]: https://github.com/syntax-tree/unist#node

[location]: https://github.com/syntax-tree/unist#location

[parser]: https://github.com/unifiedjs/unified#processorparser

[extend]: #extending-the-parser

[tokenizer]: #function-tokenizereat-value-silent

[locator]: #tokenizerlocatorvalue-fromindex

[eat]: #eatsubvalue

[add]: #addnode-parent

[blocks]: https://github.com/remarkjs/remark/blob/master/packages/remark-parse/lib/block-elements.json
