# VIDI: A Video Dataset of Incidents

We present a video dataset --- Video Dataset of Incidents, VIDI --- that contains 4,534 video clips corresponding to 43 incident categories. This is the official VIDI repository. In this repository, we provide the code to download our dataset and additional materials for our results.

Samples from the dataset can be found here: https://vididataset.github.io/VIDI/

## Statistics
VIDI contains 4,534 unique videos in total. Since some of the videos have more than one label, there are 4,767 labels in the dataset. Each incident class has around 100 video clips. The number of videos per class is shown figure.

![](https://i.imgur.com/NNVnOca.png)

Mainly, six different common languages have been used in video queries. These languages are English, Turkish, French, Spanish, Simplified Chinese, and Standard Arabic. Apart from these languages, when the amount of collected videos is not sufficient, to collect more videos, Hindi, German, and several other languages have also been used in the dataset. The language statistics of the collected video
clips are shown in the table.

<div align="center">

| Language | # of clip | 
| ----------- | ----------- |
| English |  2140 |  
| Spanish |  560 |  
| Turkish |  452 |   
| French |  376 |   
| Simplified Chinese |  343 |   
| Standard Arabic |  280 |  
| Other |  144 | 
</div>

## Implementation Details


The training parameters used in the experiments are listed in the table. 

| Experiments | Optimizer | Loss fn | Base Learning Rate | LR shrinkage | # of frames |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| ViT on Incidents Dataset | SGD | CE Loss | 0.001 | lambdaLR | 1 | 
| TimeSformer on Incidents Dataset | Adam | CE Loss | 0.005 | - | 1 |
| TimeSformer on VIDI | SGD | BCE with Logits | 0.01 | MultiStepLR | 8 |  
| TimeSformer on VIDI | SGD | BCE with Logits | 0.01 | MultiStepLR | 1 | 
| ViT on VIDI | SGD | BCE with Logits | 0.25 | ReduceLROnPlateau | 1 |  

## Benchmark Results

Top-1 and Top-5 accuracies (%) of different models on the datasets. 

*Using multiple frames. In the rest of the experiments, a single frame is used. 

†Result was published in Incidents Dataset

<div align="center">

| Architecture      | Dataset | Top-1 Acc | Top-5 Acc   |
| ----------- | ----------- | ----------- | ----------- |
| ResNet-18† | Incidents Dataset | 77.30 |  95.90 | 
| ViT | Incidents Dataset | 78.50 | 96.33  |  
| TimeSformer | Incidents Dataset | **81.47** | **96.95**  | 
| ViT | VIDI | 61.78  | 86.78 |
| TimeSformer | VIDI | 67.37 | 90.59  |
| TimeSformer | VIDI* | **76.56**  | **96.51** |

</div>

## Error Analysis

We further analyzed the wrong predictions on the VIDI test set. Some sample frames from wrong predictions can be seen in the figure. As can be observed, in some cases, the inputs are visually very similar to the samples of the predicted classes. 

![](https://i.imgur.com/dpgoWQj.png)

In the figure, we showed the false prediction matrix. From this matrix, one can observe which classes are mostly confused by the model. The most misclassified classes are found to be ”ice storm & snow-covered”, ”flooded & storm surge”, and ”landslide & rockslide rockfall”

![](https://i.imgur.com/FMwK4WM.png)

Finally, we have calculated the prediction accuracy per class as shown in the figure. The video clips are labeled with ”bicycle accident”, ”nuclear explosion”, ”dirty contamined”, ”airplane accident”, ”wildfire”, ”traffic jam”, ”tornado”, ”dust sand storm”, ”dust devil”, and ”snow-covered” have been predicted with higher accuracies than the other classes. It can be seen that the lowest accuracy belongs to the ”landslide”. According to the results, the classes with lower accuracies are mostly mixed within different vehicle accidents

![](https://i.imgur.com/UgmoJYh.png)

## How to Download Videos

Clone repo and enter directory
  > git clone https://github.com/vididataset/VIDI.git
  > 
  > pip install --upgrade youtube-dl
  
Execute following code:
  > python download.py path/to/csv /path/to/location/


## Reference

This study is accepted for IVMSP 2022.

> Sesver D., Gençoglu A. E., Yıldız Ç. E., Gunindi Z., Habibi F., Yazıcı Z. A., Ekenel H. K. VIDI: A Video Dataset of Incidents. 2022 IEEE 14th Image, Video, and Multidimensional Signal Processing Workshop (IVMSP 2022).

