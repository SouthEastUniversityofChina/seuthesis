http://bbs.seu.edu.cn/bbstcon.php?board=TeX&gid=3510

发信人: oldoldstone (阿蒙), 信区: TeX 
标  题: seuthesis 2.1.2 在texlive2012中编译不通过的解决方案 
发信站: 虎踞龙蟠SBBS (Sat Sep  1 20:26:39 2012), 站内 

系统又自动升级了texlive2012，发现编译不过去，错误提示 
Package caption Error: Can be used only in preamble 
摸索了一下临时的解决方案： 
1. 搜索seuthesis-utf8.cfg文件中的以下代码 

\DeclareCaptionFont{capFont}{\song\wuhao} % 表格名及图名用5号宋体 
\DeclareCaptionLabelSeparator{twospace}{~~} 
\captionsetup{ 
  labelsep=twospace,% 去掉图标签后的冒号 
  font={capFont},% 
  figurename=图,% 
  tablename=表,% 
  listfigurename=插图目录,% 
  listtablename=表格目录} 

用%注释或者删除。 

2 将上述代码添加到 seuthesis.cls文件中。我加在下列代码的上面。 
\AtBeginDocument{\CJKindent{}% 
    \InputIfFileExists{seuthesis-utf8.cfg}% 引入配置文件 
    {\typeout{[seuthesis]: Load seuthesis-utf8.cfg successfully!}}% 
    {\typeout{[seuthesis]: Load seuthesis-utf8.cfg failed!}}% 
    \makeindex% 
    \wuhao% 
    \linespacing{\mainlineskip} 
  } 

最后特别感谢seuthesis 的作者，极大方便了东大的TeXers。 
分享一下我的经验，特别适用于对LaTeX的文本模式畏惧的tx：使用\input将每章分开写，用半可视化的lyx编辑器写，导出LaTex文件，然后将所有LaTeX文件头尾去掉，最后编译。当然这些工作一个批处理就搞定了。 

