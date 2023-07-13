# 4.Mat and QImage

## All about the Mat class

### Constructors, properties, and methods

Create a 10x10 matrix, with each element a single channel 8-bit unsigned integer (or byte):

```cpp
Mat matrix(10, 10, CV_8UC(1));
```

Create the same matrix and initialize all of its elements with the value of 0:

```cpp
Mat matrix(10, 10, CV_8UC(1), Scalar(0);
```

The third parameter though, which is a very important one, mixes the type, bit count, and the number of channels into a single macro. Here is the pattern of the macro and values that can be used:

```cpp
CV_<bits><type>C(<channels>)
```

`<bits>` can be replaced by:

- 8: It is used for unsigned and signed integer numbers
- 16: It is used for unsigned and signed integer numbers
- 32: It is used for unsigned and signed integer and floating-point numbers
- 64: It is used for unsigned and signed floating-point numbers

`<type>` can be replaced by:

- U: It is used for unsigned integer
- S: It is used for signed integer
- F: It is used for signed floating-point number

Theoretically speaking, `<channels>` can be replaced by any value, but for general computer vision functions and algorithms, it won't be higher than four.

You can omit the opening and closing parentheses for the `<channels>` parameter if you use a channel count no greater than four. You can also omit `<channels>` and the preceding C altogether if the number of channels is just one.

Create a cube (three-dimensional array) with the side length of 10 and with two channel elements of type double (64-bit), and initialize all values with the value of 1.0. This is shown as follows:

```cpp
int sizes[] = {10, 10, 10};
Mat cube(3, sizes, CV_64FC(2), Scalar::all(1.0));
```

You can also use the create method of the Mat class to change the size and type of it later on. Here's an example:

```cpp
Mat matrix;
// ...
matrix.create(10, 10, CV_8UC(1));
```

You can create a Mat class that is part of another Mat class. This is called **region of interest (ROI)**.

Here's how you create an ROI Mat class containing a 50x50 pixel wide square starting in the position 25,25 (X,Y) in an image:

```cpp
Mat roi(image, Rect(25,25,50,50));
```

As seen in the following image, the top-left corner of the image is considered to be the origin of the coordinate system in an image. So, the position of the origin is (0,0).

The top-right corner of the image has the location value of (width is 1,0).

The right-bottom corner of the image will have the location value of (width-1, height-1)

