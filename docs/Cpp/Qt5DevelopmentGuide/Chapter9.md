# 第9章 Qt Charts

## 9.1 Qt Charts概述

### 9.1.1　Qt Charts模块

要在项目中使用QtCharts模块，必须在项目的.pro文件中增加下面的一行语句：
```
Qt += charts
```

在需要使用QtCharts的类的头文件或源程序文件中，要使用如下的包含语句：
```cpp
#include <QtCharts>
using namespace QtCharts;
```
也可以使用宏定义：
```cpp
#include <QtCharts>  
Qt_CHARTS_USE_NAMESPACE
```

### 9.1.2　一个简单的QChart绘图程序

在主窗口类中定义一个createChart()函数，并在构造函数中调用此函数，即：
```cpp
MainWindow::MainWindow(QWidget *parent) : QMainWindow(parent), ui(new Ui::MainWindow)
{
   ui->setupUi(this);
   createChart();
}
```

createChart()函数用于创建图表，其代码如下：
```cpp
void MainWindow::createChart()
{ 
//创建图表
   QChartView *chartView=new QChartView(this); //创建 ChartView
   QChart *chart = new QChart(); //创建 Chart
   chart->setTitle("简单函数曲线");
   chartView->setChart(chart); //Chart添加到ChartView
   this->setCentralWidget(chartView);
//创建折线序列
   QLineSeries *series0 = new QLineSeries();
   QLineSeries *series1 = new QLineSeries();
   series0->setName("Sin曲线");
   series1->setName("Cos曲线");
   chart->addSeries(series0); //序列添加到图表
   chart->addSeries(series1);
//序列添加数值
   qreal   t=0,y1,y2,intv=0.1;
   int cnt=100;
   for(int i=0;i<cnt;i++)
   {
      y1=qSin(t);//+qrand();
      series0->append(t,y1);
      y2=qSin(t+20);
      series1->append(t,y2);
      t+=intv;
   }
//创建坐标轴
   QValueAxis *axisX = new QValueAxis; //X 轴
   axisX->setRange(0, 10); //设置坐标轴范围
   axisX->setTitleText("time(secs)"); //标题

   QValueAxis *axisY = new QValueAxis; //Y 轴
   axisY->setRange(-2, 2);
   axisY->setTitleText("value");

   chart->setAxisX(axisX, series0); //为序列设置坐标轴
   chart->setAxisY(axisY, series0); 
   chart->setAxisX(axisX, series1); //为序列设置坐标轴
   chart->setAxisY(axisY, series1); 
}
```

### 9.1.3　图表的主要组成部分

1. QChartView的功能

QChartView类定义的函数有以下几个：
- void setChart(QChart *chart)，设置一个QChart对象作为显示的图表。
- QChart * chart()，返回QChartView当前设置的QChart类对象。
- void setRubberBand(RubberBands &rubberBand)，设置选择框的类型，即鼠标在视图组件上拖动选择范围的方式，是一个QChartView::RubberBand枚举类型的组合，QChartView:: RubberBand枚举类型有以下几种取值：
  - QChartView::NoRubberBand——无选择框；
  - QChartView::VerticalRubberBand——垂向选择；
  - QChartView::HorizontalRubberBand——水平选择；
  - QChartView::RectangleRubberBand——矩形框选择。
- RubberBands rubberBand()，返回设置的选择框类型。

2. 序列

常见的序列类：柱状图QBarSeries、水平柱状图QHorizontalBarSeries、
百分比柱状图QPercentBarSeries、水平百分比柱状图QHorizontalPercentBarSeries、堆叠柱状图QStackedBarSeries、水平堆叠柱状图QHorizontalStackedBarSeries、火柴盒图QBoxPlotSeries、饼图QPieSeries、折线图QLineSeries、光滑曲线图QSplineSeries、散点图QScatterSeries、	
面积图QAreaSeries。

3. 坐标轴

