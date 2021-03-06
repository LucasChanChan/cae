# Tensorflow Convolutional Auto-Encoder
This is an implementation of Stacked What-Where Auto Encoder in Tensorflow.
### Adjusting Layers  
Layer format is like the following: ```(16)5c-(32)3c-2p```, in which ```(16)5c``` denotes convolution layer with 16 feature maps
while kernel size being set to 5. ```2p``` denotes 2 × 2 pooling layer.  
### Auto-Encoder
Encoder is formed using the given layer structure. Decoder is formed using the inverse of given structure.
Note that pooling layers are converted to ```max_unpooling``` using the ```argmax``` of the pooling 
layer in the encoder. If pooling layer is not available in an encoding layer, decoder does not unpool. After unpooling -if exists- 
a new convolution layer is applied in the decoder -not deconvolution-.  

L2 losses between corresponding layers of encoder and decoder is called middle error. Recosntruction and these
errors are added to get the total loss. Gradient descent is used for backpropogation.  

```train_classifier.py``` trains a Linear SVM and saves the embeddings of the previously trained Autoencoder. To train the Autoencoder you should use ```train_autoencoder.py```. Output directory in ```train_classifier``` is the output directory where your Autoencoder is saved (Naming could have been better). Therefore, this model do not include the softmax layer in the network as discussed in the reference so the ```-fc``` parameter given while traning is not connected to a classifier but it is a bottleneck between encoder and decoder.  

I have managed to obtain good reconstructions with this code. Classification (SVM) works well on MNIST and Fashion MNIST but not that well on CIFAR-10 dataset.

For details see the reference.  

**Reference:** https://arxiv.org/pdf/1506.02351.pdf
