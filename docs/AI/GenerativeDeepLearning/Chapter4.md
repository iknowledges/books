# Chapter 4. Generative Adversarial Networks

## Introduction to GANs

A GAN is a battle between two adversaries, the generator and the discriminator. The generator tries to convert random noise into observations that look as if they have been sampled from the original dataset and the discriminator tries to predict whether an observation comes from the original dataset or is one of the generator’s forgeries.

## Your First GAN

### The Discriminator

The goal of the discriminator is to predict if an image is real or fake.

### The Generator

The input to the generator is a vector, usually drawn from a multivariate standard normal distribution. The output is an image of the same size as an image in the original training data.

The generator of a GAN fulfills exactly the same purpose as the decoder of a VAE: converting a vector in the latent space to an image.

- UPSAMPLING

In this GAN, we instead use the Keras Upsampling2D layer to double the width and height of the input tensor. This simply repeats each row and column of its input in order to double the size.

### Training the GAN

We can train the discriminator by creating a training set where some of the images are randomly selected real observations from the training set and some are outputs from the generator. The response would be 1 for the true images and 0 for the generated images. 

To train the generator, we must first connect it to the discriminator to create a Keras model that we can train. Specifically, we feed the output from the generator (a 28 × 28 × 1 image) into the discriminator so that the output from this combined model is the probability that the generated image is real, according to the discriminator.

The loss function is then just the binary cross-entropy loss between the output from the discriminator and the response vector of 1.

We must freeze the weights of the discriminator while we are training the combined model, so that only the generator’s weights are updated.

## GAN Challenges

### Oscillating Loss

Typically, there is some small oscillation of the loss between batches, but in the long term you should be looking for loss that stabilizes or gradually increases or decreases, rather than erratically fluctuating, to ensure your GAN converges and improves over time.

### Mode Collapse

Mode collapse occurs when the generator finds a small number of samples that fool the discriminator and therefore isn’t able to produce any examples other than this limited set. 

Suppose we train the generator over several batches without updating the discriminator in between. The generator would be inclined to find a single observation (also known as a mode) that always fools the discriminator and would start to map every point in the latent input space to this observation. This means that the gradient of the loss function collapses to near 0.

### Uninformative Loss

However, since the generator is only graded against the current discriminator and the discriminator is constantly improving, we cannot compare the loss function evaluated at different points in the training process.
