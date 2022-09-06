---
title: hexo-renderer-marked 渲染器配置
date: 2022-09-06 11:08:10
updated: 2022-09-06 11:08:10
categories: hexo
tags: 
    - hexo
    - hexo-renderer-marked
top_img:
cover: https://iili.io/6hT2ee.png
---


## markdown 中的锚点问题

markdown 中的锚点会自动将所有大写字母转换为小写。例如，锚点为：

```markdown
### 现代 Unix 密码破解
```

则链接会转换为：

```markdown
[查看](#现代-unix-密码破解)
```

而 `hexo-renderer-marked` 渲染器默认情况无法识别，必须是 `[查看](#现代-Unix-密码破解)` 才能识别。

可以通过修改配置来转换大小写。在 Hexo 的 `_config.yml` 配置文件中添加：

```yaml
marked:
  modifyAnchors: 1   #modifyAnchors - Transform the anchorIds into lower case (1) or upper case (2).
```

更多 `hexo-renderer-marked` 配置请见[官方文档](https://github.com/hexojs/hexo-renderer-marked#options)。
