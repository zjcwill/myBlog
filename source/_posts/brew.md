---
title: brew
date: 2019-05-18 10:21:40
tags: [brew]
---

brew 是 macOS 一款包管理。通过替换国内源，可以节约下载时长。

## brew 更换国内源 

替换brew.git:

```bash
cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git
```
替换homebrew-core.git:

```bash
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
```

重置brew.git:

```bash
cd "$(brew --repo)"
git remote set-url origin https://github.com/Homebrew/brew.git
```

重置homebrew-core.git:

```bash
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://github.com/Homebrew/homebrew-core.git
```