---
title:  "Linux 筆記 - KornShell (ksh) 底下的 vi 模式"
subtitle: ""
categories: []
---

# ksh 下的 vi mode
開始講這個故事之前請大家回想一下，在 Linux shell 底下使用文字介面操作時（以我個人來說是 Ubuntu 預設的 bash shell），如果不小心打錯字，比如說 `ls -l | grep -P abc` 不小心手滑打成了 `ls -l | grep -i abc` 這時你會怎麼做？我的直覺是按下方向鍵左鍵到 `-i` 旁邊然後按 backspace 刪除打錯的 `i` 再按下正確的 `P` 這樣（Backspace 一路到底跟 Ctrl + c 全部重打派這裡先不討論XD）。

某天偶然聽聞某單位的主機在 KornShell (ksh) 某種神秘的設定下，要修改這種錯誤必須：
  1. 按方向鍵左鍵到 `-i` 的 `i` 上面
  2. 此時 Backspace 會不能用（如果一開始不按方向鍵的話就可以一路 Backspace 回去），所以得用 x 鍵刪除打錯的 `i`
  3. 此時還無法直接打上新的 `P`，得按下 i 鍵之後才能打上想要加入的字元

嗯？怎麼聽起來好像跟 vi 的操作模式有點似曾相似，上網一查才發現原來在 shell 底下也有分 vi 跟 emacs 的操作模式，原來編輯器聖戰早已燒出了編輯器本身之外啊...（亂講）。而上面所描述的的確就是 vi mode 的行為。對於用慣了 bash 的 emacs 模式但根本不知道有這種東西存在的我來說實在可說是 mind blowing XD，雖然平常寫程式用 vim ，但舊 vi 的操作早也忘得差不多了，只依稀記得以前教授在介紹這編輯器的時候還有發一張 cheatsheet 給大家XD。（有安裝 vim 想試試看舊 vi 的朋友可以在 vim 裡面輸入 `:set compatible` 來試試）

![想起了曾被困在 vi 裡面出不來嗎？](/images/2021-10-ksh-vi/ksh-vi.jpg)
[stackoverflow: How do I exit the Vim editor?](https://stackoverflow.com/questions/11828270/how-do-i-exit-the-vim-editor)

有興趣想試試看的話可以下 `ksh -o vi` 來看看～

受此苦難的人們啊，set -o emacs 是你們的救贖

Reference: [StackExchange: What is meant by a shell is in "vi" mode or "emacs" mode?](https://unix.stackexchange.com/questions/85390/what-is-meant-by-a-shell-is-in-vi-mode-or-emacs-mode)
