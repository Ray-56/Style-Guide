# Git提交规范

Git每次提交代码, 都要写 Commit message(提交说明), 否则就不允许提交.
一般来说 Commit message 应该清晰明了, 说明本次提交的目的.

内容:

1.  [作用](#作用)
2.  [格式](#格式)
    1.  [Header](#Header)
    2.  [Body](#Body)
    3.  [Footer](#Footer)
        1.  [不兼容变动](#不兼容变动)
        2.  [关闭Issue](#关闭Issue)
3.  [生成Changelog](#生成Changelog)

## 作用

格式化 Commit message, 有以下几个好处:

1.  提供更多的信息, 方便排查与回退.
2.  过滤关键字, 迅速定位.
3.  方便生成文档Change Log.

## 格式

每次提交, Commit message 都包括三个部分: `Header`、`Body`以及`Footer`.

```
<type>(<scope>): <subject>

// 空一行<body>

// 空一行<footer>
```

其中, `Header`是必须的, `Body`和`Footer`可以省略.

不管是哪一个部分, 任何一行都不得超过72|100个字符. 这是为了避免自动换行影响美观.

eg:

```
1> fix List组件: 删除item后滚动卡住(#8547)
2> feat 本周任务: 添加xxx功能(#0947)
3> docs Button: 加入clear属性
```

### Header(必需)

Header部分只有一行, 包括三个字段:

1.  `type`(必需): type用于说明 commit 的类别, 只允许使用下面7个标识:
    1.  `feat`: 新功能(feature).
    1.  `fix`: 修补bug.
    1.  `docs`: 文档(documentation).
    1.  `style`: 样式(不影响代码运行的变动).
    1.  `refator`: 重构(即不是新增代码, 也不是修改bug的代码变动).
    1.  `test`: 增加测试.
    1.  `chore`: 构建过程或辅助工具的变动.
    
    如果`type`为`feat`和`fix`, 则该 commit 将肯定出现在 Change log 之中. 其他情况(`docs`、`style`、`refactor`、`test`、`chore`) 由你决定, 要不要放入 Change log, 建议是不要.
2.  `scope`(可选): 说明 commit影响的范围, 比如数据层、控制层、视图层等等, 这里看项目不同而影响的范围不同.
3.  `subject`(必需): 此次 commit的目的的简短描述, 不超过50个字符.
    1.  以动词开头, 使用第一人称现在时, 例如`change`, 而不是`changed`或`changes`.
    1.  第一个字母小写.
    1.  结尾不加句号`.`.

### Body

Body 部分是对本次 commit 的详细描述, 可以分成多行. eg:

```
更详细的说明文字. 不要超过72个字符.
```

有两点注意:

1.  使用第一人称现在时, 比如使用`change`而不是`changed`或者`changes`.
2.  应该说明代码变动的动机, 以及与以前行为的对比.

### Footer

Footer 部分只用于两种情况.

#### 不兼容变动

如果当前代码与上一个版本不兼容, 则 Footer 部分以`BREAKING CHANGE`开头, 后面是对变动的描述、以及变动的理由和迁移方法.

```
BREAKING CHANGE: 隔离范围绑定定义已经改变.

    移植代码, 请参照下面的例子:

    Before:

    scope: {
        myAttr: 'attribute`,
    }

    After:

    scope: {
        myAttr: '@',
    }

    移除的`inject`不是一般有用的指令, 所以这里本应该没有用它的编码.
```

#### 关闭Issue

如果当前 commit 针对某个 issue, 那么可以在Footer部分关闭这个 issue.

```
Close #765
```

也可以一次关闭多个 issue.

```
Close #123, #223, #323
```

## 生成Changelog

如果我们的提交都按照规范的话, 那就很简单了. 生成的文档包括以下三个部分:

- New features(新功能)
- Bug fixes(修复bug)
- Breaking changes(代码版本改动)

每个部分都会罗列相关的 commit, 并且有指向这些 commit 的链接. 当然, 生成的文档允许手动修改, 所以发布前, 你可以添加其他内容.

[Conventional Changelog](https://github.com/conventional-changelog/conventional-changelog)就是生成 Change log的工具:

```
npm install -g conventional-changelog
cd jartto-domo
conventional-changelog -p angular -i CHANGELOG.md -w
```

方便使用, 可以将其写入`package.json`中的`scripts`字段.

```
{
  "scripts": {
    "changelog": "conventional-changelog -p angular -i CHANGELOG.md -w -r 0"
  }
}
```

so far. 麻麻再也不担心我的Git了.