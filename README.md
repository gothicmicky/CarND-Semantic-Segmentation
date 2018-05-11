# Semantic Segmentation
### Introduction
The goal of this project is to label the pixels of a road in images using a Fully Convolutional Network (FCN). The FCN paper can be found [here](https://people.eecs.berkeley.edu/~jonlong/long_shelhamer_fcn.pdf). 

FCNs consist of two part, encoder and decoder. The encoder is usually a normal pretrained CNN (e.g. VGG or GoogleNet). The fully connected layers are replaced by 1x1 convolution.
The image is then "upsampled" through the use of "deconvolution" layer (transposed convolutional layers) to restore to the original size. 

### Setup
##### Frameworks and Packages
Make sure you have the following is installed:
 - [Python 3](https://www.python.org/)
 - [TensorFlow](https://www.tensorflow.org/)
 - [NumPy](http://www.numpy.org/)
 - [SciPy](https://www.scipy.org/)
##### Dataset
Download the [Kitti Road dataset](http://www.cvlibs.net/datasets/kitti/eval_road.php) from [here](http://www.cvlibs.net/download.php?file=data_road.zip).  Extract the dataset in the `data` folder.  This will create the folder `data_road` with all the training a test images.

### Implement
Reused the VGG network, pulling out the layer 3/4/7 and follow the FCN paper to implemenet the FCN-8. 
![alt text](assets/FCN.png "FCN architecture")

### Run
Run the following command to run the project:
```
python main.py
```
 
 ### Tips
- The link for the frozen `VGG16` model is hardcoded into `helper.py`.  The model can be found [here](https://s3-us-west-1.amazonaws.com/udacity-selfdrivingcar/vgg.zip)
- The model is not vanilla `VGG16`, but a fully convolutional version, which already contains the 1x1 convolutions to replace the fully connected layers. Please see this [forum post](https://discussions.udacity.com/t/here-is-some-advice-and-clarifications-about-the-semantic-segmentation-project/403100/8?u=subodh.malgonde) for more information.  A summary of additional points, follow. 
- The original FCN-8s was trained in stages. The authors later uploaded a version that was trained all at once to their GitHub repo.  The version in the GitHub repo has one important difference: The outputs of pooling layers 3 and 4 are scaled before they are fed into the 1x1 convolutions.  As a result, some students have found that the model learns much better with the scaling layers included. The model may not converge substantially faster, but may reach a higher IoU and accuracy. 
- When adding l2-regularization, setting a regularizer in the arguments of the `tf.layers` is not enough. Regularization loss terms must be manually added to your loss function. otherwise regularization is not implemented.
 
 ### More about FCN
 
 ### References
 