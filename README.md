# Image_Cut

Readme in [English](https://github.com/JimyuAn-98/Image_Cut/blob/master/README_EN.md)

将高分辨率图片切割为低分辨率图片，并且保留对应的bbox信息

这个工具是我在学习yolov4时制作的

这是yolov4项目的链接：[tensorflow-yolov4-tflite](https://github.com/hunglc007/tensorflow-yolov4-tflite)

## 举例说明：

输入为1920*1080的图像，模型要求的输入大小为416

1920 / 416 = 4.62 取5

1080 / 416 = 2.60 取3

那么工具将裁切出5 * 3 = 15个图像，并且会对bbox进行处理

假设有原图中的bbox_1，裁切后的图img_1，bbox_1在img_1中的部分nbbox

如果nbbox的面积小于bbox_1的面积的20%，那么这个bbox将被舍弃

如果大于20%，则会根据nbbox在img_1中的位置，重新计算坐标，并保存到annotation中

## 使用说明

### 前提

因为是在学习yolov4的过程中制作的，所以annotation的格式是根据yolov4来写的

trans coco中的是yolo项目中的用于转换coco格式数据的工具

trans voc中的是yolo项目中的用于转换voc格式数据的工具

我的工具是在进行了格式转换之后，通过读取上面的工具得到的txt文档得到一些关键信息（比如图片路径，bbox坐标），再进行切割

>Ask：为什么需要进行格式转换？
>Ans：因为我懒 o_o

### 需要的包

opencv-python numpy absl

### 使用

在控制台中即可使用

输入`python image_cut.py --help`即可查看帮助

```
image_cut.py:
  --fap: path to the former annotation txt file
    (default: './data/dataset/tiny_train.txt')
  --oap: path to save processed annotation file
    (default: './data/dataset/tiny_cut_train.txt')
  --oip: path to save processed images
    (default: './data/tiny_set/train/cut_images')
  --size: the input size of your model
    (default: '416')

Try --helpfull to get a list of all flags.
```

举例：

```
python image_cut.py --fap ./data/dataset/tiny_train.txt --oap ./data/dataset/tiny_cut_train.txt --oip ./data/tiny_set/train/labeled_cut_images --size 416
```

## 后续工作

使之免去数据格式转换工作，可以直接读取coco或voc的annotation
