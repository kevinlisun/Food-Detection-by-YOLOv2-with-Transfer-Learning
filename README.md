# Food Detection System Design by DCNN

## 1. What's this repo about

- Hello, this is my project repo for my master degree of McGill University. I proposed a multi-object food detection architecture by deep convolutional neural networks (DCNN) with transferring features. In the world of computer vision, it could be pretty painful if you train everything from scratch. In my research, I pre-trained a food/non-food image classifier and then copy part of its weights to the food detectio neural networks.
- The overall architecture can be visualized like this: 

<img src="https://github.com/jianing-sun/Food-Detection-by-YOLOv2-with-Transfer-Learning/blob/master/asset/overall_method.png" />

Note the structure of *Feature Extraction Network* and *Food Detection Network* can be replaced by any CNN-based architecture as long as they have the same layer arrgement.

- Three state-of-the-art CNN architectures ([MobileNet](https://arxiv.org/pdf/1704.04861.pdf), [MobileNetV2](https://arxiv.org/pdf/1801.04381.pdf), [Resnet-18](https://arxiv.org/pdf/1512.03385.pdf)) have been implemented as backbones and evaluated. Below is the result contrasting the training process (loss history), mAP under different IoU (Intersection over Union) on datasets UECFood100 and UECFood256:

<img src="https://github.com/jianing-sun/Food-Detection-by-YOLOv2-with-Transfer-Learning/blob/master/asset/ablation_results.png"  />

- The effect of transfer learning has been quantified by designing the following experiments on MobileNet:

<img src="https://github.com/jianing-sun/Food-Detection-by-YOLOv2-with-Transfer-Learning/blob/master/asset/tl.png" height="500px" />

​	and the result as below: 

<img src="https://github.com/jianing-sun/Food-Detection-by-YOLOv2-with-Transfer-Learning/blob/master/asset/tlFig.png"  />

- Some results for food detection with MobileNetV2 backend:

<img src="https://github.com/jianing-sun/Food-Detection-by-YOLOv2-with-Transfer-Learning/blob/master/asset/results.png"  />

##2. How to use it

`cam to localize food` - train a food/non-food classifier and calculate Class Activation Mapping (CAM) with  a global averaging pooling (GAP) layer after removing the last several layers to get 14x14 resolution input to feed into the GAP.

`dcnn_yolov2` - apply CNN-based backbones with one-stage detection framework, YOLOv2; the process of how to do transfer learning and the mAP evaluation is also included. (a bit of unorganized)

`example` - a jupyter notebook rice example with MobileNet backend to perform YOLOv2 

`k_means_generated_anchors` - kmeans clustering algorithm to generate bounding box priors (they call anchor box) with trade-off between model complexity and performance.

`01_preprocess_dataset.ipynb` - regulaize all images in the dataset to the same dimension (800, 600) and rescale bounding box annotations

`02_split_uecfood100.ipynb` - split dataset to training set, validation set and testing set

`03_anchor_generator.ipynb` - code for k-means clustering with IoU distance to generate anchor boxes

`04_visualize_anchors.ipynb` - visualize generated anchors

`05_generate_npz.ipynb` - deprecated. I changed to use BatchGenerator (as see in preprocessing.py) to load the training instances to neural networks

`anno_template.xml` - an annotation file example. each image has one `.xml` annotation file (`.xml` files are generated by running `gen_xml_step1.py` and `gen_xml_step2.py` in `dcnn_yolo2` folder)

`aws.ipynb` - some notes when using for Awazon Web Service for training in remote virtual machine (Google Cloud Platform is good also)

`avg_iou.png` - trade-off between the number of anchor boxes with average IoU



