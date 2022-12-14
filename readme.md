#### 运行环境：

Vscode + jupyter notebook + python3.10.4 + macOS Monterey 12.4

#### 输入输出结果：

输入图片为一张1920*1200的png格式的彩色图像。

![test](readme.assets/test.png)

##### 采用自己编写的高斯滤波输出以下为各阶段的结果：

###### 灰度图像：

![image-20220910221629693](readme.assets/image-20220910221629693.png)

###### 给灰度图像添加高斯噪声：

![image-20220910221714666](readme.assets/image-20220910221714666.png)

###### 高斯核大小为3*3时的结果：

![image-20220910221949837](readme.assets/image-20220910221949837.png)

###### 高斯核大小为5*5时的结果：

![image-20220910221825958](readme.assets/image-20220910221825958.png)

###### 高斯核大小为7*7时的结果：

![image-20220910222038167](readme.assets/image-20220910222038167.png)

###### 高斯核大小为15*15时的结果：

![image-20220910222342552](readme.assets/image-20220910222342552.png)



##### 采用opencv的高斯滤波输出以下为各阶段的结果：

###### 高斯核大小为3*3时的结果：

![image-20220910222639210](readme.assets/image-20220910222639210.png)

###### 高斯核大小为5*5时的结果：

![image-20220910222730420](readme.assets/image-20220910222730420.png)

###### 高斯核大小为7*7时的结果：

![image-20220910222935203](readme.assets/image-20220910222935203.png)

###### 高斯核大小为15*15时的结果：

![image-20220910223140123](readme.assets/image-20220910223140123.png)



#### 当对彩色图像实施高斯滤波的时候需将原图像分为R,G,B三个分量，分别实施高斯滤波后再对其进行融合，分解时可以利用opencv的split()函数，聚合时可以利用opencv的merge()函数。但此种方法的速度较慢，可用于小型项目，另一种方法是使用数组直接提取分量。

##### 对原图分解后实施添加噪声结果如下：

![image-20220910224221544](readme.assets/image-20220910224221544.png)

##### 使用自己编写的函数的结果如下：

###### 高斯核大小为3*3时的结果：

![image-20220910223826426](readme.assets/image-20220910223826426.png)

###### 高斯核大小为5*5时的结果：

![image-20220910224459161](readme.assets/image-20220910224459161.png)

###### 高斯核大小为7*7时的结果：

![image-20220910224619430](readme.assets/image-20220910224619430.png)

###### 高斯核大小为15*15时的结果：

![image-20220910224904651](readme.assets/image-20220910224904651.png)



##### 使用库函数时的结果如下：

###### 高斯核大小为3*3时：

![image-20220910225634151](readme.assets/image-20220910225634151.png)

###### 高斯核大小为7*7时：

![image-20220910225529413](readme.assets/image-20220910225529413.png)

###### 高斯核大小为15*15时：

![image-20220910225749141](readme.assets/image-20220910225749141.png)

#### 结论：

1. 从速度上说，自己编写的高斯滤波函数速度明显慢于库函数，在相同核大小的情况下，自己编写的函数运行时间大约是库函数的1.5倍左右。在灰度图像的处理中，核大小偏小的情况下，使用自编写函数耗时大概9-11秒左右，库函数耗费时间大概为6-8秒。在彩色图像的处理中，核大小偏小的情况下，使用自编写函数耗时大概32-36秒，而使用库函数耗时大概14-18秒。对速度而言，库函数有明显优势。
2. 从核大小上说，处理灰度图片时，当核大小偏小，如（3,3）、（5,5）、（7,7）的情况下滤波效果随核大小增加而变好，而当核大小达到一定水平后则效果开始变差，如（15,15）。处理彩色图片时，也是同理。但彩色图像处理中还会存在颜色失真的情况，随着核大小增加，会逐步好转，核越小这种问题影响越大。
3. 从两种函数的质量上来说，自编写函数随着核增大对图像的滤波效果的下降慢于库函数。简而言之，库函数的核随着增大到一定程度的同时滤波效果会剧烈下降。