![Constructors-properties-and-methods-1](https://github.com/iknowledges/BookImage/raw/main/ComputerVisionWithOpenCV3AndQt5/Constructors-properties-and-methods-1.png)

If for any reason you want to copy a Mat class into a new (and completely independent) Mat, then you need to use the `clone` function, as seen in this example:

```cpp
Mat imageCopy = image.clone();
```

Assuming that the Mat image contains the previous image (from the previous chapters), you can use the following example code to select the ROI seen in the image and make all pixels in the highlighted region have a black color:

```cpp
4: Mat roi(image, Rect(500, 138, 65, 65));
roi = Scalar(0);
```

You can also select one or more rows, or columns in a Mat, in a way quite similar to the way we did with ROI, except we need to use the `row`, `rowRange`, `column`, or `colRange` functions in a Mat class. Here's how:

```cpp
Mat r = image.row(0); // first row
Mat c = image.row(0); // first column
```

Here's another example of using the `rowRange` and `colRange` functions that can be used to select a range of rows and columns instead of only a single row.

```
Mat centralRows = image.rowRange(image.rows/2 - 10, image.rows/2 + 10);
Mat centralColumns = image.colRange(image.cols/2 - 10, image.cols/2 + 10);
centralRows = Scalar(0);
centralColumns = Scalar(0);
```

And here's the result, executed on our test image:

![Constructors-properties-and-methods-2](https://github.com/iknowledges/BookImage/raw/main/ComputerVisionWithOpenCV3AndQt5/Constructors-properties-and-methods-2.png)

When you extract an ROI using the methods mentioned previously, and store it in a new Mat class, you can use the `locateROI` function to get the size of the parent image and the top-left position of the ROI inside the parent image. Here's an example:

```cpp
Mat centralRows = image.rowRange(image.rows/2 - 10, image.rows/2 + 10);
Size parentSize;
Point offset;
centralRows.locateROI(parentSize, offset);
int parentWidth = parentSize.width;
int parentHeight = parentSize.height;
int x = offset.x;
int y = offset.y;
```

The following three example codes achieve the same goal using the access methods mentioned in the preceding codes, they all make the image darker by dividing every pixel value by 5. First, using the at function:

```cpp
for(int i=0; i<image.rows; i++)
{
    for(int j=0; j<image.cols; j++)
    {
        image.at<Vec3b>(i, j) /= 5;
    }
}
```

Next, using STL-like iterators with begin and end functions:

```cpp
MatIterator_<Vec3b> it_begin = image.begin<Vec3b>();
MatIterator_<Vec3b> it_end = image.end<Vec3b>();
for( ; it_begin != it_end; it_begin++)
{
    *it_begin /= 5;
}
```

And finally, using the forEach function, provided with a lambda:

```cpp
image.forEach<Vec3b>([](Vec3b &p, const int *)
{
    p /= 5;
});
```

Here is the resulting darker image that would be the same for all of the three preceding codes:

![Constructors-properties-and-methods-3](https://github.com/iknowledges/BookImage/raw/main/ComputerVisionWithOpenCV3AndQt5/Constructors-properties-and-methods-3.png)

It's also important to note that all standard arithmetic operations are also possible with the Mat class.

```cpp
Mat darkerImage = image / 5; // or image * 0.2
```

### The Mat_<_Tp> class

The Mat_<_Tp> class provides a better access
method (more readable, so to speak) than the at function of the Mat class. Here's a short example:

```cpp
Mat_<Vec3b> imageCopy(image); // image is a Mat class
imageCopy(10, 10) = Vec3b(0,0,0); // imageCopy can use ()
```

### The UMat class

It's always best to use the `UMat` class instead of `Mat` especially in CPU-intensive functions with an underlying OpenCL implementation.

Just note that in cases when an explicit conversion between a Mat and UMat is
required, each class provides a function that can be used to convert it to the other:

```cpp
Mat::getUMat
UMat::getMat
```

For both of these functions an access flag is required, which can be:

- ACCESS_READ
- ACCESS_WRITE
- ACCESS_RW
- ACCESS_FAST

## Reading images using OpenCV

The `imread` function can be used to read images from the disk. Here's an example:

```cpp
Mat image = imread("c:/dev/test.jpg", IMREAD_GRAYSCALE | IMREAD_IGNORE_ORIENTATION);
```

`imread` simply takes a C++ `std::string` class as the first parameter and an `ImreadModes` flag as the second parameter.

The second parameter means we want the image to be loaded as grayscale and we also want to ignore the orientation information stored in the EXIF data part of the image file.

OpenCV also supports reading multi-page image files. You need to use the `imreadmulti` function for this reason. Here's a simple example:

```cpp
std::vector<Mat> multiplePages;
bool success = imreadmulti("c:/dev/multi-page.tif", multiplePages, IMREAD_COLOR);
```

OpenCV also supports reading images from a memory buffer using the `imdecode` function.

## Writing images using OpenCV

The `imwrite` function in OpenCV can be used to write images into files on disk. It uses the extension of the filename to decide the format of the image. To customize the compression rate and similar settings in an `imwrite` function, you need to use `ImwriteFlags`, `ImwritePNGFlags`, and so on.

```cpp
std::vector<int> params;
params.push_back(IMWRITE_JPEG_QUALITY);
params.push_back(20);
params.push_back(IMWRITE_JPEG_PROGRESSIVE);
params.push_back(1); // 1 = true, 0 = false
imwrite("c:/dev/output.jpg", image, params);
```

OpenCV also supports writing images into a memory buffer using the `imencode` function.

## Reading and writing videos in OpenCV

OpenCV provides a single and extremely easy-to-use class called `VideoCapture` for reading videos (or image sequences) from files saved on disk, or from capture devices, cameras, or a network video stream.

```cpp
VideoCapture video;
video.open("c:/dev/test.avi");
if(video.isOpened())
{
    Mat frame;
    while(true)
    {
        if(video.read(frame))
        {
            // Process the frame ...
        }
        else
        {
            break;
        }
    }
}
video.release();
```

If you want to load an image sequence, you simply need to replace the filename with the file path pattern. For instance, `image_%02d.png` will read images with filenames like image_00.png, image_01.png, image_02.png, and so on.

As you'll notice if you give it a try, whenever your program enters the while loop it will keep the GUI frombeing updated and your application might even crash. When working with Qt, a quick fix for this is to make sure GUI (and other) threads are also processed by adding the following code inside the loop:

```cpp
qApp->processEvents();
```

The `VideoCapture` class provides two important
functions, namely `set` and `get`. These can be used to configure numerous parameters of the class. For a complete list of configurable parameters, you can refer to the `VideoCaptureProperties` enum.

Here's a simple example that reads the number of frames in the video:

```cpp
double frameCount = video.get(CAP_PROP_FRAME_COUNT);
```

Here's another example that sets the current position of the frame grabber in the video to frame number 100:

```cpp
video.set(CAP_PROP_POS_FRAMES, 100);
```

When writing videos with the `VideoWriter` class you need a few more parameters. Here's an example:

```cpp
VideoWriter video;
video.open("c:/dev/output.avi", CAP_ANY, CV_FOURCC('M','P', 'G', '4'), 30.0, Size(640, 480), true);
if(video.isOpened())
{
    while(framesRemain())
    {
        video.write(getFrame());
    }
}
video.release();
```

In this example, the `framesRemain` and `getFrame` functions are imaginary functions that check if there are remaining functions to be written, and also get the frame (Mat).

## Image and video handling in Qt

### The QImage class

We can create an empty `QImage` class with a given size and format, as seen in the following example:

```cpp
QImage image(320, 240, QImage::Format_RGB888);
```

We can also pass a `QSize` class instead of the values and write the following:

```cpp
QImage image(QSize(320, 240), QImage::Format_RGB888);
```

By default, OpenCV loads color images in the BGR format (not
RGB), so if we try to construct a `QImage` using that, we'll have wrong channel data in place. So, we first need to convert it to RGB. Here's an example:

```cpp
Mat mat = imread("c:/dev/test.jpg");
cvtColor(mat, mat, CV_BGR2RGB);
QImage image(mat.data,
             mat.cols,
             mat.rows,
             QImage::Format_RGB888);
```

The `cvtColor` function in this example is an OpenCV function that can be used to change the color space of a Mat class. If we omit that line, we'll get a `QImage` that has its blue and red channels swapped.

A correct version of the previous code (and the recommended way of converting a `Mat` to a `QImage`) can be created with the next QImage constructor that we're going to see. It also requires a `bytesPerLine` parameter, which is the `step` parameter we learned about in the `Mat` class. Here's an example:

```cpp
Mat mat = imread("c:/dev/test.jpg");
cvtColor(mat, mat, CV_BGR2RGB);
QImage image(mat.data,
             mat.cols,
             mat.rows,
             mat.step,
             QImage::Format_RGB888);
```

The advantage of using this constructor and the `bytesPerLine` parameter is that we can also convert image data which is continuously stored in memory.

The next constructor is also a method of reading `QImage` from files saved on disk. Here's an example:

```cpp
QImage image("c:/dev/test.jpg");
```

We can add a `convertToFormat` function that makes sure our `QImage` is a standard three-channel RGB image. Here's an example:

```cpp
QImage image("c:/dev/test.jpg");
image = image.convertToFormat(QImage::Format_RGB888);
Mat mat = Mat(image.height(),
              image.width(),
              CV_8UC(3),
              image.bits(),
              image.bytesPerLine());
```

`transformed` takes a `QMatrix` or `QTransform` class and returns the transformed image. Here's a simple example:

```cpp
QImage image("c:/dev/test.jpg");
QTransform trans;
trans.rotate(45);
image = image.transformed(trans);
```

### The QPixmap class

`QPixmap` can be used to load and save an image (just like QImage) but it doesn't provide the flexibility to manipulate image data, and we'll also use it only when we need to display any images after we're done with all our modifications, processing, and manipulation.

We are now going to write an application that displays images that are dragged and dropped inside it:

1. Start by creating a new Qt Widgets Application in Qt Creator and name it `ImageViewer`.
2. Then choose `mainwindow.ui` and, using the Designer, remove the menu bar, status bar, and toolbar, and drop a single label widget (QLabel) on the window. Click on an empty space on the window and press *Ctrl + G* to lay out everything (your only widget which is a label) as a
grid. This will make sure everything is always resized to fit the window.
3. Now change the `alignment/Horizontal` property of the `label` to AlignHCenter. Then change both of its `Horizontal` and `VerticalsizePolicy` properties to `Ignored`. Next, add the following include statements to your `mainwindow.h` file:

```cpp
#include <QPixmap>
#include <QDragEnterEvent>
#include <QDropEvent>
#include <QMimeData>
#include <QFileInfo>
#include <QMessageBox>
#include <QResizeEvent>
```

4. Now, add the following protected functions to the `MainWindow` class definition in `mainwindow.h` using the code editor:

```cpp
protected:
void dragEnterEvent(QDragEnterEvent *event);
void dropEvent(QDropEvent *event);
void resizeEvent(QResizeEvent *event);
```

5. Also, add a private QPixmap to your `mainwindow.h`:

```
QPixmap pixmap;
```

6. Now, switch to `mainwindow.cpp` and add the following into the `MainWindow` constructor function so that it's called right at the beginning of the program:

```cpp
setAcceptDrops(true);
```

7. Next, add the following function in the `mainwindow.cpp` file:

```cpp
void MainWindow::dragEnterEvent(QDragEnterEvent *event)
{
    QStringList acceptedFileTypes;
    acceptedFileTypes.append("jpg");
    acceptedFileTypes.append("png");
    acceptedFileTypes.append("bmp");
    if (event->mimeData()->hasUrls() && event->mimeData()->urls().count() == 1)
    {
        QFileInfo file(event->mimeData()->urls().at(0).toLocalFile());
        if(acceptedFileTypes.contains(file.suffix().toLower()))
        {
            event->acceptProposedAction();
        }
    }
}
```

8. Another function that should be added to `mainwindow.cpp` is the following:

```cpp
void MainWindow::dropEvent(QDropEvent *event)
{
    QFileInfo file(event->mimeData()->urls().at(0).toLocalFile());
    if(pixmap.load(file.absoluteFilePath()))
    {
        ui->label->setPixmap(pixmap.scaled(ui->label->size(), Qt::KeepAspectRatio, Qt::SmoothTransformation));
    }
    else
    {
        QMessageBox::critical(this,
        tr("Error"),
        tr("The image file cannot be read!"));
    }
}
```

9. Finally, add the following function to `mainwindow.cpp`, and we're ready to execute our application:

```cpp
void MainWindow::resizeEvent(QResizeEvent *event)
{
    Q_UNUSED(event);
    if(!pixmap.isNull())
    {
    ui->label->setPixmap(pixmap.scaled(ui->label->width()-5,ui->label->height()-5, Qt::KeepAspectRatio, Qt::SmoothTransformation));
    }
}
```

By adding a `dragEnterEvent` function to `MainWindow` we were able to check if the dragged object is a file, and especially if it's a single file. Then we checked for the image type to make sure it's supported.

In the `dropEvent` function, we simply loaded the `QPixmap` with the image file that is dragged and dropped into the window of our application. Then we set the pixmap property of the `QLabel` class to our pixmap.

Finally, in the `resizeEvent` function we made sure that no matter the size of the window, our image is always scaled to fit the window with a correct aspect ratio.

We can write something like the following to load an image using OpenCV, process it using some computer vision algorithms, then convert it to a `QImage` and consequently to a `QPixmap`, and finally display the result on a `QLabel` as seen in this example code:

```cpp
cv::Mat mat = cv::imread("c:/dev/test.jpg");
QImage image(mat.data,
             mat.cols,
             mat.rows,
             mat.step,
             QImage::Format_RGB888);
ui->label->setPixmap(QPixmap::fromImage(image.rgbSwapped()));
```

### The QPainter class

We are going to create a new Qt widget that
simply shows a blinking circle:

1. Start by creating a Qt Widgets Application called `Painter_Test`.
2. Then select File/New File or Project from the main menu.
3. In the New File or Project window, select C++ and C++ Class then press Choose.
4. In the window that appears, make sure Class name is set to `QBlinkingWidget` and Base class is selected as QWidget. Make sure the Include QWidget checkbox is checked and leave the rest of the options.
5. Now press Next and then Finish. This will create and add a new class with a header and a source file to your project.
6. Now you need to override the `paintEvent` method of the `QBlinkingWidget` and do some drawing with `QPainter`. So, start by adding the following include statements to the `qblinkingwidget.h` file:

```cpp
#include <QPaintEvent>
#include <QPainter>
#include <QTimer>
```

7. Now, add the following protected member to the `QBlinkingWidget` class (add it after the existing public members for instance):

```cpp
protected:
    void paintEvent(QPaintEvent *event);
```

8. You also need to add a private slot to this class. So, add the following after the previous protected `paintEvent` function:

```cpp
private slots:
    void onBlink();
```

9. There's one last thing to add to the `qblinkingwidget.h` file, add the following private members we are going to use in our widget:

```cpp
private:
    QTimer blinkTimer;
    bool blink;
```

10. Now, switch to `qblinkingwidget.cpp` and add the following code inside the constructor function that is automatically created:

```cpp
blink = false;
connect(&blinkTimer,
        SIGNAL(timeout()),
        this,
        SLOT(onBlink()));
blinkTimer.start(500);
```

11. Next, add the following two methods to `qblinkingwidget.cpp`:

```cpp
void QBlinkingWidget::paintEvent(QPaintEvent *event)
{
Q_UNUSED(event);
QPainter painter(this);
if(blink)
    painter.fillRect(this->rect(), QBrush(Qt::red));
else
    painter.fillRect(this->rect(), QBrush(Qt::white));
}

void QBlinkingWidget::onBlink()
{
    blink = !blink;
    this->update();
}
```

12. Now, switch to the Design mode by opening `mainwindow.ui`, and then add a widget to your `MainWindow` class. By Widget, we mean exactly Widget, which is an empty one, as you'll notice when you add it to your MainWindow.
13. Now, right click on the added empty widget, which is a `QWidget` class, and choose Promote to from the pop-up menu.
14. In the new window that will be opened, called the Promoted Widgets window, set Promoted class name to `QBlinkingWidget` and press the Add button.
15. Finally, press Promote. Your application and custom widget are ready torun. As soon as your application starts you will see it blinking every 500 milliseconds (half a second).

In the preceding example, we used the `fillRect` function of QPainter to simply fill it with red and white colors every second, depending on the blink variable status.

In case we want to draw on a QImage, we just need to make sure we construct the QPainter by passing the QImage to it or using the begin function. Here's an example:

```cpp
QImage image(320, 240, QImage::Format_RGB888);
QPainter painter;
painter.begin(&image);
painter.fillRect(image.rect(), Qt::white);
painter.drawLine(0, 0, this->width()-1, this->height()-1);
painter.end();
```