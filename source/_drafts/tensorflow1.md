

Tensorflow已经用了一些和时间并且跑过一些项目了。但是当时用的比较急匆匆，所以对于一些比较基础的内容并没有太深入的了解，导致现在出了问题，如果stack Overflow上没有，只能仰天长叹，重启IDE和系统，祈求上天让我发出程序员终极问题之二：“这是怎么好的？？”（终极问题之一：“这程序哪里有错？？？”）

逆练九阴真经不可取。于是下定决心，最近把tensorflow再过一遍。当初选用deep learning 框架的时候也是纠结了一番，时间有限，比较主流的有caffe/tensorflow/pytorch/torch，评论讲caffe在逐渐被淘汰且灵活度较低，义无反顾入坑tf（虽然caffe也用过）。时过境迁，caffe的生命力在逐渐下降，甚至连tensorflow也有些过气，听说pytorch正异军突起？

闲话少说，书归正传（这闲话就不少了），咱们打板就唱。

## 计算模型、数据模型、运行模型

#####计算模型——计算图

所谓Tensorflow,即为Tensor+flow，tensor指数据模型张量，flow指计算模型“流”。计算图就是tensorflow中用来表示数据之间的计算关系，记录数据“流”向的结构。

计算图中使用结点表示运算形式，结点之间的箭头连线描述了计算之间的依赖关系。

Tensorflow 在使用中需要首先定义计算图来明确各种变量之间的计算关系，然后才是执行计算。

可以通过定义自定义计算图并命名来确定变量的作用范围，如果没有特意指定计算图，将使用当前默认的计算图进行运算。


#####数据模型——张量

Tensorflow中，张量是一种特殊的数据结构，可以简单理解为向量，但并不完全等价。张量中保存的并不是数组数字，而是对运算结果的引用，保存的是如何得到这些结果的过程。
如果要获得计算结果，可以使用`tf.Session().run(result)`得到计算结果。

张量中主要保存了三个属性：“名字(name)”、“维度(shape)”、“类型(type)”。


#####运行模型——会话
会话(Session)的意义就是执行上面定义好的张量(Tensor)和计算图(graph)进行运算。
举个栗子，计算图是计划书，张量是完成计划所需要的物资，会话就是计划的执行者。会话拥有并管理Tensorflow程序运行时的所有资源。

使用会话的两种模式：
```
sess = tf.Session()
sess.run(...)
sess.close()
```
```
with tf.Session() as sess:
	sess.run(...)
```
第一种方式需要手动close session,如果因为异常退出或者忘记close 将会导致资源泄露。第二种当上下文管理器退出的时候会自动释放所有资源。推荐使用第二种方式。

当默认的会话被制定之后可以通过`tf.Tensor.eval`来计算一个张量的取值。以下代码展示了通过设定默认会话计算张量的取值。
```
sess = tf.Session()
with sess.as_default():
	print(result.eval())
```

等价于：
```
sess = tf.Session()
print(sess.run(result))
print(result.eval(session = sess))
```
下面给出通过ConfigProto配置会话参数的方式：
```
config = tf.ConfigProto(allow_soft_placement = True,
log_device_placement = True)
sess = tf.Session(config = config)
