# makeWindowsIcon
制作windows下应用程序的图标（以便通过Py2exe打包Python程序为exe时能有一个漂亮的程序图标）

笔者之前用PyQ4写GUI程序，然后通过Py2exe导出为可在windows上独立运行的exe，示例的Python脚本如下：
```python
#-*- coding: utf-8 -*-
from distutils.core import setup
import py2exe

setup( zipfile=None,
       windows=[{"script":"main.py", "icon_resources":[(1, "logo.ico")]}],
	   options={"py2exe":{"compressed":2, "bundle_files":1,
                          "includes":["sip", "PyQt4.QtGui", "PyQt4.QtCore"],
                          "dll_excludes": ["msvcm90.dll", "msvcp90.dll", "msvcr90.dll"] }})
```

起初是随便在网上找了一些ico作为程序的图标，结果发现生成exe后有的ico可以，有的却无法显示。后来发现Windows的Icon其实由多个不同尺寸的图片拼合而成的。
具体的方法如下所述，以便日后使用时查阅：

1. 下载喜欢的图标(png格式)
2. 为该png图标生成四种尺寸：248x248，48x48，32x32，16x16
3. 下载png2ico.exe命令行工具，然后在图片所在目录中执行：

png2ico.exe  logo.ico  demo248.png demo48.png demo32.png demo16.png

生成的logo.ico即可作为程序的图标，在Windows下正常显示。
