---
title: vim 常用命令
date: 2022-10-27 14:38:07
updated: 2022-10-27 17:53:36
categories: vim
tags: vim
description:
top_img: https://iili.io/DpU62s.jpg
cover: https://iili.io/DpU62s.jpg
---


`j`: ↓

`k`: ↑

`h`: ←

`l`: →

`x`: 删除字符

`i`: 插入字符

`A`: 在行尾追加字符

`:q!`: 强制退出, 不保存文件

`:wq`: 保存文件并退出

`dw`: 删除一个单词, 删除至下一个单词的首字母(不包含)

`de`: 删除一个单词, 删除至当前单词的最后一个字母(包含)

`d$`: 删除至行尾

`w`: 移动光标至下一个单词的首字母

`e`: 移动光标至下一个单词的最后一个字母, 如果光标不在单词的最后一个字母, 则移动至当前单词的最后一个字母

`<number>w`: 移动光标至下 `<number>` 个单词的首字母; 例: `2w`

`<number>e`: 移动光标至下 `<number>` 个单词的最后一个字母; 例: `2e`

`0`: 移动光标至行首

`d<number>w`: 删除 `<number>` 个单词; 例: `d2w`

`dd`: 删除当前行

`<number>dd`: 删除 `<number>` 行

`u`: 撤销最后一个命令

`U`: 撤销当前行的所有命令

`CTRL-R`: 撤销撤销命令

`p`: 在光标处粘贴先前删除的文本

`r<x>`: 将光标处的字符替换为 `x`

`ce`: 从光标处更正单词至词尾; 相当于命令 `de` + `i`

`cc`: 更正光标所在行; 相当于命令 `dd` + `i`

`cw`: 相当于命令 `dw` + `i`

`c$`: 相当于命令 `d$` + `i`

`CTRL-G`: 显示你在文档中的位置和文档状态

`G`: 定位至文档末尾

`gg`: 定位至文档开头

`<number>G`: 定位至第 `<number>` 行

`/`: 向下搜索文档, `n` 匹配下一个, `N` 向前搜索

`?`: 向前搜索文档

`CTRL-O`: 向后移动, 返回之前的位置

`CTRL-I`: 向前移动

`%`: 匹配 `(`, `)`, `[`, `]`, `{`, `}`; 将光标放在其中一个括号上, 按下 `%`, 光标会移动至与之匹配的括号上

`:s/old/new/g`: 将 old 替换为 new; 替换当前行的所有 old

`:s/old/new`: 只替换当前行第一个匹配到的 old

`:#,#s/old/new/g`: 替换两行间所有匹配的 old

`:%s/old/new/g`: 替换文档中所有匹配的 old

`:%s/old/new/gc`: 查找文档中所有匹配的 old 并给出是否替换的提示

`:!`: 执行外部命令

`:w <FileName>`: 文件另存为

`v`: 开始选择文本

`:r <FileName>`: 取回 `<FileName>` 中的文本并置于光标之后; 也可以读取外部命令的执行结果, 如: `:r !ls`

`o`: 在光标的下一行新增一行

`O`: 在光标的上一行新增一行

`a`: 在光标后插入字符

`R`: 替换多个字符

`y`: 拷贝

`:set <option>`: 设置选项

`:help`: 打开帮助文件
