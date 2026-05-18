+++
date = '2026-05-17'
draft = true
title = '使用Claude Code製作 KFC PFC Calculator ①'
tags = ["Claude Code", "side projects"]
description = "使用Claude Code製作小型Web Application的紀錄"
+++

記錄下的指令和過程、token花費。  
使用Claude Pro Plan。

repo: https://github.com/nannannanhe/kfc-jp-pfc-checker

## idea

有陣子很在意自己到底攝取多少蛋白質，吃完速食會去官網找成份表。  
因而發現日本麥當勞官網本身就有[營養成份計算器](https://www.mcdonalds.co.jp/products/nutrition_balance_check/, "栄養バランスチェック")，可以自由選擇點餐的內容來計算各成份含量，不會被套餐綁住，但日本肯德基只有公布一覽表的 pdf，要自己計算。

如果可以從 pdf 抽出各餐點成份含量的 json 嵌在 html 裡，應該可以只靠前端做出功能類似的簡易 PFC 計算器。功能包含選擇各類餐點(可複選，也可單品選擇多份)，並計算加總的成份含量。

## 使用 claude.ai 製作 CLAUDE.md

在之前就曾經就這個idea和各家ai商量過想法和架構，打算用沒有碰過的Svelte來做。

中間忙別的事，放置這個idea一段時間後，有一陣子一直看到各種文章說 Claude Code 多厲害又多厲害，又剛好聽到敏迪也在 podcast 中介紹，想說玩玩看，決定用這個idea來試。

其實就連claude.ai也是第一次用。(不過之前用 VsCode GitHub Copilot 時應該是有用過Claude家的model) 因為我的ChatGPT當時不知為何沉迷於先說我說得很對然後否定我說我走偏了他想要「給我一個更乾淨的結論」然後硬要給我建議，搞得我很煩，所以claude.ai不會硬給建議的風格給我非常好的印象。  
順帶一提，在我和gemini討論Claude和ChatGPT的行為後，ChatGPT突然就收歛了，why???
