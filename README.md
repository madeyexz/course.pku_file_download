# 自动化批量下载教学网课件(PKU)

Ian Xiao

20220223

### 零、说明

1. 成功经过《普通生物B》与《数据库概论（实验班）》测试
2. 如果使用时发现，脚本只能在Chrome中“打开”这些pdf而不是“下载”这些pdf，可以在Chrome的「设置 > 安全与隐私设置 > 网站设置 > 更多内容设置 > PDF文档」中将默认行为设置成“下载PDF文件”

### 一、初始化

1. 登入教学网，打开 `课程内容`
2. <kbd>⌘ + ⌥ + I</kbd> 或 <kbd>F12</kbd> 或右上角打开`开发者工具`
3. 在`element`栏目点开`<body id: ..>`里，右键`Edit as HTML`，然后把所有内容复制下来
4. `cd ~/Desktop; vim html.txt`(或在桌面新建`html.txt`), 把刚才复制的内容黏贴进去

### 二、一行代码版本（MacOS）

```bash
grep -o -e '/bbcswebdav/[^"]*_1' html.txt | sed 's/^/https:\/\/course.pku.edu.cn/' | xargs open
```

### 三、按步骤执行（MacOS & Windows）

#### （一）获得教学网的链接

1. 获得教学网与下载链接相关的链接

   ````bash
   grep -o -e '/bbcswebdav/[^"]*_1' html.txt > file.txt
   ````
   
2. 加上网站前缀 

   ````bash
   sed -i -e 's/^/https:\/\/course.pku.edu.cn/' file.txt
   ````
   
   如此链接便都配置好了

#### （二）下载

1. MacOS: 为了使用chrome快速下载，我们先配置一个`alias`

   ``` bash
   alias chrome='/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome'
   ```
   
   再来 `for i in file.txt; do chrome $i; done` 完成！
   
2. 其它系统 (Windows)：可以使用chrome插件 [Open Multiple URLs](https://chrome.google.com/webstore/detail/open-multiple-urls/oifijhaokejakekmnjmphonojcfkpbbh)，手动复制 `file.txt`中的内容，然后黏贴到插件中。
   

（应该有 `curl` 等命令可以用，但我现在还没搞明白，以后再说吧）
