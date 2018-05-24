---
layout:     post                    
title:      打开任意路径的文件夹在 Jupyter Notebook               
subtitle:     
date:       2018-05-16              
author:     Bear                     
header-img: img/0409.PNG    
catalog: true                       
tags:                              
    - 生活常识
---

假如要打开文件夹 C:\Users\Bear\document\py_script

Windows+R 打开 run

输入 `cmd`

在 `>` 后边依次输入 `C:\Users\Bear>C:`，然后依次 `C:\Users\Bear>cd\`，`C:\>cd Users\Bear\document\py_script`。出现 `py_script` 文件夹之后，在 `>` 后边输入 `jupyter notebook`，就可以查看这个文件夹里的 `*.ipynb` 文件了。

一把年纪的我第一次用这个，感谢 CSDN 的各位大佬（