# cocoeval_with_yolov7
custom dataset evaluate using pycocotools

## Installation

- setup default environment

```bash
conda create -n cocoevalYOLO python=3.9 -y
conda activate cocoebalYOLO
# you must modify cudatoolkit version
conda install pytorch torchvision torchaudio cudatoolkit=11.3 -c pytorch -y
pip install -r requirements.txt
```

- Install yolov7

```bash
git clone https://github.com/WongKinYiu/yolov7
git clone https://github.com/Taeyoung96/Yolo-to-COCO-format-converter
```

## Step for get coco dataset metric Results

### step1. setup yolov7 custom dataset
---------------------------

- if you already have custom dataset, jump to step2
- see the following link for preparation for custom datasets
- [link1](https://blog.roboflow.com/yolov7-custom-dataset-training-tutorial/), [link2](https://www.analyticsvidhya.com/blog/2022/08/how-to-train-a-custom-object-detection-model-with-yolov7/)

### step2. get yolov7 custom dataset test result best_predictions.json
---------------------------

- you have to validation your custom dataset using `yolov7/test.py` and then you will get best_predictions.json file in test result folder
 

### step3. yolov7 dataset format to coco format, only valid or test dataset
---------------------------

- conversion yolo to coco format using [this](https://github.com/Taeyoung96/Yolo-to-COCO-format-converter) or other method

### step4. get coco dataset metric result
---------------------------

```
python get_coco_metric.py --annotation <valid or test dataset json file> --prediction <best_predictions.json file in your test result folder>
```

- example

```bash
python get_coco_metric.py --annotation anno.json --prediction res.json
#### example output
loading annotations into memory...
Done (t=0.00s)
creating index...
index created!
Loading and preparing results...
DONE (t=0.00s)
creating index...
index created!
Running per image evaluation...
Evaluate annotation type *bbox*
DONE (t=0.00s).
Accumulating evaluation results...
DONE (t=0.00s).
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 1.000
 Average Precision  (AP) @[ IoU=0.50      | area=   all | maxDets=100 ] = 1.000
 Average Precision  (AP) @[ IoU=0.75      | area=   all | maxDets=100 ] = 1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = 1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Precision  (AP) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=  1 ] = 1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets= 10 ] = 1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=   all | maxDets=100 ] = 1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= small | maxDets=100 ] = 1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area=medium | maxDets=100 ] = -1.000
 Average Recall     (AR) @[ IoU=0.50:0.95 | area= large | maxDets=100 ] = -1.000
```

## [Example.ipynb](./example.ipynb)


## Reference

- https://github.com/Taeyoung96/Yolo-to-COCO-format-converter, yolo format to coco format
- https://github.com/WongKinYiu/yolov7, yolov7