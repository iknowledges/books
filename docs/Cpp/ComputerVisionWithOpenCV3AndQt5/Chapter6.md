# 6.Image Processing in OpenCV

## Image filtering

It's important to note that all of the functions discussed in this section take a `Mat` image as an input and produce a `Mat` image of the same size and the same number of channels.

1. Open the `plugin.ui` file and make sure its user interface includes the following widgets. Also, pay attention to the objectName values of the widgets. Notice that the layout of the entire PluginGui file is set to a grid layout.
2. Set the `size Policy/Horizontal Policy` property of `borderTypeLabel` to Fixed. This will ensure that the label occupies a fixed horizontal space according to its width.
3. Add a method for the `currentIndexChanged(int)` signal of the `borderTypeComboBox` widget by right-clicking on it, selecting Go to slot..., choosing the mentioned signal, and clicking on the OK button. Then, write the following line of code in the newly created function (or slot, to be precise) for this signal:

```cpp
emit updateNeeded();
```

4. Now, in the `copymakeborder_plugin.cpp` file, add the following piece of code to its `setupUi` function. The contents of the `setupUi` function should look like this:

```cpp
ui = new Ui::PluginGui;
ui->setupUi(parent);
QStringList items;
items.append("BORDER_CONSTANT");
items.append("BORDER_REPLICATE");
items.append("BORDER_REFLECT");
items.append("BORDER_WRAP");items.append("BORDER_REFLECT_101");
ui->borderTypeComboBox->addItems(items);
connect(ui->borderTypeComboBox, SIGNAL(currentIndexChanged(int)), this, SLOT(on_borderTypeComboBox_currentIndexChanged(int)));
```

5. Finally, update the `processImage` function in the plugin, as seen here:

```cpp
int top, bot, left, right;
top = bot = inputImage.rows/2;
left = right = inputImage.cols/2;
cv::copyMakeBorder(inputImage,
    outputImage,
    top,
    bot,
    left,
    right,
    ui->borderTypeComboBox->currentIndex());
```

Here, we will call the `copyMakeBorder` function that is similarly called inside functions that need to deal with an assumption about the non-existing pixels outside of an image. We will simply assume that the added border to the top and bottom of the image is half the image height, and the added border to the left and right of the image is half the image width.

### Filtering functions in OpenCV