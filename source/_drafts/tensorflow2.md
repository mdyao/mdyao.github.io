FC全连接层就是相邻两层之间的任意两个结点之间都有连接。

通过定义损失函数来刻画预测值于真实值的差距
```python
cross_entropy = -tf.resuce_mean(y_ * tf.log(tf.clip_by_value(y, 1e-10, 1.0)))
#定义学习率
learning_rate  = 0.001
train_step =\ tf.train.AdamOptimizer(learning_rate).minimize(cross_entry)
```

[TOC]

###变量：创建、初始化、保存和加载
储存变量
```python
saver = tf.train.Saver()
with tf.Session as sess:
	sess.run(int_op)
    save_path = saver.save(sess,"tmp/model.ckpt")
    print save_path
```
恢复变量
```python
saver = tf.train.Saver
with tf.Session as session:
	saver.restore(sess,"tmp/model.ckpt")
    print("MODEL RESTORED")
```
存储和保存部分变量
```python
saver = tf.train.Saver({"my_v2":v2})
# Use the saver objeect normally after that
...
```
###Tensorboard

```python
with tf.Session as sess:
    merged = tf.summary.marge_all()
    file_writer = tf.summary.Filewriter("/tmp/logs/",sess.graph)
    _,summary = sess.run([train_op,merged])
    file_writer.add_summary(summary, total_step)
```
启动tensorboard
```python
tensorboard --logdir=LOGPATH
```
地址：`localhost:6006`
###读取数据

-   供给数据(Feeding)： 在TensorFlow程序运行的每一步， 让Python代码来供给数据。
-  从文件读取数据： 在TensorFlow图的起始， 让一个输入管线从文件中读取数据。
-  预加载数据： 在TensorFlow图中定义常量或变量来保存所有数据(仅适用于数据量比较小的情况)。


###线程和队列 

![FIFOqueue](http://wiki.jikexueyuan.com/project/tensorflow-zh/images/IncremeterFifoQueue.gif)
Tensorflow 提供了`FIFOQueue`和`RandomShuffleQueue`两种队列。
同时提供`tf.Coordinator`和`tf.QueueRunner`两个类来完成多线程协同的功能。

- tf.Coordinator主要用于协同多个线程同时停止,提供以下函数
 - `should_stop()`:如果线程停止则返回True
 - `request_stop(<exception>)`:请求线程停止
 - `join(<list of thread>)`:等待被指定的线程终止


```python
import threading

num_thread = 20
coord = tf.train.Coordinator()
for i in range(num_thread):
    t = threading.Thread(target = TAGET_FUNCTION, args = (coord, ARGS))
    threads = []
    threads.appent(t)
    t.start()

#或者以下方式
threads = [threading.Thread(target=TARGET_FUNCTION), args=(coord, ARGS) for i in range(num_thread)]
for t in threads: t.start
```
但是以上步骤还不完整，还没有使用`request_stop`和`should_stop`，目前没搞明白python的多线程，todo.


https://blog.csdn.net/lenbow/article/details/52181159


