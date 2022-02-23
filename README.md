# 批量下载教学网文件教程(PKU)

Ian Xiao

20220223

### 零、说明

1. 仅使用普通生物B测试过，不过方法大同小异。

### 一、初始化

1. 登入教学网，打开 `课程内容`
2. `⌘ + ⌥ + J` 或右上角打开开发者工具
3. 在`element`栏目点开`<body id: ..>`里，右键`Edit as HTML`，然后把所有东西复制下来
4. `cd ~/Desktop; vim html.txt`, 把刚才复制的文件黏贴

### 二、获得教学网的链接

1. 获得教学网与下载链接相关的链接

   ````bash
   grep -o -e '/bbcswebdav/[^"]*_2' html.txt > file.txt
   ````

2. 加上网站前缀 

   ````bash
   sed -i -e 's/^/https:\/\/course.pku.edu.cn/' file.txt
   ````

### 三、下载

1. MacOS: 为了使用chrome快速下载，我们先配置一个`alias`，如果你不是

   ``` bash
   alias chrome='/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome'
   ```

2. 其它系统 (Windows)：可以使用chrome插件 [Open Multiple URLs](https://chrome.google.com/webstore/detail/open-multiple-urls/oifijhaokejakekmnjmphonojcfkpbbh)，手动复制 `file.txt`中的内容，然后黏贴到插件中。

3. `for i in file.txt; do chrome $i; done` 完成！

   

   

（应该有 `curl`等命令可以用，但我现在还没搞明白，以后再说吧）
