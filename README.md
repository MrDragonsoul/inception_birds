# Inception Birds
Kaggle competition notebook using an inceptionnet based model for transfer learning to perform bird classification.


<!--     Problem description
    Previous work (including what you used for your method i.e. pretrained models)
    Your approach
    Datasets
    Results
    Discussion
        What problems did you encounter?
        Are there next steps you would take if you kept working on the project?
        How does your approach differ from others? Was that beneficial?
 -->
## Problem Description
The task was the Kaggle bird classification competition hosted by the class. Given an image of a bird, identify which of 555 different bird specie and age classifications the image is.
### Datasets
I used the provided bird image dataset, and implictly Imagenet's challenge dataset.

## Previous Work
I used [Inception_V3](https://pytorch.org/hub/pytorch_vision_inception_v3/), which uses the google inception net architecture in a more modern iteration, pretrained on Imagenet reporting a 22.55% top 1 error.

## My Approach
Taking the inception net as a basepoint, I chopped off the end classifier for image net and put in a short network to instead classify to 555 categories. I then started training the network, using a preprocess of random padding cropping and horizontal flips after sizing the image and then applying the normaliztion the inception net architecture expects.

The training process was long, mostly consisting of attempting different mini-nets over epochs of training and then seeing the training accuracy (or the test accuracy, because running the notebook as a submission was much easier on my computer).

## Results
### Model Demo? Can I do that?

## Discussion
### Problems
### Next Steps
### Approach Differences and Benefits
