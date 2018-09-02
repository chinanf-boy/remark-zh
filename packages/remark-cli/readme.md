# remark-cli [![Build Status][build-badge]][build-status] [![Coverage Status][coverage-badge]][coverage-status] [![Chat][chat-badge]][chat]

[**remark**][remark]命令行界面.

- 加载[`remark-`插件][plugins]
- 搜索[markdown 扩展][markdown-extensions]
- 忽略找到的路径[`.remarkignore`文件][ignore-file]
- 加载配置[`.remarkrc`,`.remarkrc.js`文件][config-file]
- 使用配置来自[package.json`文件的`remarkConfig`字段`][config-file]

## 安装

[npm][]:

```sh
npm install remark-cli
```

## 用法

```sh
# Add a 目录表格 to `readme.md`
$ remark readme.md --use toc --output

# Lint markdown files in the 当前目录
# 根据 the markdown 风格指南.
$ remark . --use preset-lint-markdown-style-guide
```

## CLI

看下[**unified-args**][unified-args],提供接口,以获取有关所有可用选项的更多信息.

```txt
Usage: remark [options] [path | glob ...]

  CLI to process markdown with remark using plugins

Options:

  -h  --help                输出使用信息
  -v  --version             输出版本号
  -o  --output [path]       指定输出位置
  -r  --rc-path <path>      指定配置文件
  -i  --ignore-path <path>  指定忽略文件
  -s  --setting <settings>  指定设置
  -e  --ext <extensions>    指定扩展名
  -u  --use <plugins>       使用插件
  -w  --watch               注意变化和重新处理
  -q  --quiet               仅输出警告和错误
  -S  --silent              仅输出错误
  -f  --frail               警告时退出,退出代码为1
  -t  --tree                将输入和输出指定为语法树
      --report <reporter>   指定报告
      --file-path <path>    指定要处理的路径
      --tree-in             将输入指定为语法树
      --tree-out            输出语法树
      --inspect             输出格式化的语法树
      --[no-]stdout         指定写入stdout（默认情况下启动）
      --[no-]color          在报告中指定颜色（默认情况下启动）
      --[no-]config         搜索配置文件（默认情况下已启用）
      --[no-]ignore         搜索忽略文件（默认情况下已启用）

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
