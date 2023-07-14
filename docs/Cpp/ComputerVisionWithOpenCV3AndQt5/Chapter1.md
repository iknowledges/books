# 1.Introduction to OpenCV and Qt

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
