
![remark][logo]

# 插件

**remark**是一个[插件][plugins]生态系统. 

看下[使用remark构建的工具»][products]. 

> `Rehype` 是另一个 html 解析的插件生态系统

## 目录

<!-- START doctoc -->
<!-- END doctoc -->

## 插件列表

有个好插件的主意吗? 让我们[聊][gitter]下,并实现它!

-   [`remark-abbr`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-abbr)- 用于处理缩写的自定义语法,自定义mdast内联节点类型`abbr`. rehype 兼容 (`<abbr title="bar">foo</abbr>`) 
-   [`remark-align`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-align)- 自定义语法来处理文本/块对齐,自定义mdast块节点类型`CenterAligned`,`RightAligned`. rehype 兼容 (包装可配置的CSS类,对齐`div`标签,) 
-   [`remark-attr`](https://github.com/arobase-che/remark-attr)- 添加对markdown的自定义属性的支持
-   [`remark-autolink-headings`](https://github.com/ben-eb/remark-autolink-headings)- 自动将GitHub样式链接添加到标题
-   [`remark-bookmarks`](https://github.com/ben-eb/remark-bookmarks)-  Markdown文件的链接管理器
-   [`remark-bracketed-spans`](https://github.com/sethvincent/remark-bracketed-spans)- 添加id,class和data属性到`<span>`标签,在markdown
-   [`remark-breaks`](https://github.com/remarkjs/remark-breaks)- 添加换行符,无需空格
-   [`remark-collapse`](https://github.com/Rokt33r/remark-collapse)- 使一个section可折叠
-   [`remark-comment-blocks`](https://github.com/ben-eb/remark-comment-blocks)- 使用注释块包装Markdown
-   [`remark-comment-config`](https://github.com/remarkjs/remark-comment-config)- 使用注释配置remark
-   [`remark-comments`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-comments)- 可配置的自定义语法,用于忽略Markdown输入的部分内容
-   [`remark-contributors`](https://github.com/hughsk/remark-contributors)- 注入给定的贡献者表
-   [`remark-custom-blocks`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-custom-blocks)- 可配置的自定义语法,用于解析自定义块,创建新的mdast节点类型. Rehype兼容
-   [`remark-defsplit`](https://github.com/eush77/remark-defsplit)- 将内联链接和图像目标提取为单独的定义
-   [`remark-disable-tokenizers`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-disable-tokenizers)- 禁用remark任何或所有`blockTokenizers`和`inlineTokenizers`
-   [`remark-embed-images`](https://github.com/dherges/remark-embed-images)- 使用数据嵌入图像: URIs, 内联base64编码的源
-   [`remark-emoji`](https://github.com/rhysd/remark-emoji)- 将unicode表情符号转换为Gemoji短代码
-   [`remark-emoji-to-gemoji`](https://github.com/jackycute/remark-emoji-to-gemoji)- 将Gemoji短代码转换为unicode表情符号
-   [`remark-external-links`](https://github.com/xuopled/remark-external-links)- 自动将target和rel属性添加到外部链接
-   [`remark-first-heading`](https://github.com/laat/remark-first-heading)- 替换文档中的第一个标题
-   [`remark-fix-guillemets`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-fix-guillemets)- 出于奇怪的排版原因,这个修复了`<<a>>`被解析为`<`+ html标签`<a>`+`>`而不是用文本`<<a>>`
-   [`remark-frontmatter`](https://github.com/remarkjs/remark-frontmatter)-  Frontmatter (yaml,toml等) 支持
-   [`remark-gemoji`](https://github.com/remarkjs/remark-gemoji)- remark中的Gemoji短代码支持
-   [`remark-gemoji-to-emoji`](https://github.com/jackycute/remark-gemoji-to-emoji)- 将Gemoji短代码转换为Unicode表情符号
-   [`remark-generic-extensions`](https://github.com/medfreeman/remark-generic-extensions)-  Commonmark通用指令扩展
-   [`remark-github`](https://github.com/remarkjs/remark-github)- 自动链接引用,如GitHub问题,PR和注释
-   [`remark-gitlab-artifact`](https://github.com/temando/remark-gitlab-artifact)- 从GitLab项目下载artifacts,与Markdown一起生活
-   [`remark-grid-tables`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-grid-tables)- 自定义Markdown语法,描述表格. Rehype兼容
-   [`remark-graphviz`](https://github.com/temando/remark-graphviz)- 替换`dot`带有渲染SVG的图形
-   [`remark-heading-gap`](https://github.com/ben-eb/remark-heading-gap)- 调整标题之间的差距
-   [`remark-highlight.js`](https://github.com/ben-eb/remark-highlight.js)- 突出显示Markdown文件中的代码块[highlight.js](https://github.com/isagalaev/highlight.js)
-   [`remark-html`](https://github.com/remarkjs/remark-html)- 编译Markdown到HTML文档
-   [`remark-html-emoji-image`](https://github.com/jackycute/remark-html-emoji-image)- 将unicode表情符号转换为HTML图像
-   [`remark-html-katex`](https://github.com/rokt33r/remark-math/blob/master/packages/remark-html-katex/readme.md)- 将数学内联和块节点转换为[KaTeX](https://github.com/Khan/KaTeX)样式的HTML方程式
-   [`remark-iframes`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-iframes)- 采用白名单方法,具有完全可配置的iframe提供程序的自定义语法. Rehype兼容
-   [`remark-inline-links`](https://github.com/remarkjs/remark-inline-links)- 将引用和定义转换为普通链接和图像
-   [`remark-inline-math`](https://github.com/bizen241/remark-inline-math)- 内联数学支持
-   [`remark-kbd`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-kbd)- 自定义语法,解析`||foo||`成一个新的mdast内联节点类型`kbd`. rehype 兼容 (`<kbd>foo</kbd>`) 
-   [`remark-license`](https://github.com/remarkjs/remark-license)- 添加许可证部分
-   [`remark-lint`](https://github.com/remarkjs/remark-lint)-  Markdown代码样式linter
-   [`remark-man`](https://github.com/remarkjs/remark-man)- 编译 markdow 到 Man页面 (roff) 
-   [`remark-math`](https://github.com/rokt33r/remark-math)- 数学内联和块支持
-   [`remark-mermaid`](https://github.com/temando/remark-mermaid)- 替换[mermaid](https://mermaidjs.github.io/)渲染SVG的图形
-   [`remark-message-control`](https://github.com/remarkjs/remark-message-control)- 启用,禁用和忽略消息
-   [`remark-metadata`](https://github.com/temando/remark-metadata)- 添加有关已处理文件的元数据以作前端使用
-   [`remark-midas`](https://github.com/ben-eb/remark-midas)- 使用[midas](https://github.com/ben-eb/midas)突出显示Markdown文件中的CSS
-   [`remark-normalize-headings`](https://github.com/eush77/remark-normalize-headings)- 确保文档中最多只有一个顶级标题
-   [`remark-openapi`](https://github.com/temando/remark-openapi)- 将本地或远程OpenAPI定义的链接转换为,包含所有路径摘要的表
-   [`remark-parse-yaml`](https://github.com/landakram/remark-parse-yaml)- 将YAML块解析为结构化数据
-   [`remark-ping`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-ping)- 自定义语法,解析`@user`,`@**first last**`,可配置的存在检查. Rehype兼容
-   [`remark-react`](https://github.com/mapbox/remark-react)- 将Markdown编译为[React](https://github.com/facebook/react)
-   [`remark-react-codemirror`](https://github.com/craftzdog/remark-react-codemirror)- 语法高亮显示[remark-react](https://github.com/mapbox/remark-react)通过[CodeMirror](https://codemirror.net)
-   [`remark-react-lowlight`](https://github.com/bebraw/remark-react-lowlight)- 语法高亮显示[remark-react](https://github.com/mapbox/remark-react)通过[lowlight](https://github.com/wooorm/lowlight)
-   [`remark-reference-links`](https://github.com/remarkjs/remark-reference-links)- 将链接和图像转换为引用和定义
-   [`remark-rehype`](https://github.com/remarkjs/remark-rehype)-[rehype](https://github.com/rehypejs/rehype)支持
-   [`remark-retext`](https://github.com/remarkjs/remark-retext)-[retext](https://github.com/retextjs/retext)支持
-   [`remark-rewrite-headers`](https://github.com/strugee/remark-rewrite-headers)- 改变标题水平
-   [`remark-shortcodes`](https://github.com/djm/remark-shortcodes)- 在Markdown中解析自定义 Wordpress/Hugo 类似的短代码
-   [`remark-slug`](https://github.com/remarkjs/remark-slug)- 添加slug 到标题
-   [`remark-strip-badges`](https://github.com/remarkjs/remark-strip-badges)- 删除徽章 (例如`shields.io`) 
-   [`remark-strip-html`](https://github.com/craftzdog/remark-strip-html)- 删除html格式
-   [`remark-squeeze-paragraphs`](https://github.com/eush77/remark-squeeze-paragraphs)- 删除空段落
-   [`remark-sub-super`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-sub-super)- 自定义语法来解析下标和上标. rehype 兼容 (使用`<sub>`和`<sup>`) 
-   [`remark-swagger`](https://github.com/yoshuawuyts/remark-swagger)- 插入一个swagger规范
-   [`remark-textr`](https://github.com/denysdovhan/remark-textr)-[`Textr`](https://github.com/shuvalov-anton/textr),模块化排版框架
-   [`remark-title`](https://github.com/RichardLitt/remark-title)- 检查并注入markdown的标题作为第一个元素. 
-   [`remark-toc`](https://github.com/remarkjs/remark-toc)- 为Markdown文件生成目录 (TOC) 
-   [`remark-unlink`](https://github.com/eush77/remark-unlink)- 删除所有链接,参考和定义
-   [`remark-usage`](https://github.com/remarkjs/remark-usage)- 在readme文件中添加一个用法示例
-   [`remark-validate-links`](https://github.com/remarkjs/remark-validate-links)- 验证链接指向现有标题和文件
-   [`remark-vdom`](https://github.com/remarkjs/remark-vdom)- 将Markdown编译为[VDOM](https://github.com/Matt-Esch/virtual-dom/)
-   [`remark-wiki-link`](https://github.com/landakram/remark-wiki-link)- 解析并呈现wiki链接
-   [`remark-yaml-annotations`](https://github.com/sfrdmn/remark-yaml-annotations)- 使用基于YAML的注释语法扩展Markdown
-   [`remark-yaml-config`](https://github.com/remarkjs/remark-yaml-config)- 使用YAML配置remark

## 预设列表

看下[npm搜索][preset-search]可用且，通常是棒棒的预设. 

## 公用工具清单

看下[**MDAST**][mdast-util]获取用于处理语法树的实用程序列表. 看下[`unist`][unist-util]适用于其他公用,同样适用**MDAST**节点. 

最后,看看[**vfile**][vfile-util]获取使用虚拟文件的实用程序列表. 

## 使用插件

要以编程方式使用插件,请调用[`use()`][unified-use]功能. 

而`remark-cli`使用插件则通过一个[`--use`][unified-args-use]或者在[配置文件][config-file-use]中指定它.

## 创建插件

首先,阅读[插件的概念][unified-plugins]. 然后,阅读["创建unified插件"指南][guide]. 最后,拿一个现有的[插件][plugins],看起来与你将要做的相似,并从那里开始工作. 如果你卡住了,[问题][issues]和[聊天室][Gitter]是获得帮助的好地方. 

你应该选择一个带有前缀的名字`'remark-'`, 如`remark-lint`. 

请注意,如果您创建的内容无法做到`remark().use()`,它不是一个"插件". 不要使用`remark-`前缀因为这可能会混淆用户. 如果它适用于HAST树,请使用`'mdast-util-'`,如果它适用于任何Unist树,请使用`unist-util-`,如果它适用于虚拟文件,请使用`vfile-`. 

<!--Definitions:-->

[logo]: https://cdn.rawgit.com/remarkjs/remark/ee78519/logo.svg

[plugins]: #list-of-plugins

[products]: https://github.com/remarkjs/remark/blob/master/doc/products.md

[mdast-util]: https://github.com/syntax-tree/mdast#list-of-utilities

[unist-util]: https://github.com/syntax-tree/unist#unist-utilities

[vfile-util]: https://github.com/vfile/vfile#utilities

[unified-use]: https://github.com/unifiedjs/unified#processoruseplugin-options

[unified-args-use]: https://github.com/unifiedjs/unified-args#--use-plugin

[config-file-use]: https://github.com/unifiedjs/unified-engine/blob/master/doc/configure.md#plugins

[unified-plugins]: https://github.com/unifiedjs/unified#plugin

[issues]: https://github.com/remarkjs/remark/issues

[gitter]: https://gitter.im/remarkjs/Lobby

[guide]: https://unifiedjs.github.io/create-a-plugin.html

[preset-search]: https://www.npmjs.com/search?q=remark-preset
