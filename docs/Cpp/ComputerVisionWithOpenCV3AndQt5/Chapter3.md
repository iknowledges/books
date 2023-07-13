# 3.Creating a Comprehensive Qt+OpenCV Project

## Behind the scenes

So, we have the following in the `Hello_Qt_OpenCV` folder:

```
Hello_Qt_OpenCV.pro
Hello_Qt_OpenCV.pro.user
main.cpp
mainwindow.cpp
mainwindow.h
mainwindow.ui
```

The first file in the `Hello_Qt_OpenCV.pro` list is basically the first file that is processed by Qt when our project is built. This is called a **Qt Project file** and an internal Qt program called qmake is responsible for processing it.

### The qmake tool

For instance, we already know that including the following line in our Qt
Project file causes the addition of Qt's core and gui modules to our
application:

```
QT += core gui
```

These lines simply mean the `TARGET` name is `Hello_Qt_OpenCV`, which is the name of our project and the `TEMPLATE` type `app` means that our project is an application.

```
TARGET = Hello_Qt_OpenCV
TEMPLATE = app
```

This is how header files, source files, and user interface files (forms) are included in our project.

```
SOURCES += \
    main.cpp \
    mainwindow.cpp
HEADERS += \
    mainwindow.h
FORMS += \
    mainwindow.ui
```

This is how Qt can see OpenCV and use it in a Qt project.

```
win32: {
    include("c:/dev/opencv/opencv.pri")
}
unix: !macx{
    CONFIG += link_pkgconfig
    PKGCONFIG += opencv
}
unix: macx{
    INCLUDEPATH += "/usr/local/include"
    LIBS += -L"/usr/local/lib" \
    -lopencv_world
}
```

```cpp
#include "mainwindow.h"
#include <QApplication>
int main(int argc, char *argv[])
{
QApplication a(argc, argv);MainWindow w;
w.show();
return a.exec();
}
```

The first two lines are used to include our current `mainwindow.h` header and QApplication header files. The `QApplication` class is the main class responsible for controlling the application's control flow, settings, and so on.

Finally, the `exec()` function of the `QApplication` class is called so that the application is entered into the main loop, and stays on until the window is closed.

To understand how the event loop really works, try removing the last line and see what happens.

### Meta-Object Compiler (moc)

Before your Qt code is actually passed on to the real C++ compiler, the `moc` tool processes your class headers to generate the code required for enabling the Qt specific capabilities. You can find these generated source files in the Build folder. Their name starts with `moc_`.

What is worth mentioning here is that `moc` searches for all header files with Qt class definitions that contain the `Q_OBJECT` macro. This macro must always be included in Qt classes that want support for signals, slots, and other Qt supported features.

Here's what we had in our `mainwindow.h` file:

```
...
class MainWindow : public QMainWindow
{
    Q_OBJECT
public:
    explicit MainWindow(QWidget *parent = 0);
    ~MainWindow();
...
```

### User Interface Compiler (uic)

Whenever a Qt application with a user interface is built, a Qt internal tool called `uic` is executed to process and convert the `*.ui` files into classes and source code usable in C++ code.

In our case, `mainwindow.h` is converted to the `ui_mainwindow.h` file, which again, you can find in the `Build` folder.

If you take a look at the contents of the `ui_mainwindow.h` file, you'll notice a class called `Ui_MainWindow` with two functions: `setupUi` and `retranslateUi`.

## Design patterns

