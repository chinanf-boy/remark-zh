![remark][logo]

# 入门

**remark**转换 markdown. 这是一个[插件][plugins]生态系统. 如果你被卡住了,[问题][issues]和[Gitter]是获得帮助的好地方.

它是建立在[unified]请务必阅读它和它的[网站][website]也是.

## 目录

<!-- START doctoc -->
<!-- END doctoc -->

## 介绍

让我们浮于表面先,**remark**转换 markdown 的过程: markdown, 重新格式化,和 复写:

```md
# Alpha

Bravo charlie **delta** **echo**.

- Foxtrot

* Golf

- Hotel
```

输出:

```md
# Alpha

Bravo charlie **delta** **echo**.

- Foxtrot
- Golf
- Hotel
```

但是,可以做得更多,[通过插件][plugins].

## 命令行

**remark 的**CLI 是从命令行处理 md 文件的一种简单方法. 它的接口由[**unified-args**][unified-args]提供.

安装[`remark-cli`][cli]和依赖关系 (在这种情况下 [lint 预置][preset]和[`remark-HTML`][html]),通过[npm][]:

```sh
npm install --global remark-cli remark-html remark-preset-lint-markdown-style-guide
```

`readme.md`包含:

```md
_Hello_.
```

现在,要处理`readme.md`运行以下内容:

```sh
remark readme.md --use html --use preset-lint-markdown-style-guide
```

输出:

```txt
<p><em>Hello</em>.</p>
readme.md.md
  1:1-1:8  warning  Emphasis should use `*` as a marker  emphasis-marker  remark-lint

⚠ 1 warning
```

## 在项目中使用 remark

在前面的示例中,`remark-cli`安装在全局. 这通常是个馊主意. 在这里,我们将使用 CLI 来处理 NPM 包.

我们有以下`packgaes`:

```json
{
  "name": "my-package",
  "version": "1.0.0",
  "scripts": {
    "test": "node test.js"
  }
}
```

安装`remark-cli`,`remark-html`和`preset-lint-markdown-style-guide`作为 DEV 依赖项进入:

```sh
npm install --save-dev remark-cli remark-html remark-preset-lint-markdown-style-guide
```

这个`--save-dev`选项存储在我们的`packages.json`的开发依赖中:

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

然后,我们改变我们`测试`脚本,包括 remark 和 添加配置:

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

这将在测试项目时,将所有的 md 文件都记录下来. [`--frail`{脆弱}}}][frail]如果发现违反代码风格,则确保命令失败;[`--quiet`{安静}][quiet]隐藏报告中的成功文件.

## 程序使用

编程接口**remark**是由[**unified**][unified]. 事实上,[`remark`][api]是两个插件: [`remark-parse`][parse]和[`remark-stringify`][stringify].

> 像极了`JSON` 

安装[`remark`][api]和依赖关系, 通过[npm][]:

```sh
npm install vfile-reporter remark remark-html remark-preset-lint-markdown-style-guide
```

`index.js`包含:

```js
var remark = require('remark');
var styleGuide = require('remark-preset-lint-markdown-style-guide');
var html = require('remark-html');
var report = require('vfile-reporter');

remark()
  .use(styleGuide)
  .use(html)
  .process('_Hello_.', function(err, file) {
    console.error(report(err || file));
    console.log(String(file));
  });
```

`node index.js`输出:

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
[api]: https://github.com/chinanf-boy/remark-zh/tree/master/packages/remark
[cli]: https://github.com/chinanf-boy/remark-zh/tree/master/packages/remark-cli
[plugins]: https://github.com/chinanf-boy/remark-zh/tree/master/doc/plugins.zh.md
[unified]: https://github.com/unifiedjs/unified
[website]: https://unifiedjs.github.io
[unified-args]: https://github.com/unifiedjs/unified-args
[frail]: https://github.com/unifiedjs/unified-args#--frail
[quiet]: https://github.com/unifiedjs/unified-args#--quiet
[parse]: https://github.com/chinanf-boy/remark-zh/tree/master/packages/remark-parse
[stringify]: https://github.com/chinanf-boy/remark-zh/tree/master/packages/remark-stringify
[preset]: https://github.com/remarkjs/remark-lint/tree/master/packages/remark-preset-lint-markdown-style-guide
[html]: https://github.com/remarkjs/remark-html
