# Matplotlib doesn't support Chinese   
## 问题描述
Matplotlib无法识别中文字符的Unicode，调用plot.show()函数后，原中文字符处由方框代为显示。   

![Garbled Characters](./Images/Garbled%20Characters.png)

**运行环境：Ubuntu 20.04 LTS，Python 3.10.*，matplotlib 3.8.3**

## 解决方法
手动下载支持Unicode中文解码的字体，给出几个例子：   
* 简体中文 SimSun.ttf
* 黑体 HeiTi.ttf
* 雅黑 Yahei.ttf
* ...

***注意***，如果使用`ttf-microsoft-installer`提供的`fc-match`指令，是无法下载上文描述的字体ttf文件的，为避免后续麻烦，最好手动下载。     

1. 下载完执行如下指令,将字体复制到你的matplotlib中：   

```bash
path2ttf=$(find | grep -m 1 "SIMSUN.ttf")
path2yourvenv=$(sudo find | grep "matplotlib" | grep -m 1 "mpl-data")
cp $path2ttf $path2yourvenv/fonts/ttf/
```

2. 刷新你的**matplotlib font manager cache**，自行创建一个scritp.py并将下述命令键入并执行:   
```python 
import matplotlib.font_manager
matplotlib.font_manager._load_fontmanager(try_read_cache=False)
```

3. matplotlib可以解释中文了    

![Chinese Charecters](./Images/Chinese%20Charecters.png)

## Referrence Links
1. Refresh matplotlib font manager cache   

    [Stack Overflow Post]("https://stackoverflow.com/questions/37920935/matplotlib-cant-find-font-installed-in-my-linux-machine")

2. Download SimSun.ttf for free

    [SimSun For Free]("https://www.dafontfree.io/simsun-font/")

