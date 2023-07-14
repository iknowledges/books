# 第6章 对话框与多窗体设计

### 6.1.2 QFileDialog对话框

1. 选择打开一个文件

若要打开一个文件，可调用静态函数QFileDialog::getOpenFileName()，“打开一个文件”按钮的响应代码如下：

```cpp
void Dialog::on_btnOpen_clicked()
{ //选择单个文件
   QString curPath=QDir::currentPath();//获取应用程序当前目录
   QString dlgTitle="选择一个文件"; 
   QString filter="文本文件(*.txt);;图片文件(*.jpg *.gif);;所有文件(*.*)";
   QString aFileName=QFileDialog::getOpenFileName(this, dlgTitle, curPath, filter);
   if (!aFileName.isEmpty())
      ui->plainTextEdit->appendPlainText(aFileName);
}　
```

QFileDialog::getOpenFileName()函数需要传递3个字符串型参数，分别如下：
- 对话框标题，这里设置为"选择一个文件"。
- 初始化目录，打开对话框时的初始目录，这里用QDir::currentPath()获取应用程序当前目录。
- 文件过滤器，设置选择不同后缀的文件，可以设置多组文件，每组文件之间用两个分号隔开，同一组内不同后缀之间用空格隔开。

QFileDialog::getOpenFileName()函数返回的是选择文件的带路径的完整文件名，如果在对话框里取消选择，则返回字符串为空。

2. 选择打开多个文件

若要选择打开多个文件，可使用静态函数QFileDialog::getOpenFileNames()，“打开多个文件”按钮的响应代码如下：

