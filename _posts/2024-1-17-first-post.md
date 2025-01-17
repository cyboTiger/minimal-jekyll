---
layout: post
title:  "building my blog"
excerpt: "1st post"
date:   2024-01-18 00:30:00
render_with_liquid: false
---

# 关于各个html文件的作用解释
## `index.html`文件
```html
---
layout: default
---

<div class="home">
  
  <ul class="posts">
    {% for post in site.posts %}
      <li>
        <span class="post-date">{{ post.date | date: "%b %-d, %Y" }}</span>
        <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
        <br>
        {{ post.excerpt }}
      </li>
    {% endfor %}
  </ul>

</div>
```
这个HTML文件是一个用于生成博客首页的模板，通常用于静态网站生成器（如Jekyll）。它使用Liquid模板语言来动态生成内容。以下是对这个文件的详细解释：
### 1. Front Matter
```html
---
layout: default
---
```
+ 这是YAML格式的Front Matter，用于配置页面的元数据。
+ `layout: default` 指定了这个页面使用 default 布局文件（通常是 `_layouts/default.html`），这意味着这个页面的内容会被插入到 default 布局的某个部分中。

### 2. HTML结构
```html
<div class="home">
```
+ 这是一个 `div` 元素，带有 `class="home"`，通常用于包裹首页的内容。

### 3. 帖子列表
```html
<ul class="posts">
```
+ 这是一个无序列表 (`<ul>`)，带有 `class="posts"`，用于显示博客文章的列表。

### 4. 循环遍历帖子
```html
{% for post in site.posts %}
```
+ 这是一个Liquid模板语言的循环语句，用于遍历 `site.posts` 中的所有博客文章。
+ `site.posts` 是Jekyll中的一个全局变量，包含了所有的博客文章。

### 5. 单个帖子项
```html
<li>
  <span class="post-date">{{ post.date | date: "%b %-d, %Y" }}</span>
  <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
  <br>
  {{ post.excerpt }}
</li>
```
+ 每个帖子都作为一个列表项 (<li>) 显示。
+ `<span class="post-date">` 显示帖子的发布日期，格式为 月 日, 年（例如：Jan 1, 2023）。
+ `<a class="post-link">` 是一个链接，指向该帖子的详细页面。`{{ post.url | prepend: site.baseurl }}` 用于生成完整的URL。
+ `{{ post.title }}` 显示帖子的标题。
+ `<br>` 是一个换行符，用于分隔标题和摘要。
+ `{{ post.excerpt }}` 显示帖子的摘要部分（通常是文章的前几行内容）。

### 6. 结束循环
```html
{% endfor %}
```
+ 结束`for`循环

### 7. 结束HTML结构
```html
  </ul>
</div>
```
+ 关闭`ul`和`div`标签。

## `_layouts/default.html`文件
```html
<!DOCTYPE html>
<html>

  {% include head.html %}

    <body>

    {% include header.html %}

    <div class="page-content">
      <div class="wrap">
      {{ content }}
      </div>
    </div>

    {% include footer.html %}

    </body>
</html>
```
这个文件是 Jekyll 静态网站生成器中的布局文件（`_layouts/default.html`），它定义了一个通用的页面结构，其他页面可以通过指定 `layout: default` 来继承这个结构。以下是对这个文件的详细解释：

### 1. `<!DOCTYPE html>`
+ 这是 HTML5 的文档类型声明，告诉浏览器这是一个 HTML5 文档。

### 2. `<html>` 标签
+ 这是 HTML 文档的根元素，所有内容都包含在这个标签内。

### 3. `{% include head.html %}`
+ 这是 Liquid 模板语言的 include 语句，用于将 `_includes/head.html` 文件的内容插入到这里。
+ `head.html` 通常包含页面的元数据（如 `<title>`、`<meta>` 标签）、CSS 文件链接、JavaScript 文件链接等。
+ 通过这种方式，可以将页面的头部内容集中管理，避免重复代码。

### 4. `<body>`
+ 这是 HTML 文档的主体部分，页面的可见内容都包含在这里。

### 5. `{% include header.html %}`
+ 这是另一个 include 语句，用于将 `_includes/header.html` 文件的内容插入到这里。
+ `header.html` 通常包含网站的导航栏、Logo、页眉等内容。
+ 通过这种方式，可以在多个页面中复用相同的页眉内容。

### 6. 页面内容区域

```html
<div class="page-content">
  <div class="wrap">
    {{ content }}
  </div>
</div>
```

+ `{{ content }}` 是 Liquid 模板语言的占位符，表示其他页面（如 Markdown 文件或其他 HTML 文件）的内容会被插入到这里。
+ `div class="page-content"` 和 `div class="wrap"` 是用于布局和样式的容器，通常用于控制页面的宽度、边距等。
+ 例如，如果一个 Markdown 文件指定了 `layout: default`，那么它的内容会被渲染并插入到 `{{ content }}` 的位置。

### 7. `{% include footer.html %}`
+ 这是另一个 include 语句，用于将 `_includes/footer.html` 文件的内容插入到这里。
+ `footer.html` 通常包含网站的页脚内容，如版权信息、联系方式、社交媒体链接等。
+ 通过这种方式，可以在多个页面中复用相同的页脚内容。

### 8. 结束标签
+ 关闭 `body` 和 `html` 标签，表示 HTML 文档的结束。

### 总结
这个 default.html 文件定义了一个通用的页面结构，包括：
+ 头部（`head.html`）：包含页面的元数据和资源链接。
+ 页眉（`header.html`）：包含导航栏和 Logo 等内容。
+ 内容区域（`{{ content }}`）：动态插入其他页面的内容。
+ 页脚（`footer.html`）：包含版权信息和联系方式等内容。

通过这种模块化的设计，可以轻松地在多个页面中复用相同的布局和组件，同时保持代码的整洁和可维护性。