# Plant-Seedlings-Classification
There is a machine learning method to complete the Kaggle Competition Plant Seedlings Classification

## Introduction

&emsp;&emsp;使用机器学习方法完成 Kaggle 竞赛 Plant Seedlings Classification

&emsp;&emsp;竞赛网址：[Plant Seedlings Classification](https://www.kaggle.com/c/plant-seedlings-classification) from Kaggle  
&emsp;&emsp;代码讲解：[Kaggle图像识别竞赛 Plant Seedlings Classification（植物幼苗分类）具体实现](https://blog.csdn.net/Friedrichor/article/details/122248139)  
&emsp;&emsp;预备知识/参考资料：[Plant Seedlings Classification(机器学习实现)预备知识&函数](https://blog.csdn.net/Friedrichor/article/details/121737819)  

&emsp;&emsp;这个代码是很久之前的了，有些地方可能有点乱，还有一些代码注释掉了，有些地方如果你是第一次运行的话需要把 “#” 去掉跑一下，自己注意一下。

## Related Issues

### bow_init()相关问题
&emsp;&emsp;如果在调用bow_init()函数时有以下报错：
```
error: OpenCV(4.5.4) D:\a\opencv-python\opencv-python\opencv\modules\features2d\src\bagofwords.cpp:55: error: (-215:Assertion failed) !_descriptors.empty() in function 'cv::BOWTrainer::add'
```
&emsp;&emsp;可能是因为提取SIFT特征时，有些图片并没有提取到SIFT特征，也就是没有提取到关键点，这样的话最简单的方法就是在image_list 和 label_list 中都把没有SIFT特征的图片及对应标签给去掉。不过如果是按本文方法做的图像预处理的话是不会出现这种问题的，经过本文的预处理后每张图都能提取到 SIFT 特征。

### 测试相关问题
&emsp;&emsp;代码中只做了训练和验证，没做测试，如果做测试的话，需要注意 bow_extractor 要沿用训练集的，而不是在测试集上重新调用 bow_init()，并且测试集也不需要提取sift特征了  
&emsp;&emsp;因为 BOW（词带模型）肯定是要有统一的词典才有效，主要就是要他这个词典统一，如果用测试集再调用 bow_init()，词典就变了。  
&emsp;&emsp;也就是说，代码中训练时的  
```python
bow_extractor = bow_init(feature_sift_list)
all_feature_bow = bow_feature(bow_extractor, image_list)
```
&emsp;&emsp;在测试时，上面代码中第一行是不需要的，直接就是
```python
test_feature_bow = bow_feature(bow_extractor, image_test_list)  # bow_extractor 是上面代码中的, 也就是训练集的; 
                                                                # image_test_list 是测试集图像列表
```
&emsp;&emsp;按理来说，应该就没有问题了，不过没有测试过，不知道会不会有其他问题

### Other Problems
&emsp;&emsp;如有其他问题，可以在博客中与我私信交流，我的博客：[Friedrichor](https://blog.csdn.net/Friedrichor?type=blog)

