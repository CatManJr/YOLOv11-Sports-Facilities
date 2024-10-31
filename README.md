# Dataset-for-Shanghai-Sports-Facilities-Detection
### *Dataset used in a competition*
Sincere appreciation to the original contributor, ***Mr. Liu Chang*** who once worked in the ***Key Laboratory of Geographic Information Science, Ministry of Education, East China Normal University, Shanghai, People’s Republic of China***.  
Our further plan is to enrich the dataset into a benchmark set of outdoor sports facilities in the Yangtze River Delta region.

### *Model choices*
This dataset uses a label style consisting of DOTA obb style like:  
```
  x1      y1       x2        y2       x3       y3       x4       y4       classname     diffcult

1686.0   1517.0   1695.0   1511.0   1711.0   1535.0   1700.0   1541.0   large-vehicle      1
```
So it can be used in any object detection model that accepts the DOTA obb style.

In the competition, we implemented the repository below:  
https://github.com/hukaixuan19970627/yolov5_obb & https://github.com/SSTato/YOLOv7_obb  
Sincere appreciation and best wishes to the writers, 胡凯旋 & SSTato!
*******
