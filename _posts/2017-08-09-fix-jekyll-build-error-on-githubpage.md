---
layout: post
title: 解決github上Jekyll編譯出錯
description: "Fix Jekyll Build Error On Githubpage."
modified: 2017-08-09
tags: [Ubuntu, Jekyll, MarkUp]
image:
  feature: abstract-0.jpg
  credit: Good things are happening...
  creditlink:
  background:
---


**編前推薦：**<a href="https://atom.io/">Atom Editor</a> `https://atom.io/`

`
Atom is a text editor that's modern, approachable, yet hackable to the core—a tool you can customize to do anything but also use productively without ever touching a config file.
`

由於對Jekyll這個東西還不熟，github上給出編譯失敗的信息卻沒有給出出錯的位置，所以搞了一晚上才解決了編譯問題。
得到的經驗是，github上編譯報錯的能力很差，一定要在本地搞好編譯環境，才能快速定位問題所在。
我的提交見: <a href="https://github.com/Grampuses/grampuses.github.io/commit/ad263e399f91b2f3e203d1a8d19844332316fc8e">ad263e3</a>

1. 由於Jekyll所依賴編譯環境經常會更新，所以一旦出現在本地編譯通過，在github上編譯失敗的時候。
一定要想到更新編譯工具，一定要先更新下ruby（一定要ruby的dev版本，普通版本可能沒有相關功能而導致編譯失敗）。
```
$ sudo apt install ruby-dev
```

2. 進入Jekyll代碼目錄
```
$ cd /home/yangzh6/work/github/grampuses.github.io
```

3. 更新bundle，在代碼目錄下執行下面的指令（如果不更新，也可能會導致編譯失敗，所以如果遇到編譯失敗，要記得更新下bundle）。
<a href="https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/#keeping-your-site-up-to-date-with-the-github-pages-gem">
Jekyll is an active open source project and is updated frequently. As the GitHub Pages server is updated, the software on your computer may become out of date, resulting in your site appearing different locally from how it looks when published on GitHub.
</a>
```
$ bundle update
```
然後再clean下Jekyll項目。
```
$ bundle exec jekyll clean
```

4. 重新編譯這個Jekyll程序
```
$ bundle exec jekyll build
```

5. 如果遇到“Liquid Exception: Can't convert Hash into String. in feed.xml”這個錯誤，
請在`_config.xml`中將`- jekyll-feed`去掉，然後再編譯下。

6. 解決完所有編譯錯誤後，執行下面指令啓動本地Jekyll服務器，這樣就可以通過瀏覽器訪問<a href="http://localhost:4000/">http://localhost:4000/</a>來查看最終效果。
```
$ bundle exec jekyll serve
```
