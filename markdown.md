# Markdown 编写规范
该规范为前端团队约定遵循的**Markdown 规范**.

内容:



## 文件布局

通常来说, 大多数布局都受益于以下布局:

```markdown
# 文档标题

简短的介绍

[TOC](table of content)

## Topic

Content.

## See also(另请参阅)

* https://link-to-more-info
```

1. `文档标题`: 第一个标题应该是一级标题, 理想情况应与文件名相同或几乎相同. 第一级标题用作页面`<title>`.
2. `简短的介绍`: 1-3 个句子, 提供该主题的高级概述. 想象一下你自己是一个萌新, 别人想要拓展你的`Extending Foo`文档, 他需要知道该文档最基本的假设. "什么是 Foo? 我为什么要拓展它?"
3. `[TOC]`: 目录表.
4. `## Topic`: 其余标题应从2级开始.
5. `## See also`: 将杂项链接放在底部, 供想要了解更多或未找到所需内容的用户使用.

## 标题

使用`#`模式.
```
## Heading 2
```

### 添加标题间距

在`#`和换行符之前和之后选择间距:

```markdown
...text before.

# Heading 1

Text after...
```

缺乏间距使得源代码中阅读起来有点困难:

```markdown
...text before.

#Heading 1
Text after... 不要这样做.
```

## Lists

### 对长列表使用数字编号(该功能需自己实现github中不支持)

```markdown
1.  Foo.
2.  Bar.
3.  Baz.
```

### 嵌套列表间距

嵌套列表时, 对编号和项目符号列表使用4个空格缩进:

```markdown
1.  编号后2个空格.
    包裹文本4个空格.
2.  还是2个空格.
    1.  编号后2个空格.
        8个空格, 是上面的内容.
3.  是不是很棒?
```

当列表很小, 没有嵌套和单行时, 一个空格就可以满足两种类型的列表:

```markdown
* Foo
* Bar
* Baz.

1. Foo.
2. Bar.

- Foo.
- Bar.
```

## Code

### 内联

`Backticks`指定内联代码, 并按字面意思呈现所有包装内容. 将它们用于短代码引用和字段名称:

```markdown
你将要执行`todosomething.js`.

后台返回参数中有`sourceType`字段.
```

### 代码块

对于长于一行的代码使用代码块:
<pre>
```python
def Foo(self, bar):
    self.bar = bar
```
</pre>

#### 声明语言

最佳的做法是显示声明语言, 以便语法高亮显示和下一个编译器不用去猜测.

#### 避免使用换行

由于大多数命令行片段都要复制粘贴到终端中, 因此最好避免使用任何换行符. 在行尾使用一个`\`(反斜杠):

<pre>
```shell
bazel run :target -- --flag --foo=longlonglonglonglongvalue \
--bar=anotherlonglonglonglonglonglonglonglonglonglongvalue
```
</pre>

#### 在列表中嵌套代码块

如果需要在列表中使用代码块, 请确保缩进以便它不会破坏列表:

```markdown
-   Bullet.

    ```c++
    int foo;
    ```
-   Next bullet.
```

还可以创建一个包含4个空格的嵌套代码块. 只需要再列表缩进中缩进4个额外的空格:

```markdown
*   Bullet.

        int foo;

*   Next bullet.
```

## 连接

长的链接地址使源Markdown文件难以阅读并打破80个字符的包装. 尽可能的缩短链接字符.

### 使用信息丰富的Markdown链接标题

Markdown链接语法允许设置链接标题, 就像HTML一样. 巧妙的使用它.

不要将将你的链接标题设置为"link"或"here", 在快速扫描文档时会准确的告诉读者链接内的内容:

```markdown
不好的做法.
有关详细信息, 请参阅语法指南: [link](syntax_guide.md).
或者, 查看样式指南: [此处](style_guide.md).
```

相反的, 自然的写出句子, 然后返回并用链接包装最合适的短语:

```markdown
详细信息, 查看[语法指南](syntax_guide.md).
或者, 查看[样式指南](style_guide.md).
```

## 图片

尽量少用图片, 使用一些简单的截图. 本指南的设计理念是, 纯文本可以让用户更快地完成业务通信, 减少读者分心和作者的拖延. 但是有时图片对显示你的意思非常有帮助.

使用方法和连接方法相似区别在于前面加了个感叹号`!`.

```markdown
![图片名称](http://图片网址)
```

当然, 也可以使用变量:

```markdown
这个链接用 1 作为网址变量 [Google][1].
然后再文档的皆为变量赋值网址.

 [1]: http://www.google.com/logo.png
```

## 表格

一个简单的表格:

```markdown
| Transport | Favored by | Advantages |
| --- | --- | --- |
| Swallow | Coconuts | Otherwise unladen |
| Bicycle | Miss Gulch | Weatherproof |
| X-34 landspeeder | Whiny farmboys | Cheap since the X-38 came out |
```

第二行的`---`是行以何种方式对齐:

- `:--`: 左对齐.
- `--:`: 右对齐.
- `---`: 居中对齐.