# face-recognition
pre-model face-recognition 
人脸识别是当下深度学习最成熟的的应用之一。在某些实验环境下，人脸识别的精度已经赶上甚至超过了人类。完整的人脸识别项目会包括两大部分：人脸检测与人脸识别。
整个项目的框架包括四个主要的部分：（1）利用opencv摄像头实时的读入视频帧；（2）使用mtcnn网络做人脸检测和对齐；（3）利用facenet网络计算人脸特征，也就是embedding；（4）训练knn算法进行具体的人脸识别。其中的mtcnn的人脸检测是很关键的一步，它检测定位的人脸准确与否直接影响到后面的特征计算与识别；facenet实际是一个对人脸进行embedding；knn的分类算法则应用于实时的人脸识别。

![image](https://github.com/fuxi5788/face-recognition/raw/master/images/face-recognition.png)

1.mtcnn由三个神经网络组成，分别是P-Net, R-Net, O-Net。在使用这些网络之前，首先要将原始图片缩放到不同尺寸，形成一个图像金字塔，接着会对每个尺寸的图片通过神经网络计算一遍。其目的在于兼顾图片中的不同大小的人脸，在统一的尺度下检测人脸。

![image](https://github.com/fuxi5788/face-recognition/raw/master/images/p-net.png)

P-Net的输入是一个12x12的3通道RGB图像，它的作用是要判断这个网络中是否有人脸，并且给出人脸框和关键点位置。

![image](https://github.com/fuxi5788/face-recognition/raw/master/images/r-net.png)

R-Net的结构与P-Net相似，输入为24x24的RGB图像，在最后的输出层前多加入了一个全连接层。

![image](https://github.com/fuxi5788/face-recognition/raw/master/images/o-net.png)

O-Net相比R-Net在结构上又多出一个中间层，输出结果一样。
2.facenet网络的输入有多种不同的大小，中间部分是一个深度卷积神经网络，设计了一种新的损失——triplet loss（三元组损失）。

![image](https://github.com/fuxi5788/face-recognition/raw/master/images/facenet.png)

训练这个三元组损失需要取训练集做成很多三元组，例如这是一个三元组（编号 1），有一个Anchor图片和 Positive图片，这两个（Anchor和Positive）是同一个人，还有一张另一个人的 Negative 图片。这是另一组（编号 2），其中 Anchor 和Positive图片是同一个人，但是 Anchor和Negative不是同一个人。
3.knn，即K最近邻(k-NearestNeighbor)分类算法，见名思意：找到最近的k个邻居（样本），在前k个样本中选择频率最高的类别作为预测类别。它是一种有监督的学习算法。算法步骤如下： 
  1）算距离：给定未知对象，计算它与训练集中的每个对象的距离； 
  2）找近邻：圈定距离最近的k个训练对象，作为未知对象的近邻； 
  3）做分类：在这k个近邻中出线次数最多的类别就是测试对象的预测类别。
使用5个人的人脸样本，每个人40张训练knn模型，从摄像头读取视频帧，下载knn模型做实时的识别，准确率在90%左右。
![image](https://github.com/fuxi5788/face-recognition/raw/master/images/log.png)
