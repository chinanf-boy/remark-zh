
![remark][logo]

# 入门

**评论**转换标记. 这是一个生态系统[插件][]. 如果你被卡住了,[问题][]和[吉特][]是获得帮助的好地方. 

它是建立在[统一的][]请务必阅读它和它的[网站][]也是. 

## 目录表

-   [介绍](#introduction)
-   [命令行](#command-line)
-   [在项目中使用备注](#using-remark-in-a-project)
-   [程序使用](#programmatic-usage)

## 介绍

走出盒子,**评论**转换标记: 降价,重新格式化,和写: 

```md
# Alpha #
Bravo charlie **delta** __echo__.
- Foxtrot
*  Golf
+ Hotel
```

产量: 

```md
# Alpha

Bravo charlie **delta** **echo**.

-   Foxtrot
-   Golf
-   Hotel
```

但是,可以做得更多,[通过插件][plugins].

## 命令行

**评论**CLI是从命令行处理标记文件的一种简单方法. 它的接口由[**统一ARG**][unified-args].

安装[`评论CLI`][cli]和依赖关系 (在这种情况下) [衬垫预置][preset]和[`注释HTML`][html]用[npm][]: 

```sh
npm install --global remark-cli remark-html remark-preset-lint-markdown-style-guide
```

`读数`包含: 

```md
_Hello_.
```

现在,要处理`读数`运行以下内容: 

```sh
remark readme.md --use html --use preset-lint-markdown-style-guide
```

产量: 

```txt
<p><em>Hello</em>.</p>
readme.md.md
  1:1-1:8  warning  Emphasis should use `*` as a marker  emphasis-marker  remark-lint

⚠ 1 warning
```

## 在项目中使用备注

在前面的示例中,`评论CLI`安装在全球范围内. 这通常是个馊主意. 在这里,我们将使用CLI来处理NPM包. 

说我们有以下`包装袋`: 

```json
{
  "name": "my-package",
  "version": "1.0.0",
  "scripts": {
    "test": "node test.js"
  }
}
```

安装`评论CLI`,`注释HTML`和`预置皮棉降价风格指南`作为DEV依赖项进入: 

```sh
npm install --save-dev remark-cli remark-html remark-preset-lint-markdown-style-guide
```

这个`ℴℴ保存DeV`选项存储我们的依赖项`包装袋`: 

```diff
 {
   "name": "my-package",
   "version": "1.0.0",
+  "devDependencies": {
+    "remark-cli": "^3.0.0",
+    "remark-html": "^6.0.0",
+    "remark-preset-lint-markdown-style-guide": "^1.0.0"
+  },
   "scripts": {
     "test": "node test.js"
   }
 }
```

然后,我们改变我们`测试`脚本包括注释和添加配置: 

```diff
 {
   "name": "my-package",
   "version": "1.0.0",
   "devDependencies": {
     "remark-cli": "^3.0.0",
     "remark-html": "^6.0.0",
     "remark-preset-lint-markdown-style-guide": "^1.0.0"
   },
   "scripts": {
-    "test": "node test.js"
+    "test": "remark . --quiet --frail && node test.js"
+  },
+  "remarkConfig": {
+    "plugins": [
+      "preset-lint-markdown-style-guide",
+      "html"
+    ]
   }
 }
```

现在我们可以从命令行运行: 

```sh
npm test
```

这将在测试项目时将所有的标记文件都记录下来. [`--脆弱`][frail]如果发现代码风格违反,则确保命令失败;[`--安静`][quiet]隐藏报告中的成功文件. 

## 程序使用

编程接口**评论**是由[**统一的**][unified].  事实上,[`评论`][api]是两个插件: [`备注解析`][parse]和[`论纲`][stringify].

安装[`评论`][api]和依赖关系[npm][]: 

```sh
npm install vfile-reporter remark remark-html remark-preset-lint-markdown-style-guide
```

`索引文件`包含: 

```js
var remark = require('remark');
var styleGuide = require('remark-preset-lint-markdown-style-guide');
var html = require('remark-html');
var report = require('vfile-reporter');

remark()
  .use(styleGuide)
  .use(html)
  .process('_Hello_.', function (err, file) {
    console.error(report(err || file));
    console.log(String(file));
  });
```

`节点索引`产量: 

```txt
  1:1-1:8  warning  Emphasis should use `*` as a marker  emphasis-marker  remark-lint

⚠ 1 warning
<p><em>Hello</em>.</p>
```

<!-- Definitions -->

[logo]: https://cdn.rawgit.com/remarkjs/remark/ee78519/logo.svg

[issues]: https://github.com/remarkjs/remark/issues

[gitter]: https://gitter.im/remarkjs/remark

[npm]: https://docs.npmjs.com/cli/install

[api]: https://github.com/remarkjs/remark/tree/master/packages/remark

[cli]: https://github.com/remarkjs/remark/tree/master/packages/remark-cli

[plugins]: https://github.com/remarkjs/remark/tree/master/doc/plugins.md

[unified]: https://github.com/unifiedjs/unified

[website]: https://unifiedjs.github.io

[unified-args]: https://github.com/unifiedjs/unified-args

[frail]: https://github.com/unifiedjs/unified-args#--frail

[quiet]: https://github.com/unifiedjs/unified-args#--quiet

[parse]: https://github.com/remarkjs/remark/tree/master/packages/remark-parse

[stringify]: https://github.com/remarkjs/remark/tree/master/packages/remark-stringify

[preset]: https://github.com/remarkjs/remark-lint/tree/master/packages/remark-preset-lint-markdown-style-guide

[html]: https://github.com/remarkjs/remark-html
