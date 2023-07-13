# 第4章 虚拟机性能监控、故障处理工具

## 4.2 基础故障处理工具

### 4.2.1 jps：虚拟机进程状况工具

jps命令格式： jps [ options ] [ hostid ]
参数hostid为RMI注册表中注册的主机名。

主要选项：

| 选项 | 作用 |
|:----:|:----:|
| -q | 只输出LMVID，省略主类名称 |
| -m | 输出虚拟机启动时传递给main函数的参数 |
| -l  | 输出主类的全名称，如果执行的是JAR包，则输出JAR路径 |
| -v | 输出虚拟机启动时的JVM参数 |

### 4.2.2 jstat：虚拟机统计信息监视工具

jstat命令格式： jstat [ option vmid [interval[s|ms] [count]] ]
如果是本地虚拟机进程，VMID与LVMID是一致的；如果是远程虚拟机进程，那VMID的格式应当是： [protocol:][//]lvmid[@hostname[:port]/servername]
参数interval和count代表查询间隔和次数，如果省略这2个参数，说明只查询一次。

主要选项：

| 选项 | 作用 |
|:----:|:----:|
| -class | 监视类加载、卸载数量、总空间以及类加载所耗费时间 |
| -gc | 监视Java堆状况，包括Eden区、2个Survivor区、老年代、永久代等的容量，已用空间、垃圾收集时间合计等信息 |
| -gccapacity | 监视内容与-gc基本相同，但输出主要关注Java堆各个区域使用到的最大、最小空间 |
| -gcutil | 监视内容与-gc基本相同，但输出主要关注已使用空间占总空间的百分比 |
| -gccause | 与-gcutil功能相同，但会额外输出导致上一次垃圾收集产生的原因 |
| -gcnew | 监视新生代垃圾收集状况 |
| -gcnewcapacity | 监视内容与-gcnew基本相同，但输出主要关注使用到的最大、最小空间 |
| -gcold | 监视老年代垃圾收集状况 |
| -gcoldcapacity | 监视内容与-gcold基本相同，但输出主要关注使用到的最大、最小空间 |
| -gcpermcapacity | 输出永久代使用到的最大、最小空间 |
| -compiler | 输出即时编译器编译过的方法、耗时等信息 |
| -printcompilation | 输出已经被即时编译的方法 |

### 4.2.3 jinfo：Java配置信息工具

jinfo命令格式： jinfo [ option ] pid

使用jps命令的-v参数可以查看虚拟机启动时显式指定的参数列表，使用jinfo的-flag选项可以查询未被显式指定的参数的系统默认值。

jinfo可以使用-sysprops选项把虚拟机进程的System.getProperties()的内容打印出来。

jinfo可以使用-flag[+|-]name或者-flag name=value在运行期修改一部分运行期可写的虚拟机参数值。

### 4.2.4 jmap：Java内存映像工具

jmap命令格式： jmap [ option ] vmid

主要选项：

| 选项 | 作用 |
|:----:|:----:|
| -dump | 生成Java堆转储快照。格式为：-dump:[live,]format=b,file=<filename>,其中live子参数说明是否只dump出存活的对象 |
| -finalizeinfo | 显示在F-Queue中等待Finalizer线程执行finalize方法的对象。只在Linux/Solaris平台下有效 |
| -heap | 显示Java堆详细信息，如使用哪种回收器、参数配置、分代状况等。只在Linux/Solaris平台下有效 |
| -histo| 显示堆中对象统计信息，包括类、实例数量、合计容量 |
| -permstat | 以ClassLoader为统计口径显示永久代内存状态。只在Linux/Solaris平台下有效 |
| -F | 当虚拟机进程对-dump选项没有响应时，可使用这个选项强制生成dump快照。只在Linux/Solaris平台下有效 |
