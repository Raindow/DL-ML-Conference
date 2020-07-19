TensorFlow与keras，pytorch有着一些不同的地方
例如,在使用TensorFlow读取图片时，我们自定义了函数deal
img1,img2=deal(root)
此时得到的结果不会是带有数据的ndarray而是tensor
我们需要运行
with tf.Session() as sess:
    img1,img2=sess.run([img1,img2])
也就是说在没有运行run时，img1,img2=deal(root)的意义为定义结构
sess.run()这个函数为根据关系计算对应数据的函数。