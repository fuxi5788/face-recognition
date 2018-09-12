# face-recognition
pre-model face-recognition 
人脸识别是当下深度学习最成熟的的应用之一。在某些实验环境下，人脸识别的精度已经赶上甚至超过了人类。完整的人脸识别项目会包括两大部分：人脸检测与人脸识别。
整个项目的框架包括四个主要的部分：（1）利用opencv摄像头实时的读入视频帧；（2）使用mtcnn网络做人脸检测和对齐；（3）利用facenet网络计算人脸特征，也就是embedding；（4）训练knn算法进行具体的人脸识别。其中的mtcnn的人脸检测是很关键的一步，它检测定位的人脸准确与否直接影响到后面的特征计算与识别；facenet实际是一个对人脸进行embedding；knn的分类算法则应用于实时的人脸识别。
1.mtcnn由三个神经网络组成，分别是P-Net, R-Net, O-Net。在使用这些网络之前，首先要将原始图片缩放到不同尺寸，形成一个图像金字塔，接着会对每个尺寸的图片通过神经网络计算一遍。其目的在于兼顾图片中的不同大小的人脸，在统一的尺度下检测人脸。
![image](https://github.com/fuxi5788/face-recognition/tree/master/images/face-recognition.png)

1.使用基于数据集CASIA-WebFace的Inception ResNet v1神经网络结构，训练好的模型作为预训练模型，再此基础上去掉顶层，训练knn_classifier.model

2.使用Inception ResNet v1神经网络结构预训练模型做静态人脸验证
