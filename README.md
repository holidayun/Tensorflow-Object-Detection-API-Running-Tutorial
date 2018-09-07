***执行过程中出现任何问题，可下方评论，看到会回复***
准备：
1.python3.6
2.tensorflow

环境搭建：

1.下载模型

从github上下载模型，下载地址：https://github.com/tensorflow/models
![这里写图片描述](https://github.com/holidayun/Tensorflow-Object-Detection-API-Running-Tutorial/blob/master/readme/clone.png)


2.Protobuf 安装：

从https://github.com/google/protobuf/releases下载win版的工具，如下图：
![这里写图片描述](https://github.com/holidayun/Tensorflow-Object-Detection-API-Running-Tutorial/blob/master/readme/protoc.png)



下载完成之后解压，例如我的路径为：D:\Tensorflow\ObjectDetection, 在D:\Tensorflow\ObjectDetection\protoc-3.5.1-win32\bin 目录下可看到可执行文件protoc.exe.   为了方便使用，将D:\Tensorflow\ObjectDetection\protoc-3.5.1-win32\bin设置为环境变量，输入命令：protoc，不报错，表示安装成功

**注：若使用3.6.1版本的protoc，在运行的时候会出现：___init__() got an unexpected keyword argument 'serialized_options'的错误**





3.protoc 编译：

用protoc可执行文件编译目录object_detection/protos下的proto文件，生成Python文件。
git终端移动到 models\research目录下执行命令：
```
protoc object_detection/protos/*.proto --python_out=.
```

不报错，即编译成功，可查看protos下的.proto文件，都生成了一份.py文件。

4.object-detection环境变量设置：

window下，环境变量需通过对应目录下的setup.py 进行设置。
终端移动到models\research目录下，依次执行

```
python setup.py build
python setup.py install
```

5.测试

终端移动到models\research目录下，执行：

```
python object_detection\builders\model_builder_test.py
```

需要等待几秒钟，若出现 "OK",则表示环境准备成功。
若出现： **" no moduel named 'nets' "**

终端移动到models\research\slim 目录下，再重新执行一次

```
python setup.py build
python setup.py install
```

若出现  **“build已经存在的问题 ”**， 将该文件夹下的build文件删掉，重新执行上面的命令即可。

再次执行：

```
python object_detection\builders\model_builder_test.py
```

**6.运行tensorflow-object-detection-api.**

有两种形式可以执行，先介绍官方给的示例。
官方示例：

终端移动到models\research目录下
终端输入：jupyter notebook
浏览器会默认打开一个 http://localhost:8888/tree的网址
打开文件**object_detection_tutorial.ipynb**， 运行demo
![这里写图片描述](https://github.com/holidayun/Tensorflow-Object-Detection-API-Running-Tutorial/blob/master/readme/run.png)


在Cell中点击 Run All
![这里写图片描述](https://github.com/holidayun/Tensorflow-Object-Detection-API-Running-Tutorial/blob/master/readme/runall.png)


耐心等待一小会儿， 出现下图结果表示环境安装成功。
![这里写图片描述](https://github.com/holidayun/Tensorflow-Object-Detection-API-Running-Tutorial/blob/master/readme/result.png)


若想修改识别的图片，可修改以下位置的代码，根据自己的需求进行修改。




为了便于后期使用，我在官方示例的基础上，做了一点点的修改，参考test.py
1.可在编辑器中直接运行该程序。
2.文件夹中(images)的图片不用指定名称与数量，有多少图片，就识别多少图片。
注：将images文件夹中非图片的文件删掉
3.识别完成的图片自动保存至指定文件夹(test_images_detection)中。

在models\research\object_detection 文件夹下，新建一个py文件，暂时命名为test.py.
然后执行 test.py即可。
