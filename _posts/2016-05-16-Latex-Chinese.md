---
layout: post
title:  "How to support Chinese in Latex"
date:   2016-05-16
excerpt: "Two ways to support Chinese fonts in Latex"
tag:
- Latex 
- Chinese 
- xelatex 
comments: true
---

> 该文目的在于讨论如何让Latex支持中文文档的书写。本文介绍两种常见的方法，推荐读者使用第二种方法


### CJK package

[**Latex**](https://www.latex-project.org/) 是基于Tex排版系统的文档书写系统。Tex排版系统最早由
[Prof. Donald Knuth](http://www-cs-faculty.stanford.edu/~knuth/)发明。然而该系统使用的不是unicode
编码,导致在本质上就不能支持中文输入，同时它不能使用系统字体,造成了很多不便。所以早期 Latex 通过外
置的包来支持中文输入，即大家常提到的 CJK package，但是其使用中据说有很多BUG。其Demo文档如下:

<script src="https://gist.github.com/Chenlonw/b0bb9c8e55a3c5392f1b27f37aaab949.js"></script>

可以直接采用`pdflatex`编译上面文档，得到中文支持。简单情况下使用少量中文可以采用该方法。

### Xelatex+xeCJK

Xetex和Tex在同一个层面上，都是排版系统。Xetex是目前公认的对中文支持最好的方法，简单不需要多余的配置。
采用Unicode进行编码，本质上支持多国语言，而且能够自由调用系统字体. 下面安装方法是就我自己的安装流程总结
，很多地方可能认识不足:

- 安装xetex: `sudo apt-get install texlive-xetex texlive-latex-extra`

- 安装中文字体:  
  + 查看现有的中文字体:`fc-list:lang=zh`  
  + 如果字体不全，可以从网上下载微软, adobe字体并拷贝到`/usr/share/fonts`或者 `~/.fonts`下.

字体安装流程如下:

sudo mkfontscale   
sudo mkfontdir   
sudo fc-cache -fv  
{: .notice}

-  生成一个package名为`zhfontcfg.sty`，该文件名字可以任意。该文件放在Latex存放宏包的地方(通常为`~/.texmf-var/tex/latex`),
 或者和你的Tex文档直接存放在一起。如果存放在默认宏包的地方，则需要执行安装`sudo mktexlsr`。

**zhfontcfg.sty/demo.tex:**
<script src="https://gist.github.com/Chenlonw/6c4332730d986e479a447d5b10992d2b.js"></script>

---

*参考文献：*   
[1.xetex完美中文配置](http://www.linuxdiyf.com/viewarticle.php?id=108646)   
[2.使用xelatex生成中文pdf](http://blog.jqian.net/post/xelatex.html)   
[3.Texlive2010 + Xetex +xeCJK 的中文配置](http://blog.sina.com.cn/s/blog_77f5a65c0101betb.html)  
