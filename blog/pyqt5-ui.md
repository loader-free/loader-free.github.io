### PyQt5  两种加载ui方式的优缺点

本人使用pyqt5中，发现有两种方式加载ui文件，研究了一下各自的优缺点。

pyuic5：

1. 优点：
- 允许继承（这点很关键）
- 运行程序时没有额外的负载

2. 缺点：
- 每次修改ui文件时都得手动将 .ui 转换为 .py



pyuic5使用例程代码:

代码高亮

```python

from PyQt5 import QtWidgets, uic
import sys
 
from PyQt5.QtWidgets import QMainWindow
 
# 导入pyUIC转化出来的.py文件,Ui_Form就是转化出的.py文件的类名
from untitled import Ui_Form
 
 
class Ui(QMainWindow, Ui_Form):
    def __init__(self, parent=None):
        super(Ui, self).__init__(parent)
        self.setupUi(self)
 
 
app = QtWidgets.QApplication(sys.argv)
window = Ui()
window.show()
sys.exit(app.exec_())

```




uic.loadUi():
1. 优点：
- 修改ui时无需修改任何内容[^1]
- 编译额外时间（我也没太看懂）

2. 缺点：
- 不允许继承（或许使用uic.loadUiType()来实现继承？）[^2]
- 不允许使用代码检查、自动补全


uic.loadUi()函数的使用例程代码 :[^3]

```python

from PyQt5 import QtWidgets, uic
import sys
 
 
class Ui(QtWidgets.QMainWindow):
    def __init__(self):
        super(Ui, self).__init__()
        uic.loadUi('main.ui', self)
 
 
app = QtWidgets.QApplication(sys.argv)
window = Ui()
window.show()
sys.exit(app.exec_())

```



---

<font size=4>.END.</font>





