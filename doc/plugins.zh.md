
![remark][logo]

# 插件

**评论**是一个生态系统[插件][plugins].

见[用注释构建的工具][products].

## 目录表

-   [插件列表](#list-of-plugins)
-   [预置列表](#list-of-presets)
-   [公用事业清单](#list-of-utilities)
-   [使用插件](#using-plugins)
-   [创建插件](#creating-plugins)

## 插件列表

有一个新插件的好主意吗?让我们[闲聊][gitter]让它发生!

-   [`评论ABBR`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-abbr)-自定义语法来处理缩写,自定义的MADAST内联节点类型`abbr`.  Rehype兼容`ABBR标题="Bar"> Foo</ABBR>`) 
-   [`备注对齐`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-align)-自定义语法来处理文本/块对齐,自定义的MADAST块节点类型`中心对齐`,`右派的`.  Rehype兼容`div`s作为可配置CSS类的对齐方式) 
-   [`备注`](https://github.com/arobase-che/remark-attr)-将自定义属性的支持添加到标记
-   [`评论AutoLink标题`](https://github.com/ben-eb/remark-autolink-headings)-自动添加GITHUB样式链接到标题
-   [`评论书签`](https://github.com/ben-eb/remark-bookmarks)链接文件的标记文件
-   [`括号内括号`](https://github.com/sethvincent/remark-bracketed-spans)-将IDㄡ类和数据属性添加到`< SPA>`标记中的标记
-   [`备注`](https://github.com/remarkjs/remark-breaks)-断开支持,不需要空间
-   [`评论崩溃`](https://github.com/Rokt33r/remark-collapse)-使一节可折叠
-   [`注释块`](https://github.com/ben-eb/remark-comment-blocks)用注释块包装标记
-   [`备注注释配置`](https://github.com/remarkjs/remark-comment-config)-用注释配置注释
-   [`备注`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-comments)-可配置的自定义语法以忽略部分标记输入
-   [`评论撰稿人`](https://github.com/hughsk/remark-contributors)-注入给定的贡献者表
-   [`注释自定义块`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-custom-blocks)-可配置的自定义语法来解析自定义块,创建新的MADAST节点类型. Rehype兼容
-   [`断言`](https://github.com/eush77/remark-defsplit)-将内联链接和图像目的地提取为单独的定义. 
-   [`备注禁止记号器`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-disable-tokenizers)-禁止任何或所有的评论`封锁者`和`内联电报机`
-   [`注释嵌入图像`](https://github.com/dherges/remark-embed-images)-嵌入数据的图像: URI,内嵌Base64编码源
-   [`言辞`](https://github.com/rhysd/remark-emoji)-将Unicode表情转换为GEMIMI短代码
-   [`艾默姬`](https://github.com/jackycute/remark-emoji-to-gemoji)-将GEMIMI短代码转换为Unicode表情符号
-   [`评论外部链接`](https://github.com/xuopled/remark-external-links)-将目标和Read属性自动添加到外部链接
-   [`备注第一标题`](https://github.com/laat/remark-first-heading)-替换文档中的第一个标题
-   [`修正GuielMes`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-fix-guillemets)-对于奇怪排版的原因,这个修正`<a>`被解析为`<`+ HTML标签`< A>`+`>`而是用文本替换这个`<a>`
-   [`评论前沿`](https://github.com/remarkjs/remark-frontmatter)- Frontmatter (YAML,TAML,和更多) 支持
-   [`格莫吉评论`](https://github.com/remarkjs/remark-gemoji)GMEMOJI短代码支持
-   [`评论表情符号`](https://github.com/jackycute/remark-gemoji-to-emoji)-将GEMIMI短代码转换为Unicode表情符号
-   [`泛型扩展的注记`](https://github.com/medfreeman/remark-generic-extensions)通用标记扩展指令
-   [`吉图布评论`](https://github.com/remarkjs/remark-github)-自动链接引用,如GITHUB问题ㄡPRS和注释
-   [`GITLAB人工制品评论`](https://github.com/temando/remark-gitlab-artifact)-从GITLAB项目下载工件以与您的降价共存
-   [`注释网格表`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-grid-tables)-自定义标记语法来描述表. Rehype兼容
-   [`注记`](https://github.com/temando/remark-graphviz)-替换`点`具有SVG的图
-   [`评论标题差距`](https://github.com/ben-eb/remark-heading-gap)-调整标题之间的差距
-   [`J.`](https://github.com/ben-eb/remark-highlight.js)-在标记文件中突出显示代码块[强光](https://github.com/isagalaev/highlight.js)
-   [`注释HTML`](https://github.com/remarkjs/remark-html)-将标记向下编译为HTML文档
-   [`HTML表情图像`](https://github.com/jackycute/remark-html-emoji-image)-将Unicode表情转换为HTML图像
-   [`注释KATEX`](https://github.com/rokt33r/remark-math/blob/master/packages/remark-html-katex/readme.md)-将数学内联和块节点转换为样式HTML方程[卡特克斯](https://github.com/Khan/KaTeX)
-   [`注释IFRAMES`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-iframes)-自定义语法与完全可配置的IFRAME提供程序,遵循白名单方法. Rehype兼容
-   [`内联链接注释`](https://github.com/remarkjs/remark-inline-links)-将引用和定义转换为正常链接和图像
-   [`内联数学`](https://github.com/bizen241/remark-inline-math)-联机数学支持
-   [`备注KBD`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-kbd)-自定义语法,解析`γ-福奥`一个新的MADST内联节点类型`kbd`. Rehype兼容`<bkd> fo</kbd>`) 
-   [`备注许可证`](https://github.com/remarkjs/remark-license)-添加许可部分
-   [`评论皮棉`](https://github.com/remarkjs/remark-lint)-标记代码样式链接器
-   [`评论人`](https://github.com/remarkjs/remark-man)-编译标记到人页 (ROFF) 
-   [`评论数学`](https://github.com/rokt33r/remark-math)-数学内联和块支持
-   [`美人鱼评论`](https://github.com/temando/remark-mermaid)-替换[美人鱼](https://mermaidjs.github.io/)具有SVG的图
-   [`备注消息控制`](https://github.com/remarkjs/remark-message-control)-启用ㄡ禁用和忽略消息
-   [`备注元数据`](https://github.com/temando/remark-metadata)-将处理过的文件的元数据作为前置事项添加
-   [`评论迈达斯`](https://github.com/ben-eb/remark-midas)-在标记文件中突出显示CSS[迈达斯](https://github.com/ben-eb/midas)
-   [`备注标题归一化`](https://github.com/eush77/remark-normalize-headings)-确保文档中最多有一个顶级标题
-   [`OpenAPI的注释`](https://github.com/temando/remark-openapi)-将指向本地或远程OpenAPI定义的链接转换为具有所有路径摘要的表
-   [`评析YAML`](https://github.com/landakram/remark-parse-yaml)解析YAML块到结构化数据中
-   [`备注`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-ping)-自定义语法,解析`@用户`,`第一个最后一个**`可配置的存在检查. Rehype兼容
-   [`评论反应`](https://github.com/mapbox/remark-react)-将标记编译为[反应](https://github.com/facebook/react)
-   [`注释反应代码`](https://github.com/craftzdog/remark-react-codemirror)-语法突出显示[评论反应](https://github.com/mapbox/remark-react)通过[代码映射器](https://codemirror.net)
-   [`评论低调`](https://github.com/bebraw/remark-react-lowlight)-语法突出显示[评论反应](https://github.com/mapbox/remark-react)通过[低照度](https://github.com/wooorm/lowlight)
-   [`备注参考链接`](https://github.com/remarkjs/remark-reference-links)-将链接和图像转换为引用和定义
-   [`备注`](https://github.com/remarkjs/remark-rehype)-[再论](https://github.com/rehypejs/rehype)支持
-   [`备注`](https://github.com/remarkjs/remark-retext)-[重述](https://github.com/retextjs/retext)支持
-   [`重写标题`](https://github.com/strugee/remark-rewrite-headers)-改变航向水平
-   [`注释短代码`](https://github.com/djm/remark-shortcodes)-在自定义标记中解析自定义WordPress/雨果类短代码
-   [`评论蛞蝓`](https://github.com/remarkjs/remark-slug)向标题添加蛞蝓
-   [`带条徽章`](https://github.com/remarkjs/remark-strip-badges)-删除徽章 (如`盾牌`) 
-   [`带条HTML`](https://github.com/craftzdog/remark-strip-html)-删除HTML格式
-   [`备注段落`](https://github.com/eush77/remark-squeeze-paragraphs)-删除空段落
-   [`备注超`](https://github.com/zestedesavoir/zmarkdown/tree/master/packages/remark-sub-super)自定义语法来解析下标和上标. Rehype兼容 (使用) `<Su>`和`<sup>`) 
-   [`评论狂妄自大`](https://github.com/yoshuawuyts/remark-swagger)-插入摇晃规范
-   [`评论`](https://github.com/denysdovhan/remark-textr)-[`特斯特`](https://github.com/shuvalov-anton/textr)模块化排版框架
-   [`备注标题`](https://github.com/RichardLitt/remark-title)-检查和注销标记的标题作为第一个元素. 
-   [`评论TOC`](https://github.com/remarkjs/remark-toc)-生成标记文件的内容表 (TOC) 
-   [`注释链接`](https://github.com/eush77/remark-unlink)-删除所有链接ㄡ引用和定义
-   [`备注用法`](https://github.com/remarkjs/remark-usage)-向您的自述添加一个使用示例
-   [`验证链接`](https://github.com/remarkjs/remark-validate-links)-验证链接指向现有标题和文件
-   [`评论VDOM`](https://github.com/remarkjs/remark-vdom)-将标记编译为[VDOM](https://github.com/Matt-Esch/virtual-dom/)
-   [`评论维基链接`](https://github.com/landakram/remark-wiki-link)解析并呈现维基链接
-   [`注释YAML注释`](https://github.com/sfrdmn/remark-yaml-annotations)用基于YAML的注释语法扩展标记
-   [`注释YAML配置`](https://github.com/remarkjs/remark-yaml-config)-用YAML配置注释

## 预置列表

见[NPM搜索][preset-search]可用的和经常鼓舞人心的预设. 

## 公用事业清单

见[**麦迪斯特**][mdast-util]用于使用语法树的实用工具列表. 见[`unist`][unist-util]对于其他公用事业公司**麦迪斯特**节点也是如此. 

最后,看到[**虚拟文件**][vfile-util]用于使用虚拟文件工作的实用工具列表. 

## 使用插件

若要以编程方式使用插件,请调用[`使用 () `][unified-use]功能. 

使用插件`评论CLI`通过一个[`--使用`旗帜][unified-args-use]或在A中指定[配置文件][config-file-use].

## 创建插件

首先,阅读[插件概念][unified-plugins].  然后,阅读["创建统一插件"指南][guide].  最后,采取一个现有的[插件][]这看起来和你要做的类似,并且从那里开始工作. 如果你被卡住了,[问题][]和[吉特][]是获得帮助的好地方. 

你应该选择一个前缀`"评论"`,如`评论皮棉`.

注意,如果你创造的东西不能给予` ()  () `它不是一个"插件". 不要使用`备注-`前缀可以混淆用户. 如果它与HAST树一起使用,请使用`"达斯特UTIL"`如果使用任何UNIST树,请使用`UIST UTIL`如果使用虚拟文件,请使用`VFISH`.

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
