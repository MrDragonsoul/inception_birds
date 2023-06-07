# Inception Birds
Kaggle competition notebook using an inceptionnet based model for transfer learning to perform bird classification.

![](https://github.com/MrDragonsoul/inception_birds/assets/45057669/b085ce60-3bb9-4aa1-9f05-480b3d2a34a8)

Sorry about the cutoff, had to trim to under 10MB


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
The task was the Kaggle bird classification competition hosted by the class. Given an image of a bird, identify which of 555 different bird species and maturity classifications the image is.
### Datasets
I used the provided bird image dataset, and implictly Imagenet's challenge dataset.

## Previous Work
I used [Inception_V3](https://pytorch.org/hub/pytorch_vision_inception_v3/), which uses the google inception net architecture in a more modern iteration, pretrained on Imagenet reporting a 22.55% top 1 error.

## My Approach
Taking the inception net as a basepoint, I chopped off the end classifier for image net and put in a linear network to instead classify to 555 categories. I then started training the network, using a preprocess of resizing to 299, then random padding cropping and horizontal flips after sizing the image and then applying the normaliztion the inception net architecture expects.

The training process was long, mostly consisting of attempting different mini-nets and training leveles over epochs of training and then seeing the training accuracy (or the test accuracy, because running the notebook as a submission was much easier on my computer). I attempted a range of strategies, like making the classifier more interesting, leaving validation data out to allow more fine tuning without overfitting, and swapping the pretrained model to see how they comapre (in preparation for an ensemble model), but the model that scored the best was a very simple classifier off the back of the pretrained, with just a few epochs of training to avoid overfitting. With the one for one replacement, I was able to replicate InceptionNet's T1 error almost exactly.

## Model Demo
<p align="center">
<iframe
	src="https://bricecm-inception-birds.hf.space"
	frameborder="0"
	width="850"
	height="450"
></iframe></p>
![Hugging face space](https://huggingface.co/spaces/bricecm/inception_birds)

## Discussion
### Problems
I ran into a variety of technical issues, but one of the main issues I encountered was the difficulty of setting up the training data into a validation set in the efficient LOOVC setup, as pytorch dataloaders aren't set up for that which means I had to give up training data for the validation, which ended up not making it in the best model. I also encounterd RAM issues on the more interesting setups I attempted, mainly for ensamblage. Becasue InceptionV3 is so large, it peaked my RAM allocation anytime I tried to use it with anything else. Additionally, the models I was trying to compare it against, like MEAL v2, were too large for the RAM allocation even by themselves which was a non-starter.
### Next Steps
With more time to work on the model, I'd like to actually get an ensemble model working (because they interest me, but also because they're greater than their parts). I would have to use less tanky models as my constituents, but I think if I could cycle what's in ram and train the constiuents individually first it could work. Another thing I'd like to do is work a bit more on data augmentation, seeing how modifying the training data could bolster the training and eventual accuracy of the model.
### Approach Differences and Benefits
My approach isn't super different from standard transfer learning techniques. I allowed the pretrained to be affected by the final classification training, which made it less general and probably contributed to my overfitting problems while increasing training, and while I tried a bunch of techniques, the model that performed the best ended up being a very standard re-decoder, finetuned by me but not outside standard practice. 
