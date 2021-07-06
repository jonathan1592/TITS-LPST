# License Plate Detection via Information Maximization (TITS-LPST)

This is the official website for "License Plate Detection via Information Maximization (submitted to T-ITS 2020)", which is a newly built real-world dataset for license plate detection and scene text detection.
- 9.7k+ images and 110k+ instances
- Scenes: **traffic** and **drone**, Tasks: **license plate detection** and **scene text (excluding license plate) detection**
- **Variations in tilt degrees**: Horizontal tilt degree (15 ~ 45 degrees) and vertical tilt degree (15 ~ 45 degrees).
- **Variations in distance**: The distance from the license plate to the camera location is relatively diverse.
- **Variations in blur**: Blurry image due to motion blur and hand jitter while capturing images.
- If you are interested in license plate detection, please refer to [our paper] or [our github project](https://github.com/brightyoun/TITS-LPST).

![Examples of DHD](imgs/tits-007.jpg)

#### Younkwan Lee, Jihyo Jeon, Yeongmin Ko, Moongu Jeon, Witold Pedrycz

## Table of Contents
0. [Abstract](#0)
1. [Introduction](#1)  
2. [License Plate Detection Benchmarks](#2)  
   2.1 [LPST-110K Sample](#2.1)  
   2.2 [Full dataset](#2.2)   
3. [Benchmark](#4)  
   3.1 [TJU-DHD-traffic](#4.1)  
   4.2 [TJU-DHD-campus](#4.2)   
   4.3 [TJU-DHD-pedestrian](#4.3) 
5. [Citation](#5)  
6. [Evaluation on the test set](#6) 
7. [Contact](#7) 

## Abstract <a name="0"></a>
License plate (LP) detection in the wild remains challenging due to the diversity of environmental conditions.  Nevertheless,  prior solutions have focused on controlled environments,  such as when  LP  images frequently emerge as from an approximately frontal viewpoint and without scene text which might be mistaken for an LP. However, even for state-of-the-art object detectors, their detection performance is not satisfactory for real-world environments, suffering from various types of degradation. To solve these problems, we propose a novel end-to-end framework for robust LP detection, designed for such challenging settings. Our contribution is threefold:  (1) A novel information-theoretic learning that takes advantage of a shared encoder, an LP detector and a scene text detector (excluding LP) simultaneously; (2) Localization refinement for generalizing the bounding box regression network to complement ambiguous detection results; (3) a large-scale, comprehensive dataset, LPST-110K, representing real-world unconstrained scenes including scene text annotations. Computational tests show that the proposed model outperforms other state-of-the-art methods on a variety of challenging datasets.License plate (LP) detection in the wild remains challenging due to the diversity of environmental conditions.  Nevertheless,  prior solutions have focused on controlled environments,  such as when  LP  images frequently emerge as from an approximately frontal viewpoint and without scene text which might be mistaken for an LP. However, even for state-of-the-art object detectors, their detection performance is not satisfactory for real-world environments, suffering from various types of degradation. To solve these problems, we propose a novel end-to-end framework for robust LP detection, designed for such challenging settings. Our contribution is threefold:  (1) A novel information-theoretic learning that takes advantage of a shared encoder, an LP detector and a scene text detector (excluding LP) simultaneously; (2) Localization refinement for generalizing the bounding box regression network to complement ambiguous detection results; (3) a large-scale, comprehensive dataset, LPST-110K, representing real-world unconstrained scenes including scene text annotations. Computational tests show that the proposed model outperforms other state-of-the-art methods on a variety of challenging datasets.


## 1. Introduction <a name="1"></a>

Object detection research has attracted great interest in recent years, with models being applied widely in many traffic-related applications. A variety of methods have demonstrated high accuracy in detecting license plates (LP) under controlled settings. While existing detectors successfully applied to the LP detection problem, many key challenges still remain in \textit{unconstrained wild scenarios}. For example, real-world LP detection causes the following problems: modifications of prior settings to adapt to wild, incorrect detection results, ambiguity in classifying objects associated with scene text, low-quality visual data, uneven lighting, motion blur, and others. However, such scenarios are becoming increasingly common and gaining significant popularity in a variety of applications, including civil security, crowd analytics, law enforcement, and street view images. Despite being the most common scenario, LP benchmarks still do not consider real-world cases, and therefore many problems are not adequately addressed. As a result, state-of-the-art detectors struggle with these images. we propose an end-to-end framework which is composed of a single shared feature encoder and two parallel detection branches. The single shared encoder learns a global feature across all detection tasks (LP and non-LP respectively). More specifically, due to non-LP objects (scene text but not LP), our framework is divided into 1) LP detection network and 2) non-LP detection network. Different from traditional LP detection models, we explicitly prevent learning of non-LP objects. To this end, we bring a novel information-theoretic loss to minimize mutual information between the embedding feature and non-LP distribution that interferes with LP detection. We collect a new large-scale dataset, LPST-110K, containing images captured from unconstrained scenes. To the best of our knowledge, LPST-110K is the first dataset to address LP and scene text simultaneously for LP detection. By evaluating state-of-the-art detection models on LPST-110K, we demonstrate the accuracy improvement of our proposed model compared with other approaches.

## 2. License Plate Detection Benchmarks <a name="2"></a>

| name       | \#images               | \#instances               | \#LP instances/Image  | \#ST instances/Image     | \#Variations in tilt degrees. | \#Variations in distance. |  \#Variations in blur. |
| :--------- | :--------------------: | :-----------------------: | :-------------------: | :----------------------: | :---------------------------: | :---------------------------: | :---------------------------: |
| AOLP       |         2,049          |          2,049            |        1              |         1                | ✓ | ✗ | ✓ |
| SSIG       |         2,000          |          8,683            |        4.34           |         4.34             | ✗ | ✓ | ✗ |
| PKU        |         3,977          |          4,389            |        1.10           |         1.10             | ✗ | ✗ | ✗ |
| UFPR       |         4,500          |          4,500            |        1              |         1                | ✗ | ✓ | ✓ |
| CD-HARD    |         102            |          102              |        1              |         1                | ✓ | ✓ | ✗ |
| CCPD       |         250K           |          250K             |        1              |         1                | ✓ | ✓ | ✓ |
| **LPST-110K**  |         9,795        |          110K             |        **5.21**         |         **11**       | ✓ | ✓ | ✓ |
 
### Annotations format
The CSV file with annotations should contain one annotation per line.
Images with multiple bounding boxes should use one row per bounding box.
Note that indexing for pixel values starts at 0.
The expected format of each line is:
```
path,x1,y1,x2,y2,class_name
```

#### 2.1 LPST-110K Sample <a name="2.1"></a>
* SAMPLE 001 set:
    * images:
      [Google Drive](https://drive.google.com/file/d/1gCy0k7afMqYMuTjo4Vna2P_IfLLeRTdI/view?usp=sharing)
    * full annotations:
      [Google Drive](https://drive.google.com/file/d/1pmgP4ccrAGwRPfCDnJHG16Q72euH6nd8/view?usp=sharing)
    * license plate annotations:
      [Google Drive](https://drive.google.com/file/d/19o-4xX6Pk9y0QUK0CWuJso1vQF4Y33Nl/view?usp=sharing)
    * scene text annotations:
      [Google Drive](https://drive.google.com/file/d/19XVGtJXvRGqjij-w5kR4oVNNyWcgQ5c3/view?usp=sharing)
    * full images:
      [Google Drive](https://drive.google.com/file/d/16XAH_uDH-wmGMKVWdni2vSXU8zSTk6dL/view?usp=sharing)
      
* SAMPLE 002 set:
    * images:
      [Google Drive](https://drive.google.com/file/d/1iLFhmBT2JMK4ZKZZv8IK7wTa-Xnza5I8/view?usp=sharing)
    * full annotations:
      [Google Drive](https://drive.google.com/file/d/1yHOXeFY3WCasgtgXYQHGKL68Qw429IgY/view?usp=sharing)
    * license plate annotations:
      [Google Drive](https://drive.google.com/file/d/1JERu9Dy2YSQONV-xiR5kTD36AJA3bQ16/view?usp=sharing)
    * scene text annotations:
      [Google Drive](https://drive.google.com/file/d/1jlqKL5_4wOctYCS0X6rvm_df1ysndKCO/view?usp=sharing)
      
* SAMPLE 003 set:
    * images:
      [Google Drive](https://drive.google.com/file/d/1VFTH3uzcQMPyl9uCj5ScLVCWFAxyLyL7/view?usp=sharing)
    * full annotations:
      [Google Drive](https://drive.google.com/file/d/1XnXWa3NR5bjwO_cq5Gf2xLivpLUQ0fHI/view?usp=sharing)
    * license plate annotations:
      [Google Drive](https://drive.google.com/file/d/1qMIt3gBH5kDDER7OY1cKCtwY9A1JhBcS/view?usp=sharing)
    * scene text annotations:
      [Google Drive](https://drive.google.com/file/d/1RwKYCxylV4t7LJXBJplzzGfrAhfCENHi/view?usp=sharing)
      
 * SAMPLE 004 set:
    * images:
      [Google Drive](https://drive.google.com/file/d/1iLFhmBT2JMK4ZKZZv8IK7wTa-Xnza5I8/view?usp=sharing)
    * full annotations:
      [Google Drive](https://drive.google.com/file/d/1yHOXeFY3WCasgtgXYQHGKL68Qw429IgY/view?usp=sharing)
    * license plate annotations:
      [Google Drive](https://drive.google.com/file/d/1JERu9Dy2YSQONV-xiR5kTD36AJA3bQ16/view?usp=sharing)
    * scene text annotations:
      [Google Drive](https://drive.google.com/file/d/1jlqKL5_4wOctYCS0X6rvm_df1ysndKCO/view?usp=sharing)
      
* evaluation tools:
  [cocoapi](https://github.com/cocodataset/cocoapi)

#### 2.2 Full dataset <a name="2.2"></a>
To see full dataset, here's the Email and request Dataset [contact us](brightyoun@gist.ac.kr).
* evaluation tools:
  [cocoapi](https://github.com/cocodataset/cocoapi)


## 3. License Plate Detection Results on Benchmarks <a name="4"></a>

#### 3.1 AOLP Dataset <a name="4.1"></a>

* Results on AOLP

  |              | :AOLP         |           |              |           |              |           : |
  | method       | AC Precision | AC Recall | LE Precision | LE Recall | RP Precision | RP Recall  |
  | :----------- | :----------: | :-------: | :----------: | :-------: | :----------: | :--------: |
  | Hsu          | 91.00        |  96.00    | 91.00        |  95.00    |  91.00       | 94.00      |
  | Li           | 98.53        |  98.38    | 97.75        |  97.62    |  95.28       | 95.58      |
  | Selmi        | 92.60        |  96.80    | 93.50        |  93.30    |  92.90       | 96.20      |
  | Rafique      | -            |  98.09    | -            |  93.92    |  -           | 89.03      |
  | Xie          | 99.51        |  99.51    | 99.43        |  **99.43**    |  99.46       | 99.46      |
  | Li           | -            |  99.12    | -            |  99.08    |  -           | 98.20      |
  | Bjorklund    | **100**          |  99.30    | **99.80**        |  99.00    |  **99.80**       | **99.00**      |
  | Selmi        | 99.30        |  99.40    | 99.20        |  99.20    |  98.90       | 98.80      |
  | **Ours**     | **99.71**        |  **99.80**    | **99.80**        |  **99.32**    |  **99.71**       | **98.79**      |
  
|             |          Grouping           ||
First Header  | Second Header | Third Header |
 ------------ | :-----------: | -----------: |
Content       |          *Long Cell*        ||
Content       |   **Cell**    |         Cell |

New section   |     More      |         Data |
And more      | With an escaped '\|'         ||  

#### 4.2 TJU-DHD-campus <a name="4.2"></a>

* Results on validation

  | method       | backbone | input size |  AP   | AP@0.5 | AP@0.75 | AP_t  | AP_s  | AP_l  | AP_l  |
  | :----------- | :------: | :--------: | :---: | :----: | :-----: | :---: | :---: | :---: | :---: |
  | RetinaNet    | ResNet50 |  1333x800  | 48.4  |  79.3  |  52.4   |  4.7  | 27.3  | 56.2  | 73.8  |
  | FCOS         | ResNet50 |  1333x800  | 49.3  |  73.8  |  53.8   |  5.6  | 29.6  | 55.9  | 74.3  |
  | FPN          | ResNet50 |  1333x800  | 52.4  |  77.5  |  58.4   |  8.5  | 37.4  | 58.6  | 74.9  |
  | Cascade RCNN | ResNet50 |  1333x800  | 55.1  |  77.6  |  60.9   | 10.8  | 40.1  | 61.2  | 78.8  |

#### 4.3 TJU-DHD-pedestrian <a name="4.3"></a>

* Miss rate with same-scene evaluation

  | method |  R/RS/HO/R+HO/A (TJU-Ped-campus)  | R/RS/HO/R+HO/A (TJU-Ped-traffic)  |
  | :----- | :---------------------------: | :---------------------------: |
  | FPN    | 27.92/73.14/67.52/35.67/38.08 | 22.30/35.19/60.30/26.71/37.78 |

* Miss rate with cross-scene evaluation

  | method | R/R+HO (TJU-Ped-campus -> traffic) | R/R+HO (TJU-Ped-traffic -> campus) |
  | :----- | :-----------------------------------------: | :---------------------------------------------: |
  | FPN    |              30.62 / 33.89               |               42.08 / 50.55               |

## 5. Citation <a name="5"></a>

If this project help your research, please consider to cite our github page.

## 6. Evaluation on the test set <a name="6"></a>

Ablation studies can be conducted on the validation set.
If you would like to evaluate your model on the test set, you can send us (connor#tju.edu.cn, replace `#` with `@`) your detection results in the `json` format.

## 7. Contact <a name="7"></a>

If you have any questions or want to add your results, please feel free to [contact us](brightyoun@gist.ac.kr).
