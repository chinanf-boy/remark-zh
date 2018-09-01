
# 此言-解析[![Build Status][build-badge]][build-status] [![Coverage Status][coverage-badge]][coverage-status] [![Chat][chat-badge]][chat]

[分析器][]对于[**统一**][unified]. 解析降价[**MDAST**][mdast]语法树. 用于[**备注**处理器][processor]. 可[扩展][extend]改变如何解析降价. 

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

-   [API](#api)
    -   [processor.use (解析\[,选项\]) ](#processoruseparse-options)
    -   [parse.Parser](#parseparser)
-   [扩展解析器](#extending-the-parser)
    -   [解析器#blockTokenizers](#parserblocktokenizers)
    -   [解析器#blockMethods](#parserblockmethods)
    -   [解析器#inlineTokenizers](#parserinlinetokenizers)
    -   [解析器#inlineMethods](#parserinlinemethods)
    -   [函数标记器 (吃,值,沉默) ](#function-tokenizereat-value-silent)
    -   [tokenizer.locator (value,fromIndex) ](#tokenizerlocatorvalue-fromindex)
    -   [吃 (子值) ](#eatsubvalue)
    -   [添加 (节点\[,父母\]) ](#addnode-parent)
    -   [add.test () ](#addtest)
    -   [add.reset (节点\[,父母\]) ](#addresetnode-parent)
    -   [关闭标记器](#turning-off-a-tokenizer)
-   [执照](#license)

## API

### `processor.use (parse [,options]) `

配置`处理器`读取降价作为输入和处理[**MDAST**][mdast]语法树. 

##### `选项`

选项直接传递,或稍后传递[`processor.data () `][data]. 

##### `options.gfm`

```md
hello ~~hi~~ world
```

GFM模式 (`布尔`,默认: `真正`)  打开: 

-   [受控代码块](https://help.github.com/articles/github-flavored-markdown/#fenced-code-blocks)
-   [自动链接网址](https://help.github.com/articles/github-flavored-markdown/#url-autolinking)
-   [删除 (删除线) ](https://help.github.com/articles/github-flavored-markdown/#strikethrough)
-   [任务列表](https://help.github.com/articles/writing-on-github/#task-lists)
-   [表](https://help.github.com/articles/github-flavored-markdown/#tables)

##### `options.commonmark`

```md
This is a paragraph
    and this is also part of the preceding paragraph.
```

CommonMark模式 (`布尔`,默认: `假`) 允许: 

-   用于分割块引用的空行
-   括号  (` (`和`) `) 链接和图像标题
-   任何逃脱[ASCII标点符号][escapes]字符
-   结束括号 (`) `) 作为有序列表标记
-   blockquotes中的URL定义 (以及启用时的脚注) 

CommonMark模式不允许: 

-   直接在段落后面的代码
-   ATX标题 (`#哈希标题`) 打开哈希后或关闭哈希值之前没有间距
-   Setext标题 (`下划线标题\ n ---`) 当遵循一个段落
-   链接和图像标题中的换行符
-   链接中的空格和自动链接中的图像URL (括号中的链接,`<`和`>`) 
-   懒惰的blockquote延续,行前面没有一个闭合角括号 (`>`) ,用于列表,代码和thematicBreak

##### `options.footnotes`

```md
Something something[^or something?].

And something else[^1].

[^1]: This reference footnote contains a paragraph...

    * ...and a list
```

脚注模式 (`布尔`,默认: `假`) 启用参考脚注和内联脚注. 两者都用方括号包裹,前面有一个插入符号 (`^`) ,可以从其他脚注中引用. 

##### `options.blocks`

```md
<block>foo
</block>
```

块 (`阵列. <字符串>`,默认: 列表[阻止HTML元素][blocks]暴露让我们的用户定义块级HTML元素. 

##### `options.pedantic`

```md
Check out some_file_name.txt
```

迂腐模式 (`布尔`,默认: `假`)  打开: 

-   重点  (`_α_`) 和重要性 (`__bravo__`用词语下划线
-   带有不同标记的无序列表 (`*`,`-`,`+`) 
-   如果`commonmark`也打开了,带有不同标记的有序列表 (`. `,`) `) 
-   而迂腐模式删除列表项中较少的空格 (最多四个,而不是整个缩进) 

### `parse.Parser`

访问[解析器][],如果你需要它. 

## 扩展解析器

大多数情况下,使用变换器来操作语法树会产生所需的输出. 有时,主要是在引入具有一定优先级的新语法实体时,需要与解析器连接. 

如果`此言-解析`使用插件,它添加了一个[`分析器`][parser]构造函数`处理器`. 其他插件可以将解析器添加到解析器的原型中,以更改解析markdown的方式. 

下面的插件添加了一个[标记生成器][]用于提及. 

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

### `解析器#blockTokenizers`

对象映射标记生成器的名称[标记生成器][]秒. 这些标记器 (例如: `fencedCode`,`表`,和`段`) 从一个值开始吃到一个行结束. 

看到`#blockMethods`下面列出了默认包含的方法列表. 

### `解析器#blockMethods`

数组`blockTokenizers`名字 (`串`) 指定它们运行的​​顺序. 

<!--methods-block start-->

-   `新队`
-   `indentedCode`
-   `fencedCode`
-   `块引用`
-   `atxHeading`
-   `thematicBreak`
-   `名单`
-   `setextHeading`
-   `html`
-   `脚注`
-   `定义`
-   `表`
-   `段`

<!--methods-block end-->

### `解析器#inlineTokenizers`

对象映射标记生成器的名称[标记生成器][]秒. 这些标记器 (例如: `网址`,`参考`,和`重点`) 从价值的开始吃. 为了提高性能,他们依赖于[定位器][]秒. 

看到`#inlineMethods`下面列出了默认包含的方法列表. 

### `解析器#inlineMethods`

数组`inlineTokenizers`名字 (`串`) 指定它们运行的​​顺序. 

<!--methods-inline start-->

-   `逃逸`
-   `自动链接`
-   `网址`
-   `html`
-   `链接`
-   `参考`
-   `强大`
-   `重点`
-   `缺失`
-   `码`
-   `打破`
-   `文本`

<!--methods-inline end-->

### `函数标记器 (吃,值,沉默) `

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

解析器知道两种类型的标记化器: 块级别和内联级别. 块级标记器与内联级别标记器相同,但后者必须具有[定位器][]. 

断词*测试*文档是否以某个语法实体开头. 在*无声*模式,他们返回该测试是否通过. 在*正常*模式,他们消耗该令牌,这个过程被称为"吃". 定位器通过提供有关下一个实体可能发生位置的信息,使标记器能够更快地运行. 

###### 签名

-   `节点?= tokenizer (吃,值) `
-   `布尔?= tokenizer (吃,价值,沉默) `

###### 参数

-   `吃` ([`功能`][eat])  - 在适用的情况下吃一个实体
-   `值` (`串`)  - 可能启动实体的价值
-   `无声` (`布尔`,可选)  - 是否检测或消费

###### 属性

-   `定位器` ([`功能`][locator])  - 内联标记生成器必需
-   `onlyAtStart` (`布尔`)  - 是否只能在文档的开头找到节点
-   `notInBlock` (`布尔`)  - 节点是否不能位于块引用,列表或脚注定义中
-   `notInList` (`布尔`)  - 节点是否不在列表中
-   `notInLink` (`布尔`)  - 节点是否不能在链接中

###### 返回

-   在*无声*模式,是否可以在开始时找到节点`值`
-   在*正常*模式,一个节点,如果它可以在开始时找到`值`

### `tokenizer.locator (value,fromIndex) `

```js
function locateMention(value, fromIndex) {
  return value.indexOf('@', fromIndex);
}
```

内联标记化需要定位器以保持过程的性能. 定位器通过提供有关下一个实体发生位置的信息,使内联标记生成器能够更快地运行. 定位器可能是错误的,如果在它们返回的索引中实际上没有找到节点,则可以,但它们必须跳过任何节点. 

###### 参数

-   `值` (`串`)  - 可能包含实体的值
-   `的fromIndex` (`数`)  - 开始搜索的位置

###### 返回

实体可以开始的指数,和`-1`除此以外. 

### `吃 (子值) `

```js
var add = eat('foo');
```

吃`子值`,这是一个字符串在开头[令牌化][tokenizer]d`值` (跟踪以确保食用正确的值) . 

###### 参数

-   `子值` (`串`)  - 吃的价值. 

###### 返回

[`加`][add]. 

### `add (node [,parent]) `

```js
var add = eat('foo');
add({type: 'text', value: 'foo'});
```

加[位置信息][location]至`节点`并将其添加到`亲`. 

###### 参数

-   `节点` ([`节点`][node])  - 节点到补丁位置和插入
-   `亲` ([`节点`][node],可选)  - 添加的地方`节点`在语法树中. 默认为当前处理的节点

###### 返回

给定的`节点`. 

### `add.test () `

得到[位置信息][location]这将被修补`节点`通过`加`. 

###### 返回

[`位置`][location]. 

### `add.reset (node [,parent]) `

`加`,但重置内部位置. 例如在列表中很有用,其中相同的内容首先用于列表,稍后用于列表项

###### 参数

-   `节点` ([`节点`][node])  - 节点到补丁位置和插入
-   `亲` ([`节点`][node],可选)  - 添加的地方`节点`在语法树中. 默认为当前处理的节点

###### 返回

给定的`节点`. 

### 关闭标记器

在极少数情况下,您可能需要关闭标记生成器以避免解析该语法功能. 这可以通过从Parser中删除tokenizer来完成`blockTokenizers` (要么`blockMethods`)  要么`inlineTokenizers` (要么`inlineMethods`) . 

以下示例关闭缩进的代码块: 

```js
delete remarkParse.Parser.prototype.blockTokenizers.indentedCode;
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
