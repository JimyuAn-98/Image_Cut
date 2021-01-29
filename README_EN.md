# Image_Cut

Readme in [Chinese](https://github.com/JimyuAn-98/Image_Cut/blob/master/README.md)

Cut the high-resolution image into low-resolution image, and keep the corresponding BBOX information

This tool was created while I was studying Yolov4

Here’s the link to the Yolov4 project: [tensorflow-yolov4-tflite](https://github.com/hunglc007/tensorflow-yolov4-tflite)

## Example

The input image’s resolution is 1920*1080. The model required input size is 416*416

1920 / 416 = 4.62 as 5

1080 / 416 = 2.60 as 3

Then the tool will crop out 5 * 3 = 15 images and process the BBOX

Assume that you have the `bbox_1` from the original image, the cropped image `img_1`, and the `nbbox` which is the part of the `bbox_1` in `img_1`

If the `nbbox` area is less than 20% of the `bbox_1` area, then thebbox will be discarded

If it is larger than 20% , the coordinates will be recalculated based on the `nbbox`’s position in `img_1` and saved to `annotation`

## How to Use

### Premis

Since it was made during the learning of Yolov4, the format of the `annotation` is based on Yolov4

`trans coco` is the tools in the Yolo Project for converting COCO formatted data

`trans voc` is the tools in the Yolo Project for converting VOC formatted data

My tool is after the format conversion, by reading the above tools’ output (TXT documents) to get some key information (such as image path, bbox coordinates) , and then cut

>Ask：Why is there a need for format conversion?
>Ans：Because Im lazy o_o

### Needed Packages

opencv-python numpy absl

### Use

You can use it in the console

Type `python image_cut.py --help` than you can get help

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

Example：

```
python image_cut.py --fap ./data/dataset/tiny_train.txt --oap ./data/dataset/tiny_cut_train.txt --oip ./data/tiny_set/train/labeled_cut_images --size 416
```

## Follow-up Work

No data format conversion, can directly read Coco or VOC annotations
