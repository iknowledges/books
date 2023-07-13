# 1.Introduction to OpenCV and Qt

## Installing Qt

### Where to get it?

Download from the following folder: qt/5.9/5.9.1/

- For Windows: *qt-opensource-windows-x86-5.9.1.exe*
- For macOS: *qt-opensource-mac-x64-5.9.1.dmg*
- For Linux: *qt-opensource-linux-x64-5.9.1.run* 

officially released versions: [https://download.qt.io/official_releases/](https://download.qt.io/official_releases/)

previous versions: [https://download.qt.io/archive/](https://download.qt.io/archive/)

### How to install?

Execute the following command to make installer file executable if you are using Linux:

```bash
chmod +x qt-opensource-linux-x64-5.9.1.run
./qt-opensource-linux-x64-5.9.1.run
```

#### Windows users

When installing Qt for Windows, on the Select Components dialog, make sure you check the checkbox next to the msvc2015 32-bit option. (选择msvc2015必须安装对应的编译器，否则也可以选择MinGW而不用安装其他编译器)

**An important thing to note for Windows users**: You need to also install Visual Studio 2015 with at least C++ desktop development features enabled in it.

#### Linux users

When installing Qt for Linux, on the Select Components dialog, make sure you select (at least) Desktop GCC (32 bit or 64 bit, depending on your OS).

Run the following command from a terminal:

```bash
sudo apt-get install build-essential libgl1-mesa-dev
```

For more information on this, you can refer to http://doc.qt.io/qt-5/linux.html.

Run QtCreator:

```bash
./Qt5.9.1/Tools/QtCreator/bin/qtcreator &
```

Uninstall Qt:

```bash
./Qt5.9.1/MaintenanceTool
```

## Installing OpenCV

### Preparing for an OpenCV build

CMake website download page: https://cmake.org/download/

### Where to get OpenCV?

OpenCV maintains its official and stable releases under the Releases page at their website: https://opencv.org/releases/

```bash
unzip 3.3.0.zip
```

### How to build?

Linux users should run the following command in a terminal before proceeding with the OpenCV build:

```bash
sudo apt-get install libgtk2.0-dev pkg-config
```

Install CMake GUI application and run it:

```bash
sudo apt-get install cmake-gui
cmake-gui
```

- (1) Set the following two folders:
  - Where is the source code: /home/admin/software/opencv-3.3.0
  - Where to build the binaries: /home/admin/software/opencv-3.3.0/build

![How-to-build-1](https://github.com/iknowledges/BookImage/raw/main/ComputerVisionWithOpenCV3AndQt5/How-to-build-1.jpg)

- (2) Click on the `Configure` button, select the correct generator and click Finish:
  - Windows users: select Visual Studio 14 2015.
  - macOS and Linux users: select Unix Makefiles.
- (3) Set parameters to configure your OpenCV build:
  - Check the checkbox next to the **BUILD_opencv_world** option.
  - Add Entry -> Name:CMAKE_CXX_STANDARD, Type:STRING, Value:11.
- (4) Click on the `Configure` button again and finally click on the `Generate` button.

For the next part, you'll need to execute somewhat different commands if you're using Windows, macOS, or Linux operating systems. So, here they are:

**Windows users**: Go to the OpenCV build folder. There should be a Visual Studio 2015 Solution that you can easily execute and build OpenCV with. You can also immediately click on the Open Project button, which is right next to the Generate button on CMake. After Visual Studio is opened, you need to select Batch Build from the Visual Studio main menu. It's right under Build:

![How-to-build-2](https://github.com/iknowledges/BookImage/raw/main/ComputerVisionWithOpenCV3AndQt5/How-to-build-2.jpg)

Make sure checkboxes in the Build column are enabled for **ALL_BUILD** and **INSTALL**, as shown in the following screenshot:

![How-to-build-3](https://github.com/iknowledges/BookImage/raw/main/ComputerVisionWithOpenCV3AndQt5/How-to-build-3.jpg)

**For macOS and Linux users**: Switch to the Binaries folder you chose in CMake and execute the following commands:

```bash
sudo make
sudo make install
```

## Configuring OpenCV installation

Create a file named `opencv.pri` in the same folder you used for OpenCV build (Technically speaking, this file can be located anywhere on your computer) and write the following inside this PRI file:

- Windows users:

```
INCLUDEPATH += c:/dev/opencv/build/install/include
Debug: {
  LIBS += -lc:/dev/opencv/build/install/x86/vc14/lib/opencv_world330d
}
Release: {
  LIBS += -lc:/dev/opencv/build/install/x86/vc14/lib/opencv_world330
}
```

There's one more thing left for Windows users, and that is adding OpenCV DLLs folder to the PATH environment variable.

- macOS and Linux users:

```
INCLUDEPATH += /usr/local/include
LIBS += -L/usr/local/lib \
-lopencv_world
```

## Testing OpenCV installation

Run Qt Creator and Create a new Console Application named `QtCvTest`.

- QtCvTest.pro

```
QT += core
QT -= gui
CONFIG += c++11
TARGET = QtCvTest
CONFIG += console
CONFIG -= app_bundle
TEMPLATE = app
SOURCES += main.cpp
DEFINES += QT_DEPRECATED_WARNINGS
# include the PRI file
include(/home/admin/workspace/opencv.pri)
```

- main.cpp

```cpp
#include <QCoreApplication>
#include "opencv2/opencv.hpp"

int main(int argc, char *argv[])
{
    QCoreApplication a(argc, argv);
    using namespace cv;
    Mat image = imread("/home/admin/workspace/test.jpg");
    imshow("Output", image);
    return a.exec();
}
```
