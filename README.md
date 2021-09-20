# EVA Session 0 - Assignment 1 (Introduction)

## Some questions to answer:
**1) What are Channels and Kernels (according to EVA)?**

Channels are containers of information about image (or any other forms of input such as audio or text). It takes 3 channels (RGB) or 4 channels (CMYK) to hold information about an image (picture) with color details (per convention), or 1 channel (gray-scale) to hold information on monochromic images.

Kernels are extractors of 'information of specific interest' such as edges (for initial stages) and features / components at later stages. They are defined by arrays of weights which attaches due relevance to the input values from channels. 

The terms channels, feature bags, feature maps mean the same, while the terms kernels, feature extractors, filters mean the same (considering 2D convolutions). In case of 3D convolutions, a filter could refer to a set of kernels.

**2) Why should we (nearly) always use 3x3 kernels?**

The basic unit of image representation is a pixel, and the nature (value) of one pixel depends mostly on its neighboring pixels which means a 3 x 3 matrix. This is analogous to the application of 1st order differential for updating a function for changes in any of the independent variables defining that function. Well, that is the intuition behind using a 3x3 kernel for convolution operations.

Added to that, a 3x3xd kernel yields 9d parameters, and convolving a 5x5xd once over a layer (of dimension nxnxd) adds 25d parameters while convolving 3x3 twice over the same layer adds 18d parameters to the model size (likewise 49d paramters for a single 7x7 convolution, and so on). This assumes significance for more number of channels (d) present in the input or preceeding layers to the current layer.


**3) How many times do we need to perform 3x3 convolution operations to reach close to 1x1 from 199x199 (type each layer output like 199x199 > 197x197 ...)**

199, 197, 195, ..., 5, 3, 1. --> This is a sequence of difference, d = -2.

a = 199, d = -2, n = we don't know yet, l = 1
n = (l-a)/d + 1 = -198/-2 + 1 = 100

It takes a set of 100 layers or convolution operations to reach to 1x1.

**4) How are kernels initialized?**

Usually the kernels are initialized using random weights, and these random weights could come from any distributions, e.g. Gaussian distribution. Some distributions are found to be optimal to attain convergence. Xavier distribution (relies on maintaining the [same or similar] variance of the activations across every layer) is preferred over Gaussian distribution (relies on keeping zero mean of activations across every layer).

**5) What happens during the training of a DNN?**

Deep Neural Network (DNN) is designed to update the weights at each layer by means of backward propagation of gradients. One complete cycle consisting of forward and backward propagation for the whole training data is termed as one epoch. During forward propagation, the existing weights of the filter are convolved over the inputs from the previous layer per model definition, yielding outputs at each layer that are fed as inputs for the successive layers, and finally yielding the loss term and the target value. During backward propagation, the gradients for each layer are computed (starting with the last layer yielding the loss term) so that the existing weights are updated based on the gradients computed. 



