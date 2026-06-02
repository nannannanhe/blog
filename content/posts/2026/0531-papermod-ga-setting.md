+++
date = '2026-05-31'
draft = false
title = '在 Hugo 靜態網站設定 Google Analytics（PaperMod Theme）'
tags = ["Hugo", "PaperMod", "GoogleAnalytics"]
description = "記錄在 hugo.toml 設定了 googleAnalytics 但不 work 後的解決方法"
+++

## 背景

- Hugo v0.155.3
- PaperMod Theme

## 不 work 的設定方法

忘記是在哪裡看到，可能是 PaperMod 的某篇關於 `hugo.toml` 裡各參數設定的範本？在 `hugo.toml` 裡如下設定了 GoogleAnalytics 的評估 ID，但不 work。  
在產生的靜態網頁裡沒有關於 GA4 的記述。

```
googleAnalytics = 'G-XXXXXXX'
```

## Claude Code 的解法

某天想起這件事，和 Claude Code 商量後，他提出的解法是在`layouts/partials/`下新增`extend_head.html`檔案，內容如下：

```
// GoogleAnaltyics 提供的代碼直接貼上
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-XXXXXXX');
</script>
```

然後就 work 了。:tada::tada:

ClaudeCode 的說法如下：

```
PaperMod 有專門的 extend_head.html 擴充點，讓我確認它的內容。

PaperMod 的 extend_head.html 就是為此設計的覆蓋點。只需在專案的 layouts/partials/ 建立同名檔案即可覆蓋主題版本，不用動 theme 目錄。

googleAnalytics 欄位沒作用是因為 PaperMod 沒有使用 Hugo 內建的 GA 模板，它只靠 extend_head.html。完成。確認 head.html 在第 197 行會 include 這個 partial，所以每個頁面的 <head> 都會注入 GA 代碼。

幾點補充：

不要動 themes/ 目錄：layouts/partials/extend_head.html 會自動覆蓋主題裡的同名檔案，Hugo 的 lookup 順序保證了這一點。
hugo.toml 裡的 googleAnalytics 欄位可以保留也可以刪除，對 PaperMod 沒有作用，不影響現在這個做法。
本地測試時 GA 不會觸發（因為 localhost 不在 GA 的追蹤域），部署到 GitHub Pages 後才會生效。
```

## 查了 PaperMod 的 Source 後覺得或許更佳的解法？

想記錄一下解決方法寫這篇時查了一下，發現 Hugo 的官方文件裡其實有介紹直接利用 hugo.toml 的方法 ([link](https://gohugo.io/templates/embedded/#google-analytics))。

好奇 search 了一下 PaperMod 的 source 裡有沒有關於 `.Site.Config.Services.GoogleAnalytics.ID`的記述，沒有 hit。但 search `extend_head`後在`PaperMod/layouts/partials/head.html`找到以下內容：

```
{{- partial "extend_head.html" . -}}

{{- /* Misc */}}
{{- if hugo.IsProduction | or (eq site.Params.env "production") }}
{{- partial "google_analytics.html" . }}
{{- partial "templates/opengraph.html" . }}
{{- partial "templates/twitter_cards.html" . }}
{{- partial "templates/schema_json.html" . }}
{{- end -}}
```

參照 PaperMod 的 source，或許新增`layouts/partials/google_analytics.html`存放 GA4 的代碼是較佳的做法？

## 直接利用`hugo.toml`的設定方法

參考 Hugo 的官方文件 ([link](https://gohugo.io/templates/embedded/#google-analytics))，在 hugo.toml 做如下的設定：

```
[services]
  [services.googleAnalytics]
    id = 'G-MEASUREMENT_ID'
```

在沒有新增`layouts/_partials/google_analytics.html`去 override 的情況下，生成的靜態網頁裡關於 GA4 的記述如下：

```
    <script async src="https://www.googletagmanager.com/gtag/js?id=G-MEASUREMENT_ID"></script>
      <script>
        var doNotTrack = false;
        if ( true ) {
          var dnt = (navigator.doNotTrack || window.doNotTrack || navigator.msDoNotTrack);
          var doNotTrack = (dnt == "1" || dnt == "yes");
        }
        if (!doNotTrack) {
          window.dataLayer = window.dataLayer || [];
          function gtag(){dataLayer.push(arguments);}
          gtag('js', new Date());
          gtag('config', 'G-MEASUREMENT_ID');
        }
      </script>
```

work! :tada::tada:

## 感想

單就 work 不 work 而言，利用 ClaudeCode 去改其實很快，也不用一直查技術文件，成就感很高。但他的說法其實似是而非，比方說：

> PaperMod 的 extend_head.html 就是為此設計的覆蓋點。

以 GA 的擴充點而言，比起`extend_head.html`，使用`google_analytics.html`好像更合適？

> googleAnalytics 欄位沒作用是因為 PaperMod 沒有使用 Hugo 內建的 GA 模板，它只靠 extend_head.html。

googleAnalytics 欄位沒作用是因為我的`hugo.toml`寫法根本就錯了，而 PaperMod 其實有使用 Hugo 內建的 GA 模板

> 本地測試時 GA 不會觸發（因為 localhost 不在 GA 的追蹤域），部署到 GitHub Pages 後才會生效。

以我實測的狀況，其實 localhost 仍然有觸發 GA

但很快就改好完成我想要做的事仍然很棒就是了。只是不一定會是最佳解。  
並且容易得到一些不一定正確的知識...

### Reference

- [Hugo](https://gohugo.io/)
- [PaperMod](https://adityatelange.github.io/hugo-PaperMod/)
