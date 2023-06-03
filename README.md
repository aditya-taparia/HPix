# Satellite Image to Vector Map Translation with HPix Architecture
In this project, I have build and train a novel conditional generative adversarial network (cGAN) called HPix that learns a mapping from input images to output images. This repository contains the implementaion, training and testing code for this network.

## Dataset
This network is trained on [maps dataset](http://efrosgans.eecs.berkeley.edu/pix2pix/datasets/maps.tar.gz) provided by Pix2Pix authors. The dataset contains 1096 paired satellite and vector tile map images for training and 1098 paired satellite and vector tile map images for testing. Size of each image is 600x600 pixels.

For preprocessing, we have resized the images to 256x256 pixels. Then we also have applied random jittering for training. The images are then normalized to the range [-1, 1] for both training and testing.

## Model
This architecture comprises two GAN frameworks, one at global level and other at local level, together forming a hierarchical model, as shown in figure below.

![HPix Architecture](./images/HierarchicalPix%20Architecture.jpg)

### Global Generator
The global generator is an architecture with nested skip connections, inspired from Unet++ architecture. The following figure shows the architecture of global generator.

![Global Generator](./images/HierarchicalPix%20Global%20Generator.jpg)

The following figure explains the components used in the global generator. They are architecture of - (a) Encoder, (b) Decoder, and (c) Transition Block. These components are also used in the local generator.

![Global Components](./images/Global%20Generator%20Components.jpg)

### Local Generator
The local generator of HPix is a modified architecture of Pix2Pix which takes two inputs, a generated output of the global generator and our original input (satellite image) and gives single output. The following figure shows the architecture of local generator.

![Local Generator](./images/HierarchicalPix%20Local%20Generator.jpg)

### Local and Global Discriminator
The local and global discriminator are similar to the PatchGAN discriminator used in Pix2Pix. The following figure shows the architecture of the discriminator.

![Discriminator](./images/HierarchicalPix%20Global%20Discriminator.jpg)

The following figure displays the discriminator CNNBlock.

<center>
<img src="./images/Global%20Discriminator%20Components.jpg" width="50%" height="50%"/>
</center>

## Training Conditions
The model was trained on Kaggle platform for 200 epochs. The model was optimized using Adam optimizer with a learning rate of 0.0002 and beta1 and beta2 as 0.5 and 0.999 and the batch size was set to 1.

## Results
The following figure shows the comparision of our model with Pix2Pix and CycleGan on the test dataset.

![Comparing with different architectures](./images/comparison%20between%20different%20models.jpg)

## Pretrained Weights
The pretrained weights for this model can be downloaded from [here](https://www.kaggle.com/datasets/adityataparia/hpix-weights).