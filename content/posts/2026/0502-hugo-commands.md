+++
date = '2026-05-02'
draft = false
title = 'Hugo 常用指令 & 遇到的小陷阱'
description = "記錄一下自己常用的指令，其他可用參數可由公式的Docs取得"
tags = ["hugo"]
+++

## 常用指令

### 建立新文章

```
hugo new [filepath]
```

filepath以content為根目錄，ex:

```
hugo new post/2026/test.md

會建立 content/post/2026/test.md 檔案
```

#### Reference

- [Hugo Docs (hugo new)](https://gohugo.io/commands/hugo_new/ "https://gohugo.io/commands/hugo_new/")

### 啟動內建的伺服器(預覽用)

```
hugo server -D
```

當指定`-D`時，`draft=true`的文章也會出現在列表

#### Reference

- [Hugo Docs (hugo server)](https://gohugo.io/commands/hugo_server/ "https://gohugo.io/commands/hugo_server/")

---

## 遇到的小陷阱

### Q: 明明使用`hugo server -D`，draft的文章卻沒有出現？

可嘗試檢查draft文章的date是否為有效時間。  
我自己遇到的情形是，我的date指定到日 (ex: `2026-05-02`)，但明明local time已經是 `2026-05-02T00:30:00+09:00`，draft的文章卻沒顯示在內建的server上。  
原因是local time和server time的不一致。  
我的解法是在`hugo.toml`裡加上`timeZone = "Asia/Tokyo"`指定Timezone。
