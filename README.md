# Pedestrian Detection

In this work we show the transition from non-neural methods, like Histogram-of-Gradients + SVM, to neural methods, like Faster RCNN, for object detection, specifically, pedestrian detection. We use [Penn-Fudan Pedestrian Detection Dataset](https://www.cis.upenn.edu/~jshi/ped_html/) for evaluating our model's performance.

## Results

|                       Model                       | Mean Average Precision (mAP) | Average Recall @ 1dpi | Average Recall @ 10dpi |
| :-----------------------------------------------: | :--------------------------: | :-------------------: | :--------------------: |
| Pretrained HoG Detector (on INRIA Person dataset) |             0.04             |         0.06          |          0.14          |
|                Custom HoG Detector                |             0.15             |         0.13          |          0.29          |
|                    Faster-RCNN                    |             0.76             |         0.30          |          0.82          |



## Installation
```bash
git clone https://github.com/sm354/Pedestrian-Detection.git
cd Pedestrian-Detection
pip install -r requirements.txt
```

`PennFudanPed_train.json`, and `PennFudanPed_val.json` contains COCO annotations for a randomly generated train-val split of the PennFudan dataset. 

##### Download Penn-Fudan Dataset

```
wget https://www.cis.upenn.edu/~jshi/ped_html/PennFudanPed.zip
unzip PennFudanPed.zip 
```

##### Download SVM model weights

```bash
gdown 1zfU44JxyHCUSWJ7ngiKyqJocgdF82pVt
```

## Running Models

#### 1. Pretrained HoG Detector

```bash
python eval_hog_pretrained.py --root <path to dataset root directory> --test <path to test json> --out <path to output json>
```

#### 2. Custom HoG Detector

**Training** (HoG descriptors + SVM Model)

```bash
python train_hog_custom.py --root <path to dataset root directory> --train <path to train json> --model <path to save trained SVM model>
```

**Testing**

```bash
python eval_hog_custom.py --root <path to dataset root directory> --test <path to test json> --out <path to output json> --model <path to trained SVM model>
```

#### 3. Faster RCNN

```bash
python eval_faster_rcnn.py --root <path to dataset root directory> --test <path to test json> --out <path to output json>
```

### Evaluation script

    python eval_detections.py --gt <path to ground truth annotations json> --pred <path to detections json>

The script `eval_detections.py` takes in ground truth annotations and predicted detections for the evaluation dataset and computes the following metrics:

1. Average Precision, computed over 10 IOU thresholds in the range 0.5:0.05:0.95
2. Average Recall computed at 1 detection per image.
3. Average Recall comptued at 10 detections per image.

## Authors

- [Shubham Mittal](https://www.linkedin.com/in/shubham-mittal-6a8644165/)
- [Aditi Khandelwal](https://www.linkedin.com/in/aditi-khandelwal-991b1b19b/)

Course assignment in Computer Vision course ([course webpage](https://www.cse.iitd.ac.in/~chetan/teaching/col780-2020.html)) taken by [Prof. Chetan Arora](https://www.cse.iitd.ac.in/~chetan)

