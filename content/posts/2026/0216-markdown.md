+++
date = '2026-03-16T22:34:01+09:00'
draft = false
title = 'markdown 的語法和 layout 確認'
description = "personal memo"
+++

## 標題 (H1~6)

```
# H1
## H2
### H3
#### H4
##### H5
###### H6
```

# H1 標題測試abc

## H2 標題測試abc

### H3 標題測試abc

#### H4 標題測試abc

##### H5 標題測試abc

###### H6 標題測試abc

---

## 字體效果

```
*斜體字*
**粗體字**
***斜體兼粗體***
~~刪除線~~
_斜體字2_
__粗體字2__
___斜體兼粗體2___
正常<sup>上標</sup>
正常<sub>下標</sub>
<ins>底線</ins>
<mark>螢光標記</mark>
<kbd>Ctrl + C</kbd> 鍵盤輸入
```

_斜體字_  
**粗體字**  
**_斜體兼粗體_**  
~~刪除線~~  
_斜體字2_  
**粗體字2**  
**_斜體兼粗體2_**  
正常<sup>上標</sup>  
正常<sub>下標</sub>  
<ins>底線</ins>  
<mark>螢光標記</mark>  
<kbd>Ctrl + C</kbd> 鍵盤輸入

---

## 段落、斷行、分隔線

```
段落間空一行分段落
文末兩個空白斷行
---分隔線 (與上面的內容需空一行)

Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Cras et scelerisque ipsum.
Nullam rhoncus tortor eget neque lobortis, a vehicula lacus iaculis. Fusce eu quam condimentum, venenatis orci commodo, viverra ante. Praesent sed aliquet odio.

Nulla congue mi tortor, sed maximus orci interdum vel. Integer finibus, tortor sit amet blandit volutpat, orci tellus luctus nunc, sodales efficitur turpis urna sit amet mi. Ut quis venenatis ex. Sed eu leo lobortis arcu pharetra consequat vel in nibh. Etiam ac nibh vel massa posuere venenatis sit amet a ex.
```

Lorem ipsum dolor sit amet, consectetur adipiscing elit.  
Cras et scelerisque ipsum.  
Nullam rhoncus tortor eget neque lobortis, a vehicula lacus iaculis. Fusce eu quam condimentum, venenatis orci commodo, viverra ante. Praesent sed aliquet odio.

Nulla congue mi tortor, sed maximus orci interdum vel. Integer finibus, tortor sit amet blandit volutpat, orci tellus luctus nunc, sodales efficitur turpis urna sit amet mi. Ut quis venenatis ex. Sed eu leo lobortis arcu pharetra consequat vel in nibh. Etiam ac nibh vel massa posuere venenatis sit amet a ex.

---

## code

### code block

````
用三個`包住, ex:
```
<!DOCTYPE html>
<html lang="en">
</html>
```

可指定語言(會有syntax highlighting), ex:
```html

加行號, ex:
```html {linenos=true}

highlight特定行，ex:
```html {hl_lines=[2,8]}

行號可和highlight特定行合併使用，ex:
```html {linenos=true,hl_lines=[2,8]}
但似乎無法在不指定語言的情況下使用行號?

````

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Example HTML5 Document</title>
  </head>
  <body>
    <p>Test</p>
  </body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Example HTML5 Document</title>
  </head>
  <body>
    <p>Test</p>
  </body>
</html>
```

```html {linenos=true}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Example HTML5 Document</title>
  </head>
  <body>
    <p>Test</p>
  </body>
</html>
```

```html {hl_lines=[2,8]}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Example HTML5 Document</title>
  </head>
  <body>
    <p>Test</p>
  </body>
</html>
```

### inline code

```
like this, `inline code`.
```

like this, `inline code`.

### pre tag

```
<pre>
aaaa
  bbb
  cc
dddddd
</pre>
```

<pre>
aaaa
  bbb
  cc
dddddd
</pre>

---

## list

```
### ordered

1. First item
2. Second item
3. Third item

### unordered

- List item
- Another item
- And another item

### nested

- Fruit
  - Apple
  - Orange
  - Banana
- Dairy
  - Milk
  - Cheese

### check box

- [ ] タスク1
- [x] タスク2
  - [x] 2.1

```

### ordered

1. First item
2. Second item
3. Third item

### unordered

- List item
- Another item
- And another item

### nested

- Fruit
  - Apple
  - Orange
  - Banana
- Dairy
  - Milk
  - Cheese

### check box

- [ ] タスク1
- [x] タスク2
  - [x] 2.1

---

## folding

```
<details><summary>防劇透folding</summary>
折起來的內容abc
ddd<br>
last line
</details>

```

<details><summary>防劇透folding</summary>
折起來的內容abc  
ddd<br>
last line
</details>

---

引用 quote

```
> 引用第一層aaaa
> 引用第一層aaaa
> > 引用第二層aaaa
> > > 第用第三層 bbbb
```

> 引用第一層aaaa
> 引用第一層aaaa
>
> > 引用第二層aaaa
> >
> > > 第用第三層 bbbb

---

## link & 插入圖片

```
[GitHub](https://github.com/ "GitHub Top")

插入圖片
![dummy image](/images/dummy_300_200.png "Dummy")
![代替テキスト](画像のURL "画像タイトル")
```

[GitHub](https://github.com/ "GitHub Top")

![dummy image](../../../images/dummy_300_200.png "Dummy")
