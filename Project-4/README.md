# Architectural Basics

## How many layers
Proper analysis and calculation of number of layers is very important as:
* It impacts the number of parameters that will be present in the network
* If number of kernals are not implemented efficiently then we can lose important features which is not good for the network
* Number of layers determine the Global Receptive Field which is very essential for a network

## Receptive Field
When a kernel convolves over an image and extracts dominant features then that window is known as receptive field. Initially what a kernel sees in known as local receptive field and global recpetive field is what the last kernel see or extracts.

## MaxPooling
Pooling is used to extract the features from our feature maps and pass them to the next layers. Pooling is used to increase the recpetive field of a network and also to decrease channel size resulting in decreasing parameters. We must avoid using maxpooling in predicition layer or when we are close to prediction layer as we may lose dominant information that are present in the channels and thus making our network less reliable.

## 1x1 Convolutons
1x1 convolutions are mostly used to decrease the number of channels without losing any information. It is mostly used in transition block. 1x1 convolutions can also be used to increase the number of channels but thats very rare and is not advised to do so.

## 3x3 Convolutions
3x3 kernels are prefered because it helps us in keeping the parameters/weights to minimum and also helps us in keeping the symmetry intact thus making it much easier to process the image. Also, NVIDIA GPUs are mainly optimised for 3x3 kernels thus models with 3x3 kernels run faster making the model efficient.

## Concept of transition layer
In a network, we always want to reduce the number of channels without losing any information from it. These kind of layers as known as transition layers. Transition layers use 1x1 convolutions to reduce the number of channels efficiently. It is mostly preceded by maxpooling.

## Position of transition layer
Position of transition layer always occurs after we have found:
* Edges and gradients
* Textures and patterns
* Parts of object
* Object

## Position of MaxPooling
* The optimal layer to execute maxpooling is transition layer.
* We should always avoid maxpooling when we are close to prediction layer.

## The distance of MaxPooling from Prediction
We should avoid maxpooling when we are close to prediction layer so that we don't lose any important/dominant features whiel executing it. Maxpooling should be atleat 2 layers away from the prediction layer

## Softmax
Softmax is a probability like which uses exponents. The calculated probability will range from 0 to 1 and the sum of all proababilities is 1. It is mostly used in multiple classification logistic regression model.

## Learning Rate
Learning rate help to keep gradient explosion and vanishing gradient problems in check. An optimal learning rate helps in faster convergence during Gradient Descent.

## LR schedule and concept behind it
* A static learning rate may or may not help in minimizing loss in tuning the parameters thus we use Learning rate schedules to adjust the learning rate during training by reducing the learning rate according to a pre-defined schedule. 
* A bigger learning rate would help us converge faster but we might not reach the global minima. Similarly a small learning rate would increase training time. 
* Common learning rate schedules include time-based decay, step decay and exponential decay.

## Image Normalization
Image Normalization is done as we do not want the pixel values to influence the kernel parameters. The ImageDataGenerator class can be used to rescale pixel values from the range of 0-255 to the range 0-1 preferred for neural network models.

## When to add validation checks
* We can add validation check when we are seeing that our training accuracy is gradually decreasing.
* Validation checks are also helpful in determining if the network is overfitting or underfitting.
* We can also add when the output of the prediction(validation accuracy) is less than the training accuracy.

## Batch Normalization
* It normalizes the parameters of a kernel so as to minimize the covariance shift.
* It is mostly used to tackle overfitting.

## The distance of Batch Normalization from Prediction
Batch normalization is used to standardize the inputs to a network. It is either applied to the activations of a prior layer or to the inputs directly.

## Batch Size, and effects of batch size
Batch size is the number of times parmeters are tuned by the optimizers in an epoch. Batch Size can be increased so as to optimally use the GPU available i.e. we can decrease the runtime of the network by increasing the batch size if hardware permits in the training machine.

## Dropout
* Dropouts are generally used to minimize overfitting.
* It randomly turns off neurons in the network so that the model learns more robust features.

## When do we introduce Dropout, or when do we know we have some overfitting
If there is a relevant gap between training accuracy and test accuracy, then it ia a clear indication of overfitting. In this kind of scenerio, dropout is used.

## Number of Epochs and when to increase them
* Number of epochs is generally calculated using the formula: Number of Epochs = Total Data / Batch Size
* While training a network, if we see that by last epoch the loss function or test accuracy or validation accuracy are changing drastically then it indicates that further epochs are required for robust learning.

## Kernels and how do we decide the number of kernels?
Kernels are nothing but feature extractors. The most favored kernel size is 3x3 as many hardware are optimized for 3x3 convolutions. In the transition layer we use 1x1 kernels to avoid loss of any features but still decreasing the number of channels. 

## When do we stop convolutions and go ahead with a larger kernel or some other alternative (which we have not yet covered)
When building a CNN architecture, we generally stop convolution when we reach a resolution like 9x9 or 7x7 or less as 3x3 convolution and would extract features from it but it does not gives any extra information. So we stop at 3x3 and directly reduce the 7x7 to 1x1 by larger size kernel 7x7

## How do we know our network is not going well, comparatively, very early
While training the network, if we find that there relevant gap between train and validation accuracy then, it may mean that our network is not working properly.

## Adam vs SGD
SGD works well with regular gradient descent when the learning rate is low whereas Adam performs well stochastic gradient decent. According to me, ADAM works well with MNIST dataset.
