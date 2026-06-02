+++
date = '2026-05-02'
draft = false
title = 'Hugo 常用指令 & 遇到的小問題'
description = "記錄一下自己常用的指令，其他可用參數可由公式的 Docs 取得"
tags = ["hugo"]
+++

## 常用指令

### 建立新文章

```
hugo new [filepath]
```

filepath 以 content 為根目錄，ex:

```
hugo new post/2026/test.md

會建立 content/post/2026/test.md 檔案
```

#### Reference

- [Hugo Docs (hugo new)](https://gohugo.io/commands/hugo_new/ "https://gohugo.io/commands/hugo_new/")

### 啟動內建的伺服器（預覽用）

```
hugo server -D
```

當指定`-D`時，`draft=true`的文章也會出現在列表

#### Reference

- [Hugo Docs (hugo server)](https://gohugo.io/commands/hugo_server/ "https://gohugo.io/commands/hugo_server/")

---

## 遇到的小問題

### Q: 明明使用`hugo server -D`，draft 的文章卻沒有出現？

可嘗試檢查 draft 文章的 date 是否為有效時間。  
我自己遇到的情形是，我的 date 指定到日 (ex: `2026-05-02`)，但明明 local time 已經是 `2026-05-02T00:30:00+09:00`，draft 的文章卻沒顯示在內建的 server 上。  
原因是 local time 和 server time 的不一致。  
我的解法是在`hugo.toml`裡加上`timeZone = "Asia/Tokyo"`指定 Timezone。

### Q: 以`hugo new [filepath]`新增的檔案的 Front matter 的欄位不夠 (ex: 沒有 tags 或 description)

可以更改`archetypes/default.md`來指定想要的 Front matter 欄位

Front matter 是在本文之前像是 metadata 的欄位，ex:

```
+++
date = '2026-05-02'
draft = false
title = 'Hugo 常用指令 & 遇到的小問題'
description = "記錄一下自己常用的指令，其他可用參數可由公式的 Docs 取得"
tags = ["hugo"]
+++
```

#### Reference

- [Hugo Docs (Front matter)](https://gohugo.io/content-management/front-matter/ "https://gohugo.io/content-management/front-matter/")
