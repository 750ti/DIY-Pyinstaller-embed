# DIY-Pyinstaller-embed 自定义更方便快捷的Python嵌入式打包程序  
根据Python嵌入式版本embeddable，搭配PyStand，自定义一个更加方便快捷的Python打包程序。

### 参考资料：
1. 知乎韦易笑大佬的开源嵌入式Python启动器：PyStand  [【知乎文章】](https://www.zhihu.com/question/48776632/answer/2336654649) / [【GitHub】](https://github.com/skywind3000/PyStand)  
2. embeddable版Python的内容参考了up主B-E-MAKE [【视频】](https://www.bilibili.com/video/BV1684y1z7Nj)

---
# Python程序/脚本，如何打包发布？
### **1.【Python嵌入式打包】**  
[【视频】](https://www.bilibili.com/video/BV1684y1z7Nj)-[【图文教程文章】](https://www.cnblogs.com/BEMAKE/p/16806999.html)  
1. 在Python官网下载 embeddable版本 32位 3.7/3.8版 [【链接Link】](https://www.python.org/downloads/windows/)
2. 解压zip文件
3. 下载`get-pip.py`文件，打开网站把内容复制粘贴到新建get-pip.py文件里保存，以`if --name--`结尾  [【链接Link】](https://bootstrap.pypa.io/get-pip.py)
4. 安装 pip包管理工具，约20MB 可不装，可在其他环境装了之后复制过去，节省空间。  
    1. 在文件路径上输入cmd打开命令管理器，`python get-pip.py`运行，下载`Lib` `Scripts`等文件夹，第三方库保存在Lib文件夹内。(关闭代理)
    2. **直接将上面的py保存到txt**，拖动文件到python.exe上可以直接打开，更加简单快捷。  
5. 记事本打开`python3x._pth` 删掉最后的#注释`#import site` 保存。# 我也不知道有什么用..  
6. **安装第三方库**，进入Scripts文件夹，打开cmd，使用正常的pip安装命令即可，如`pip install numpy`, 文件会被安装在当前环境的`Lib\site-packages`文件夹内
7. **运行程序**：
   1. 在`python.exe`目录打开cmd，键入`python.exe demo.py`即可运行`demo.py`
   2. 使用BAT批处理程序调用
        ```bat
        @echo off
        chcp 65001
        .\runtime\python.exe .\demo.py
        ```
   3. 使用知乎大佬的 PyStand程序调用 ↓ 


### **2.【PyStand】韦易笑大佬的嵌入式Python启动器**
[【知乎文章】](https://www.zhihu.com/question/48776632/answer/2336654649) / [【GitHub】](https://github.com/skywind3000/PyStand)  
1. 下载压缩包，解压 [【GitHub releases Downlows】](https://github.com/skywind3000/PyStand/releases)
2. **第三方库**，把电脑中相同的Python环境的库复制到`site-packages`(不过很容易漏掉，一个库通常包含多个文件夹)
3. 代码加密？ 加密方法见原作者描述
4. **运行程序**：
   - 运行`PyStand.exe`程序会调用`python`运行与程序同名的`.int`文件，比如`PyStand.int`，将py代码写入`.int`文件内即可
### 3. 【PyInstaller】
参考文章： [【知乎】](https://zhuanlan.zhihu.com/p/470301078) / [【CSDN过程+去坑】](https://blog.csdn.net/hdudb/article/details/122055537)  
1. 安装Pyinstaller，`pip install pyinstaller`
2. 在`.py`文件的目录运行打开cmd命令窗口
3. 命令行窗口输入`pyinstaller demo.py`即可。  
**其中，可以填入的一些参数选项：**  
`-F` 大写，是onefile，打包成单个独立exe程序  
(本质上就是1个自解压程序，将整个Python解释器解压至temp缓存目录再运行，关闭后又删除如此反复，所以启动速度迟钝、慢半拍)  
`-D` 大写,默认选项可不填。D是onedir，打包生成多个依赖文件和exe程序，放在一个文件夹内，略显凌乱，但启动速度快，可以在上层目录用 BAT调用程序启动。(或PyStand调用)  
`-c` 显示命令行窗口  
`-w` 不显示命令行窗口，去除黑框框  
`-i` 修改生成exe程序的图标，ico格式尺寸16x16、32x32等  
示例：`pyinstaller -w -i D:\123.ico demo.py`  
4. 其它可能会出现的问题，有些库可能打包不全，需要手动复制到文件夹内  
- Pyinstaller + UPX 打包程序（不太重要） [【相关视频】](https://www.bilibili.com/video/BV1j341137De/)

> 未完待续...

---

### 注意事项：
1. 为了更简单轻便，`PyStand.exe` 和 `run.BAT` 的启动方式，二选一即可，`PyStand.exe` 程序的注意事项请自行阅读原作者的文章 [【文章链接】](https://www.zhihu.com/question/48776632/answer/2336654649)  
2. 请注意Python解释器为32位，有些库可能不兼容32位，需要64位请自行去Python官网下64位版的embeddable嵌入式版  
3. 嵌入式版的Python压缩后大小为7M，解压后也仅十几M，我打包的包含了pip管理器和相关的库，以及PyQt5, 可自行删除。如`site-packages`和`Scripts`文件夹的内容。  
4.


> 未完待续...

---
### 目前发现的问题：
1. 由于是嵌入式版的原因，Python并没有自带`Tkinter` 库/模块，尝试了很多种方法都不行，导致一些小脚本想做一个带小窗口界面不能用简单的TK库，只能使用PyQt5这种稍微复杂/繁琐/庞大的库，又多浪费了几十MB的空间...  
（如果你有解决办法，希望大佬们可以在仓库的`lssues`反馈一下，或者发送邮件到`1209977969@qq.com`，同时我也会把内容更新到本仓库，谢谢大佬）  
2. 

> 欢迎反馈，未完待续...


---
### 我的打包文件下载
1. 在GitHub页面右边的 **发行版Releases**  
2. [【蓝奏云】](https://wwt.lanzoue.com/iE2XZ0eeqexc) 密码:diy  


---

### 更新日志：（倒序）  
2022年10月23日 发布在GitHub  
2022年10月22日 创建  




