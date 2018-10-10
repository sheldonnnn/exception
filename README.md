广东工业制造算法赛代码及数据格式解释
==================================
文件格式问题
-------------
首先是文件名处理，因为带有中文程序总是报错，就通过批处理把所有图片的中文给删掉了！比如’打磨印20180907101503对照样本.jpg‘就变成了’20180907101503.jpg‘。所有图片都做了这种处理，其次文件夹名也都改成了原中文名字的英文，比如’图层开裂‘变为’tuceng‘，’不导电‘变为了’budaodian‘，然后将无瑕疵文件夹移动了跟瑕疵文件在一起，就是跟各个瑕疵文件夹并列，这个文件夹包含12个文件分别是’wuxiaci’，‘budaodian’，‘cahua’，...，‘qita‘。  
然后为了做数据增强在此文件夹中创建了12个空文件夹，分别是上面文件名后面加了个1’wuxiaci1：‘，’budaodian1‘，’cahua1‘，...，’qita1‘.将上面带有图片的原文件移动到相应后缀带1的文件中，比如wuxiaci1文件下现在有一个wuxiaci文件，budaodian1中有budaodian文件（原数据图片都在不带1的文件中）。随后做数据增强（旋转，反转，白化），数据增强的图片保存到了不带1的文件中比如’budaodian1/budaodian‘中，这时所有要用的数据也都在这个文件中了，随后删除了一些形状扭曲和模糊面积大的图片。  
具体文件格式data——12个文件（文件名为：‘zhengchang1’，‘budaodian1’，...,‘qita1’）  
zhengchang1——zhengchang——训练所用图片；budaodian1——budaodian——训练所用图片........  
文件根目录是main.py中的or_path(data).
## 程序说明
----------------
### 框架tensorflow
### content
1.main.py:主要运行模块，train()训练:  
2.xception.py:xception框架：  
3.preprocess.py:包含用keras数据增强和获取数据及label。  
### 训练思路
对数据量较少的图片类别增强，主要进行翻转，旋转和白化，然后删除一些形状变形的图片，用xception模型进行训练。  
batch——size=16；初始学习率0.01，每个epoch乘0.9，如果误差不下降lr除以5，优化方法SGD。
## 注意3
-----------------
未使用开源数据集，使用开源框架exception  
开源框架论文引用地址：Xception: Deep Learning with Depthwise Separable Convolutions.https://arxiv.org/abs/1610.02357  
作用是主要训练的baseline，在此基础上修改的模型及参数。未使用开源训练数据。
