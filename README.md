# BSDN: Context-Aware Bidirectional Spatial Dropout Network for Weakly-Supervised Object Detection
This is a PyTorch implementation of our BSDN.

## Contents
### 1. Hardwares
NVIDIA GTX 1080Ti (11G of memory) is OK  
NVIDIA GTX 2080Ti (11G of memory) is OK  
NVIDIA GTX 3090Ti (24G of memory) is OK  

### 2. Installation
1. Clone the BSDN repository  
```
git clone https://github.com/zhengshangdong/BSDN.git
```  
2. Install libraries  
See [install.sh](https://github.com/zhengshangdong/BSDN/blob/master/install.sh)

### 3. Datasets  
Download VOC2007, 2012, and MS-COCO datasets and use the following basic structure to organize these data
```
$VOC2007/                           
$VOC2007/annotations
$VOC2007/JPEGImages
$VOC2007/VOCdevkit
```
```
$MSCOCO/                           
$MSCOCO/annotations
$MCSOSO/train2014
$MSCOCO/val2014
```
All the annotations, proposals, and models can be downloaded from [link1](https://baidu.com) or [link2](https://baidu.com). Please put the annotations into the corresponding `annotations` folder.  

Create symlinks
```
mkdir data
mkdir pretrained_model
mkdir selevtive_search_data
cd data
ln -s /MSCOCO/annotations data/coco/annotations
ln -s /MSCOCO/train2014 data/coco/train2014
ln -s /MSCOCO/val2014 data/coco/val2014
```
```
ln -s /VOCdevkit/VOC2007 data/voc/VOC2007
ln -s /VOCdevkit/VOC2012 data/voc/VOC2012
```
Please put proposals into `selevtive_search_data` folder and put vgg16_caffe.pth into `pretrained_model` folder.
### 4. Training and testing
Evaluating the released model:
```
CUDA_VISIBLE_DEVICES=0 python tools/test_net.py \
  --dataset voc2007test \
  --cfg configs/baselines/vgg16_voc2007.yaml \
  --load_ckpt Outputs/vgg16_voc2007/$model_path \
  --vis False
```
Detection results will be dumped in the `Outputs/vgg16_voc2007/$model_path/test` folder. You can set --vis to True to visualize the detection results.


### 5.Known issues
1. Since the VOC2007 dataset is very small, the performance on VOC2007 is not stable. Please re-training our methods on VOC2012 or MS-COCO to verify the performance of BSDN. 
2. The best results of VOC datasets usually are not achieved in the last epoch. Please save the intermediate models. You can also set the random seed SEED. Note that setting SEED to a fixed value still cannot guarantee deterministic behavior.
