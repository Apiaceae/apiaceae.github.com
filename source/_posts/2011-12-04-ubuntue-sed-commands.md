--- 
layout: default 
title: "Ubuntu使用Sed命令批量替换文件夹中文件内的字符串" 
date: 2011-12-04 13:56
categories: linux
tags: sed
---

### linux sed 批量替换多个文件中的字符串
``` text
sed -i "s/oldstring/newstring/g" \`grep oldstring -rl yourdir\`
```

例如：替换/resources下所有文件中的[www.admin99.net](http://www.admin99.net)为admin99.net

```text
sed -i "s/www.admin99.net/admin99.net/g" \`grep www.admin99.net -rl /home\`
``` 

这个\` 符号是F1下边，tab键上边，数字1左边的那个，不是单引号 '
