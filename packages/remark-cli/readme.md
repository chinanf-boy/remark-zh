
# 一句话,CLI[![Build Status][build-badge]][build-status] [![Coverage Status][coverage-badge]][coverage-status] [![Chat][chat-badge]][chat]

命令行界面[**备注**][remark]. 

-   加载[`备注-`插件][plugins]
-   搜索[降价扩展][markdown-extensions]
-   忽略找到的路径[`.remarkignore`档][ignore-file]
-   从中加载配置[`.remarkrc`,`.remarkrc.js`档][config-file]
-   使用配置来自[`remarkConfig`中的字段`的package.json`档][config-file]

## 安装

[npm][]: 

```sh
npm install remark-cli
```

## 用法

```sh
# Add a table of contents to `readme.md`
$ remark readme.md --use toc --output

# Lint markdown files in the current directory
# according to the markdown style guide.
$ remark . --use preset-lint-markdown-style-guide
```

## CLI

看到[**统一-ARGS**][unified-args],提供接口,以获取有关所有可用选项的更多信息. 

```txt
Usage: remark [options] [path | glob ...]

  CLI to process markdown with remark using plugins

Options:

  -h  --help                output usage information
  -v  --version             output version number
  -o  --output [path]       specify output location
  -r  --rc-path <path>      specify configuration file
  -i  --ignore-path <path>  specify ignore file
  -s  --setting <settings>  specify settings
  -e  --ext <extensions>    specify extensions
  -u  --use <plugins>       use plugins
  -w  --watch               watch for changes and reprocess
  -q  --quiet               output only warnings and errors
  -S  --silent              output only errors
  -f  --frail               exit with 1 on warnings
  -t  --tree                specify input and output as syntax tree
      --report <reporter>   specify reporter
      --file-path <path>    specify path to process as
      --tree-in             specify input as syntax tree
      --tree-out            output syntax tree
      --inspect             output formatted syntax tree
      --[no-]stdout         specify writing to stdout (on by default)
      --[no-]color          specify color in report (on by default)
      --[no-]config         search for configuration files (on by default)
      --[no-]ignore         search for ignore files (on by default)

Examples:

  # Process `input.md`
  $ remark input.md -o output.md

  # Pipe
  $ remark < input.md > output.md

  # Rewrite all applicable files
  $ remark . -o
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

[plugins]: https://github.com/remarkjs/remark/blob/master/doc/plugins.md

[markdown-extensions]: https://github.com/sindresorhus/markdown-extensions

[config-file]: https://github.com/unifiedjs/unified-engine/blob/master/doc/configure.md

[ignore-file]: https://github.com/unifiedjs/unified-engine/blob/master/doc/ignore.md

[unified-args]: https://github.com/unifiedjs/unified-args#cli
