# Object detection of Tube worms
|label|annotation|
|----|--------------|
|![picture](https://github.com/boguss1225/obect-detection-tubeworm/blob/main/results/val_batch1_labels.jpg)|![picture](https://github.com/boguss1225/obect-detection-tubeworm/blob/main/results/val_batch1_pred.jpg)| \
↑ tubeworm detection result from unseen dataset

# Introduction
Deep-sea tubeworms belong to the annelid group Siboglinidae and have drawn considerable attention due to their abundance and dominance in deep-sea chemosynthetic environments.(Li et al. 2019) \
\
\
![picture](https://github.com/boguss1225/obect-detection-tubeworm/blob/main/results/intro_image.png)
↑ Picture of tube worm. The width of each worm tube is ca. 2 cm. (Hoeksema et al. 2022) \
\
↓ Cropped instances of tube worm.
|       |instance 1       |instance 2      |instance 3     |
|----|--------------|--------------|--------------|
|tubeworm|![picture](https://github.com/boguss1225/obect-detection-tubeworm/blob/main/results/crop1.png)|![picture](https://github.com/boguss1225/obect-detection-tubeworm/blob/main/results/crop2.png)|![picture](https://github.com/boguss1225/obect-detection-tubeworm/blob/main/results/crop3.png)|

# System Requirements
- CPU : AMD EPYC Rome 7352 2P 24-Core CPU 2.3GHz 
- GPU : NVIDIA A40
- Ubuntu : 20.04.5 LTS (GNU/Linux 5.4.0-131-generic x86_64)
- CUDA : 11.5
- Conda : 4.8.3
- Python : 3.9.15
- YOLOv5 : https://github.com/ultralytics/yolov5 (version: f9ca365)

# packages in virtual environment
- numpy==1.23.5
- nvidia-cudnn-cu11==8.5.0.96
- opencv-python==4.6.0.66
- pandas==1.5.2
- Pillow==9.3.0
- torch==1.13.0
- torchaudio==0.13.0
- torchvision==0.14.0

# Data
## Data overview
- Images : 9
- labels : 44
- Augmented : x24 (rotating objects 15 degree)
- class : 1 (only tubeworm-top view)
![picture](https://github.com/boguss1225/obect-detection-tubeworm/blob/main/results/data_collograph.png)
↑ data analysis

## Data features
- tiny (avg less than 40 x 40 px)
- transparent
- rare (only 44 objects in 9 images)

## Data Augmentation methodology
![picture](https://github.com/boguss1225/obect-detection-tubeworm/blob/main/results/augmented_frame1.jpg)
\
augmentation is done based on each object not whole picture.
\
In the given image, you can find only object has been rotated.


# Training Setting
- Base model : YOLOv5L6
(https://github.com/ultralytics/yolov5/releases/download/v6.2/yolov5l6.pt)
- Epoch : 250
- Batch size : 8

# Hyper parameter
- Input Image size : 1280
- Optimizer : SGD
- Learning rate : 0.01
- More detail : check hip.yaml

# Result
## Evaluation on unseen test dataset
|mAP(0.5)       |mAP(0.95)      |Precision     |Recall     |
|-------------|---------------|------------|----------|
|62.9%|41.5%|75.9%|57.1%|

## Inference speed
- **1.3ms** pre-process (only once)
- **48.4ms** inference
- **3.2ms** NMS pre image at shape 1280 x 1280px, 3 channels (RRB)

## Training learning curves
![picture](https://github.com/boguss1225/obect-detection-tubeworm/blob/main/results/training_result.png)

## F1 curve, P curve & R curve
|dataset|F1 curve.    |P curve      |R curve      |
|--------|-----------|-----------|-----------|
|train|![picture](https://github.com/boguss1225/obect-detection-tubeworm/blob/main/results/F1_curve_train.png)|![picture](https://github.com/boguss1225/obect-detection-tubeworm/blob/main/results/P_curve_train.png)|![picture](https://github.com/boguss1225/obect-detection-tubeworm/blob/main/results/R_curve_train.png)|
|test|![picture](https://github.com/boguss1225/obect-detection-tubeworm/blob/main/results/F1_curve_test.png)|![picture](https://github.com/boguss1225/obect-detection-tubeworm/blob/main/results/P_curve_test.png)|![picture](https://github.com/boguss1225/obect-detection-tubeworm/blob/main/results/R_curve_test.png)|

# Common installation errors
https://github.com/boguss1225/obect-detection-tubeworm/issues?q=is%3Aissue+is%3Aclosed

# Further things to do
- Check missing annotation in the image (I think there are some)
- Additional image preprocessing adjustment

# References
- Hoeksema BW, Timmerman RF, Spaargaren R, Smith-Moorhouse A, van der Schoot RJ, Langdon-Down SJ, Harper CE. Morphological Modifications and Injuries of Corals Caused by Symbiotic Feather Duster Worms (Sabellidae) in the Caribbean. Diversity. 2022; 14(5):332. https://doi.org/10.3390/d14050332
- Li, Y., Tassia, M.G., Waits, D.S. et al. Genomic adaptations to chemosymbiosis in the deep-sea seep-dwelling tubeworm Lamellibrachia luymesi. BMC Biol 17, 91 (2019).
- YOLOv5 🚀 : https://github.com/ultralytics/yolov5
