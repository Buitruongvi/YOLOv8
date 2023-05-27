# Human Detection with YOLOv8
![image](https://github.com/Buitruongvi/YOLOv8/assets/49474873/f1c4f5ea-fc69-4619-bc84-f9354a03422b)

In this project, we will learn and implement the Python source code for Human Detection in an image using an algorithm called YOLOv8.

## Installation

To use this project, follow these steps to set up the environment:

1. Clone the repository: The source code for [YOLOv8](https://github.com/ultralytics/ultralytics) is publicly available on GitHub. 
```python
!git clone https://github.com/ultralytics/ultralytics.git
```
2. Install the required requirement:
```python
%cd ultralytics
!pip install ultralytics
import ultralytics
ultralytics.checks()
```
3. Download the pre-trained YOLOv8s weights: [YOLOv8s](https://github.com/ultralytics/assets/releases/download/v0.0.0/yolov8s.pt)
```python
!wget https://github.com/ultralytics/assets/releases/download/v0.0.0/yolov8s.pt
```
## Download dataset

The human dataset can be downloaded [here](https://drive.google.com/drive/folders/12FNzjRpVDUf2fFlhZfrIrIRWfseLg6fM?usp=share_link). You can manually download the .zip file or use the following command lines to download and automatically extract the file:
```python
!gdown https://drive.google.com/drive/folders/12FNzjRpVDUf2fFlhZfrIrIRWfseLg6fM?usp=share_link
!unzip /content/ultralytics/human_detection_dataset.zip
```
## Training

After completing the preparation steps, we will proceed with training using the prepared dataset. Please execute the following command line (for different datasets, you need to change the corresponding .yaml file name):
```python
!yolo train model=yolov8s.pt data=./human_detection_dataset/data.yaml epochs=20 imgsz=640
```
Check the **./runs** directory, and you will find a file named **./detect/train**. This file is the output of YOLOv8s.
Here are the basic meanings of some of these parameters:
- **img**: The size of the training images. The training and test images will be resized to the specified size, which is 640 by default. You can experiment with different image sizes.
- **batch**: During the training process, models can either read the entire training data at once or divide it into batches for processing. The default value is 64, meaning the training data will be divided into batches of 64 samples. You can set different values according to 2^n (n ≥ 0).
epochs: The number of times the dataset is iterated during training.
- **data**: Information about the dataset (in the .yaml file) you want to use for training.
- **weights**: The file of the pretrained model to be used. You can download and use different pretrained model files from the provided list.

## Predict
With uploaded image:
```python
from google.colab import files
uploaded = files.upload()
filename = next(iter(uploaded))
print(f"Uploaded file: {filename}")

!yolo predict model=./runs/detect/train/weights/best.pt source='image_path>'
```
With online image:
```python
!yolo predict model=/content/ultralytics/detect/train/weights/best.pt source='image_address'
```


# References
