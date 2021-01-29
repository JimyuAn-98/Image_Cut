# Image_Cut
Crop high-resolution images into low-resolution images and preserve the BBOX information
将高分辨率图片切割为低分辨率图片，并且保留对应的bbox信息


这个工具是我在学习yolov4时制作的

## 举例说明：

输入为1920*1080的图像，模型要求的输入大小为416

1920 / 416 = 4.62 取5

1080 / 416 = 2.60 取3

那么工具将裁切出5 * 3 = 15个图像，并且会对bbox进行处理

假设有原图中的bbox_1，裁切后的图img_1，bbox_1在img_1中的部分nbbox

如果nbbox的面积小于bbox_1的面积的20%，那么这个bbox将被舍弃

如果大于20%，则会根据nbbox在img_1中的位置，重新计算坐标，并保存到annotation中

## 使用说明
