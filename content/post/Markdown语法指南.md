---
title: Markdown 语法指南
date: 2026-01-14
share: "true"
description: 本文提供了一些基本的 Markdown 语法示例，可用于 Hugo 内容文件，同时还展示了 Hugo 主题中基本 HTML 元素是否带有 CSS 样式修饰。
dir: post
math: "true"
---

本文提供了一些基本的 Markdown 语法示例，可用于 Hugo 内容文件，同时还展示了 Hugo 主题中基本 HTML 元素是否带有 CSS 样式修饰。

<!--more-->

## 标题

以下 HTML `<h1>`—`<h6>` 元素代表六个级别的章节标题。`<h1>` 是最高级别的章节，而 `<h6>` 是最低级别的。

# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题

## 段落

Xerum，quo qui aut unt expliquam qui dolut labo。Aque venitatiusda cum，voluptionse latur sitiae dolessi aut parist aut dollo enim qui voluptate ma dolestendit peritin re plis aut quas inctum laceat est volestemque commosa as cus endigna tectur，offic to cor sequas etum rerum idem sintibus eiur？Quianimin porecus evelectur，cum que nis nust voloribus ratem aut omnimi，sitatur？Quiatem。Nam，omnis sum am facea corem alique molestrunt et eos evelece arcillit ut aut eos eos nus，sin conecerem erum fuga。Ri oditatquam，ad quibus unda veliamenimin cusam et facea ipsamus es exerum sitate dolores editium rerore eost，temped molorro ratiae volorro te reribus dolorer sperchicium faceata tiustia prat。

Itatur？Quiatae cullecum rem ent aut odis in re eossequodi nonsequ idebis ne sapicia is sinveli squiatum，core et que aut hariosam ex eat。

## 引用块

引用块元素表示从其他来源引用的内容，可选择性地包含引用来源（必须在 `footer` 或 `cite` 元素内），以及可选的内联更改，如注释和缩写。

### 无归属的引用块

> Tiam，ad mint andaepu dandae nostion secatur sequo quae。
> **注意** 你可以在引用块内使用 *Markdown 语法*。

### 有归属的引用块

> 不要通过共享内存来交流，而要通过交流来共享内存。<br>
> — <cite>Rob Pike[^1]</cite>

[^1]: 以上引用摘自 Rob Pike 在 2015 年 11 月 18 日 Gopherfest 大会上的演讲。

## 表格

表格不是 Markdown 核心规范的一部分，但 Hugo 开箱即用地支持它们。

   姓名 | 年龄
--------|------
    鲍勃 | 27
  爱丽丝 | 23

### 表格内的内联 Markdown

| 斜体   | 粗体     | 代码   |
| --------  | -------- | ------ |
| *斜体* | **粗体** | `代码` |

| A                                                        | B                                                                                                             | C                                                                                                                                    | D                                                 | E                                                          | F                                                                    |
|----------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------|------------------------------------------------------------|----------------------------------------------------------------------|
| Lorem ipsum dolor sit amet，consectetur adipiscing elit。 | Phasellus ultricies，sapien non euismod aliquam，dui ligula tincidunt odio，at accumsan nulla sapien eget ex。 | Proin eleifend dictum ipsum，non euismod ipsum pulvinar et。Vivamus sollicitudin，quam in pulvinar aliquam，metus elit pretium purus | Proin sit amet velit nec enim imperdiet vehicula。 | Ut bibendum vestibulum quam，eu egestas turpis gravida nec | Sed scelerisque nec turpis vel viverra。Vivamus vitae pretium sapien |

## 代码块

### 使用反引号的代码块

```html
<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8">
  <title>示例 HTML5 文档</title>
</head>
<body>
  <p>测试</p>
</body>
</html>
```

### 使用四个空格缩进的代码块

    <!doctype html>
    <html lang="zh-CN">
    <head>
      <meta charset="utf-8">
      <title>示例 HTML5 文档</title>
    </head>
    <body>
      <p>测试</p>
    </body>
    </html>

### 差异代码块

```diff
[dependencies.bevy]
git = "https://github.com/bevyengine/bevy"
rev = "11f52b8c72fc3a568e8bb4a4cd1f3eb025ac2e13"
- features = ["dynamic"]
+ features = ["jpeg", "dynamic"]
```

### 单行代码块

```html
<p>一个段落</p>
```

## 列表类型

### 有序列表

1. 第一项
2. 第二项
3. 第三项

### 无序列表

* 列表项
* 另一项
* 另一项

### 嵌套列表

* 水果
  * 苹果
  * 橙子
  * 香蕉
* 乳制品
  * 牛奶
  * 奶酪

## 其他元素 — abbr、sub、sup、kbd、mark

<abbr title="图形交换格式">GIF</abbr> 是一种位图图像格式。

H<sub>2</sub>O

X<sup>n</sup> + Y<sup>n</sup> = Z<sup>n</sup>

按 <kbd>CTRL</kbd> + <kbd>ALT</kbd> + <kbd>Delete</kbd> 结束会话。

大多数<mark>蝾螈</mark>是夜行性动物，捕食昆虫、蠕虫和其他小型生物。