| 坐标轴类 | 特点 | 用途 |
|---|---|---|
| QValueAxis | 数值坐标轴 | 作为数值型数据的坐标轴 |
| QCategoryAxis | 分组数值坐标轴 | 可以为数值范围设置文字标签 |
| QLogValueAxis | 对数数值坐标轴 | 作为数值型数据的对数坐标轴，可以设置对数的基 |
| QBarCategoryAxis | 类别坐标轴 | 用字符串作为坐标轴的刻度，用于图表的非数值坐标轴 |
| QDateTimeAxis | 日期时间坐标轴 | 作为日期时间数据的坐标轴 |

4. 图例

QLegend是封装了图例控制功能的类，可以为每个序列设置图例中的文字，可以控制图例显示在图表的上、下、左、右不同位置。
QLegendMarker可以为每个序列的图例生成一个类似于QCheckBox的组件，在图例上单击序列的标记，可以控制序列是否显示。

## 9.2 QChart绘制折线图

### 9.2.2 主窗口类定义和初始化

下面是主窗口类MainWindow的类定义（省略了Action和界面组件的槽函数定义）。在mainwindow.h文件中需要包含QtChart，并使用宏Qt_CHARTS_USE_NAMESPACE导入命名空间。
```cpp
#include <QtCharts>
Qt_CHARTS_USE_NAMESPACE
class MainWindow : public QMainWindow
{
   Q_OBJECT
private:
   QLineSeries *curSeries; //当前序列
   QValueAxis *curAxis; //当前坐标轴
   void   createChart(); //创建图表
   void   prepareData(); //更新数据
   void   updateFromChart(); //从图表更新到界面
public:
   explicit MainWindow(QWidget *parent = 0);
private:
   Ui::MainWindow *ui;
};
```

createChart()函数用于创建图表的各个基本部件，在构造函数里调用，prepareData()用于更新序列的数据，updateFromChart()用于读取图表的一些属性，并刷新界面显示。下面是主窗口构造函数，以及这3个函数的代码。
```cpp
MainWindow::MainWindow(QWidget *parent) : QMainWindow(parent), ui(new Ui::MainWindow)
{
   ui->setupUi(this);
   createChart();//创建图表
   prepareData();//生成数据
   updateFromChart(); //从图表获得属性值，刷新界面显示
}

void MainWindow::createChart()
{//创建图表的各个部件
   QChart *chart = new QChart();
   chart->setTitle("简单函数曲线");
   ui->chartView->setChart(chart);
   ui->chartView->setRenderHint(QPainter::Antialiasing);

   QLineSeries *series0 = new QLineSeries();
   QLineSeries *series1 = new QLineSeries();
   series0->setName("Sin曲线");
   series1->setName("Cos曲线");
   curSeries=series0; //当前序列
   
   QPen  pen;
   pen.setStyle(Qt::DotLine);
   pen.setWidth(2);
   pen.setColor(Qt::red);
   series0->setPen(pen); //折线序列的线条设置
   pen.setStyle(Qt::SolidLine);
   pen.setColor(Qt::blue);
   series1->setPen(pen);//折线序列的线条设置
   chart->addSeries(series0);
   chart->addSeries(series1);

   QValueAxis *axisX = new QValueAxis;
   curAxis=axisX; //当前坐标轴
   axisX->setRange(0, 10); //设置坐标轴范围
   axisX->setLabelFormat("%.1f"); //标签格式
   axisX->setTickCount(11); //主分隔个数
   axisX->setMinorTickCount(4);
   axisX->setTitleText("time(secs)"); //标题
   QValueAxis *axisY = new QValueAxis;
   axisY->setRange(-2, 2);
   axisY->setTitleText("value");
   axisY->setTickCount(5);
   axisY->setLabelFormat("%.2f"); //标签格式
   axisY->setMinorTickCount(4);
   
   chart->setAxisX(axisX, series0); //设置X坐标轴
   chart->setAxisX(axisX, series1); //设置X坐标轴
   chart->setAxisY(axisY, series0); //设置Y坐标轴
   chart->setAxisY(axisY, series1); //设置Y坐标轴
}

void MainWindow::prepareData()
{//为序列生成数据
   QLineSeries *series0=(QLineSeries *)ui->chartView->chart()->series().at(0);
   QLineSeries *series1=(QLineSeries *)ui->chartView->chart()->series().at(1);
   series0->clear(); //清除数据
   series1->clear();
   qsrand(QTime::currentTime().second());//随机数初始化
   qreal   t=0,y1,y2,intv=0.1;
   qreal   rd;
   int cnt=100;
   for(int i=0;iappend(t,y1);  //序列添加数据点
      rd=(qrand() % 10)-5; //随机数,-5~+5
      y2=qCos(t)+rd/50;
      series1->append(t,y2); //序列添加数据点
      t+=intv;
   }
}

void MainWindow::updateFromChart()
{ //从图表上获取数据更新界面显示
   QChart*  aChart=ui->chartView->chart();  //获取chart
   ui->editTitle->setText(aChart->title()); //图表标题
   QMargins   mg=aChart->margins(); //边距
   ui->spinMarginLeft->setValue(mg.left());
   ui->spinMarginRight->setValue(mg.right());
   ui->spinMarginTop->setValue(mg.top());
   ui->spinMarginBottom->setValue(mg.bottom());
}
```

