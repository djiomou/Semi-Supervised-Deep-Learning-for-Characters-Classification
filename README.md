# Semi-Supervised-Deep-Learning-for-Characters-Classification

 In the search for more effective Deep Learning methods to Overcoming the need for large annotated data sets, we have seen a great deal of research interest in recent years in semi-supervised learning methods. Semi-supervised learning is halfway between supervised and unsupervised learning. In addition to the untagged data, the algorithm is provided with a supervised task. In this context, our work consists in classifying MNIST images from the Tensorflow library using the method used in the article [1]. In this paper, the pretext task is the recognition by the network of the geometrical shapes applied to the data. Following this method, we will first train on the unlabelled data, a network(Basic Network) for predicting the geometrical transformations. The aim being to draw knowledge from it. Then we use this knowledge as a starting point for our supervised network. Finally, to compare the contribution of unsupervised learning on the performance of the network, we build a network called "Baseline" with the same architecture as the base network. 
 
 ## The Bacic network
 Our basic network is built according to the NIN (Network-In-Network) architecture where we have three layer blocks each containing three convolution layers. The convolution layers each have different filters. After each conv2D layer, a batch normalization and a "relu" activation layer is performed. Between the first and the second block, a MaxPooling is performed. Between the second and third block, an averagePooling2D is performed. At the end one performs a globalAverage Pooling and then a dense layer and a softmax activation layer are added.  
 
 ## the Semi-supervised network
 Once the basic network has been trained on transformed unlabelled data, the first two blocks are frozen and the weights of the last block can be modified. We take the exit of the 4th last layer starting from the last layer. This layer corresponds to the last layer before the classification layers. The outputs of this layer are the characteristics of the image. Then we add a Dense layer (10, activation="softmax") for the prediction of our 10 classes (0,1,...,9). The semi-supervised network is thus built. 
 
 # Data
 The data at our disposal are MNIST images containing 70000 images of which 60000 are for training and 10000 for testing. For the work required, only 100 images with labels are to be taken and the rest, 59900 images without labels. For the basic network (the one that predicts the rotations), we took 80% of the 59900 for training and 20% for validation. 
 
 ## "BaseLine" network
 For the "BaseLine" network, we built a supervised network that has the same architecture as the previous semi-supervised network and trained it to recognise semantic features and to predict image classes. The classes here being the 0,1,2,3,4,5,6,7,8,9. To train this network, we used the 100 images we initially took from the 60,000 train images and left the other 5,9900 images aside. We did not apply here any geometric transformation (rotation) to the data. We then tested the network on the test dataset and compared its performance with that of the semi-supervised network.  
 
 ## Result
 Once the network was built according to the indicated method, we obtained an overall performance of 99.53% for the basic network, 86.48% for the semi-supervised network and 11% for the "BaseLine" network. In view of these results, we can say that the combined use of supervised and unsupervised learning techniques improves the performance of the network.