| Design pattern | Description | Example cases |
| --- | --- | --- |
| Abstract Factory | This can be used to create so-called factory classes that are capable of creating objects and control the creation of new objects in every possible way, such as preventing an object having more than a defined number instance. | In this chapter, we will learn how to use this design pattern to write plugin-based Qt applications. The create() function in the DescriptorMatcher abstract class is an example of this design pattern in OpenCV. |
| Command | Using this design pattern, actions can be represented with objects. This allows capabilities such as organizing the order of actions, logging them, reverting them, and so on. | **QAction**: This class allows creating specificactions and assigning them to widgets. For example, a QAction class can be used to create an Open File action with an icon and text, and then it can be assigned to the main menu item and a keyboard shortcut (like Ctrl + O) and so on. |
| Composite | This is used to create objects that consist of child objects. This is especially useful when making complex objects that can consist of many simpler objects. | **QObject**: This is the base of all Qt classes. **QWidget**: This is the base of all Qt widgets. Any Qt class with a tree-like design architecture is an example of the Composite pattern. |
| Facade (or Façade) | This can be used to encapsulate lower-level capabilities of an operating system (or any system for that matter) by providing a simpler interface. Wrapper and Adaptor design patterns are considered to be quite similar in definition. | **QFile**: These can be used to read/write files. Basically, all Qt classes that are wrappers around low-level APIs of operating systems are examples of the Façade design pattern. |
| Flyweight (or Bridge or Private-Implementation) | The goal of this design pattern is to avoid data copying and use shared data between related objects (unless otherwise is needed). | **QString**: This can be used to store and manipulate Unicode strings. In fact, many Qt classes enjoy these design patterns that help to pass a pointer to a shared data space whenever a copy of an object is needed, which consequently leads to faster object copying and less memory space usage. Of course, with a more complex code. |
| Memento | This can be used to save and (later on) load the state of objects.| This design pattern would be the equivalent of writing a class that is capable of storing all properties of a Qt object and restoring them to create a new one. |
| MetaObject (or Reflection) | In this design pattern, a so-called metaobject is used to describe the details of the object for a more robust access to that object. | **QMetaObject**: This simply contains meta-information about Qt classes. Covering the details of Qt's meta-object system is out of the scope of this book, but simply put, each Qt program is first compiled with the Qt MetaObject compiler (MOC) to generate the required meta objects and then compiled by the actual C++ compiler. |
| Monostate | This allows multiple instances of the same class to behave the same way. (Usually, by accessing the same data or executing the same functions.) | **QSettings**: This is used to provide application settings save/load. We already used the QSettings class in Chapter2, Creating Our First Qt and OpenCV Project, to load and save with two different instances of the same class. |
| MVC (Model-view-controller) | This is a widely-used design pattern, and it is used to separate the implementation of the application or data storage mechanism (Model) from the user interface or data representation (view) and the data manipulation(controller). | **QTreeView**: This is a tree-like implementation of model-view. **QFileSystemModel**: This is used to get a data model based on the contents of the local file system. A combination of `QFileSystemModel` (or any other `QAbstractItemModel`, for that matter) with `QTreeView` (or any other `QAbstractItemView`) can result in an MVC design pattern implementation. |
| Observer (or Publish/Subscribe) | This design pattern is used to make objects that can listen (or observe) to changes in other objects and respond accordingly. | **QEvent**: This is the base of all Qt's event classes. Think of QEvent (and all of its numerous subclasses) as a low-level implementation of the observer design pattern. On the other hand, Qt supports signal and slot mechanism, which is a more convenient and high-level method of using the Observer design pattern. We already used QCloseEvent (a subclass of QEvent) in Chapter 2, Creating Our First Qt and OpenCV Project. |
| Serializer | This pattern is used when creating classes (or objects) that can be used to read or write other objects. | **QTextStream**: This can be used to read and write text into files or other IO devices. **QDataStream**: This can be used to read or write binary data from IO devices and files. |
| Singleton | This can be used to restrict a class to only a single instance. | **QApplication**: This can be used to handle a Qt widgets application in various ways. To be precise, the `instance()` function in QApplication (or the global qApp pointer) is an example of the Singleton design pattern. The `cv::theRNG()` function in OpenCV (used to get the default Random Number Generator (RNG)) is an example ofSingleton implementation. Note that the RNG class itself is not a Singleton. |

## Qt Resource System

Qt supports resource management using the `*.qrc` files (Resource Collection Files), which are simply XML files that include information about resource files that need to be included in our applications.