### 9.2.3 画笔设置对话框QWDialogPen

QWDialogPen是一个可视化设计的对话框，其类定义如下：
```cpp
class QWDialogPen : public QDialog
{ //QPen属性设置对话框
   Q_OBJECT
private:
   QPen   m_pen; //成员变量
public:
   explicit QWDialogPen(QWidget *parent = 0);
   ~QWDialogPen();
   void   setPen(QPen pen); //设置QPen，用于对话框的界面显示
   QPen   getPen(); //获取对话框设置的QPen的属性
   static  QPen  getPen(QPen  iniPen, bool &ok);  //静态函数
private slots:
   void on_btnColor_clicked();
private:
   Ui::QWDialogPen *ui;
};
```

QWDialogPen类的静态函数getPen()以及相关函数的实现代码如下：
```cpp
QPen QWDialogPen::getPen(QPen iniPen,bool &ok)
{ //静态函数，获取QPen
   QWDialogPen *Dlg=new QWDialogPen; //创建一个对话框
   Dlg->setPen(iniPen); //设置初始化QPen
   QPen   pen;
   int ret=Dlg->exec(); //弹出对话框
   if (ret==QDialog::Accepted)
   {
      pen=Dlg->getPen(); //获取
      ok=true;   }
   else
   {
      pen=iniPen;
      ok=false;   }
   delete  Dlg; //删除对话框对象
   return  pen; //返回设置的QPen对象
}

void QWDialogPen::setPen(QPen pen)
{ //设置QPen，并刷新显示界面
   m_pen=pen;
   ui->spinWidth->setValue(pen.width()); //线宽
   int  i=static_cast<int>(pen.style());  //枚举类型转换为整型
   ui->comboPenStyle->setCurrentIndex(i);
   QColor  color=pen.color();
   ui->btnColor->setAutoFillBackground(true); //设置颜色按钮的背景色
   QString str=QString::asprintf("background-color: rgb(%d, %d, %d);",
                        color.red(),color.green(),color.blue());
   ui->btnColor->setStyleSheet(str);
}

QPen QWDialogPen::getPen()
{//获得设置的属性
   m_pen.setStyle(Qt::PenStyle(ui->comboPenStyle->currentIndex())); //线型
   m_pen.setWidth(ui->spinWidth->value()); //线宽
   QColor  color=ui->btnColor->palette().color(QPalette::Button);
   m_pen.setColor(color); //颜色
   return  m_pen;
}
```
