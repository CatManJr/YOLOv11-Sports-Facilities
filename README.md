# YOLOv11-Sports-Facilities
*Updated Jan 3 2025*
*Geo Data Mining using YOLOv11-obb + SAHI*
*****
### *Model*
In the updated repository, we implemented the latest Ultralytics YOLOv11-obb to learn our outdoor sports facilities dataset.
On our validation dataset, YOLOv11n-obb and YOLOv11s-obb achieved very high mAP:

| Model               |  Input Size   | Precision(B) | Recall(B) | mAP50(B)  | mAP50-95(B) |
|---------------------| ------------- |--------------|-----------|-----------|-------------|
| yolov11n-obb-100    | 1024 * 1024px | 0.9647       | 0.93973   | 0.97289   | 0.87496     |
| yolov11n-obb-150    | 1024 * 1024px | 0.97194      | 0.92553   | 0.96654   | 0.89414     |
| yolov11s-obb-200    | 1024 * 1024px | 0.96612      | 0.95119   | 0.98045   | 0.93171     |

We found that although a larger model cannot get improvement in P & R, the detection boxes are much more satisfying.

*Note that yolov11s-obb-200 may be over-fitted.*

### *Interference and Shapefile*
We found that using SAHI(Structured Attention-based Hierarchical Inference) can greatly improve the performance of the pre-trained model on 2048 * 2048px images.
You can find both hbb box and obb mask in the picture below
<p align="center">  
  <img src = https://imgur.com/X81PdqW.png alt = "use VPN to load the image" title="SAHI result demo", height = 400px, wide = auto>
</p>


Also, we found that the detection results of the obb model in SAHI are the `sahi.annotation.mask` object. So we provide a pipeline of how to draw the mask directly into the ESRI polygon, which is amazingly precise.

Here is a demo of our shapefile in ArcGIS Pro:
<p align="center">  
  <img src = https://imgur.com/UHjPEHn.png alt = "use VPN to load the image" title="SAHI result demo", height = 450px, wide = auto>
</p>

You may try more images in the `test_images` folder, they are actually level 19 images of Nanjing, 2024. So you can feel the strong transfer ability of YOLOv11-obb.

### *Dataset from our lab*
Sincere appreciation to the original contributor, ***Mr. Liu Chang*** who once worked in the ***Key Laboratory of Geographic Information Science, Ministry of Education, East China Normal University, Shanghai, People’s Republic of China***.  
Our further plan is to enrich the dataset into a benchmark set of outdoor sports facilities in the Yangtze River Delta region.

### *Model choices*
This dataset uses a label style consisting of DOTA obb style like:  

| x1      | y1      | x2      | y2      | x3      | y3      | x4      | y4      | classname       | difficult |
|---------|---------|---------|---------|---------|---------|---------|---------|----------------|----------|
| 1686.0  | 1517.0  | 1695.0  | 1511.0  | 1711.0  | 1535.0  | 1700.0  | 1541.0  | large-vehicle  | 1        |

So it can be used in any object detection model that accepts the DOTA obb style.

In the competition, we implemented the repository below:  
https://github.com/hukaixuan19970627/yolov5_obb & https://github.com/SSTato/YOLOv7_obb  
Sincere appreciation and best wishes to the writers, 胡凯旋 & SSTato!

In release v1.0.0, we provide a new version of over dataset for YOLOv11-obb, in such a structure:
```
dataset/
├── images/
│   ├── train/
│   │   └── 1024px*1024px images
│   └── val/
│       └── 1024px*1024px images
└── labels/
    ├── train_original/
    │   └── ...(DOTA labels)
    ├── val_original/
    │   └── ...(DOTA labels)
    ├── train/
    │   └── ...(YOLO-obb labels)
    └── val/
        └── ...(YOLO-obb labels)

```

So now, our dataset can be used directly in Ultralytics YOLO-obb in this style:

| class_index | x1          | y1          | x2          | y2          | x3          | y3          | x4          | y4          |
|------------|------------|------------|------------|------------|------------|------------|------------|------------|
| 0          | 0.780811    | 0.743961    | 0.782371    | 0.74686     | 0.777691    | 0.752174    | 0.776131    | 0.749758    |

Note that the coordinates used in yolo-obb must be standardized. We provide the transform function in the notebook.
### *Code Implementation*
In `yolov11-obb.ipynb` we provide the whole pipeline from `transform dota labels to yolo style` -> `train` -> `Predict with SAHI` -> `Save detection results to ESRI Shapefile`.

The only requirements are `PyTorch`, `Ultralytics`, `SAHI`, and a `GPU` with no less than `8GB of CUDA memory`. 
*******
*Updated Jan 3 2025*
