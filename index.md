Source code is in this [jupyter notebook](https://colab.research.google.com/drive/1gLUj6_ho7ZafWqwCv2hYjHO5JGHJwfD2#scrollTo=uBEH1kB0r2np) as well as on [Github](https://github.com/saadhassan99/cse455-FinalProject/blob/main/CSE455_Final_Project.ipynb)

## Project Video

<p align="center">
<iframe width="560" height="315" src="https://www.youtube.com/embed/EDeUqlfrY30" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>

## Abstract

For this project, I explored a few pretrained segmentation models to judge their performed on a challenging dataset of identifying whale flukes. The purpose of the project was to help with convervation efforts of known whales as well as identify new whale species. I used transfer learning, a process that involves taking the learnings of pretrained few state of the art models and repurpose their learning to the problem at hand by attaching linear classifiers of our own and compare the results of the models qualitavelivey. At the end, i discussed, a few challenges and roadmap for future work.  

## Problem and Motivation
The main goal was to identify whether the given photo of the whale fluke belongs to one of the 5004 known individual of
whales or, it is a `new_whale` never been seen before.

![download](https://user-images.githubusercontent.com/39425395/158084537-432939c7-6b1f-4da6-998f-cbb74b459f48.png)

The puzzling aspect of this competition was the huge class imbalance. For more than 2000 of the classes there was **only one** training sample, which made it hard to use the classification approach out of the box. Whats more, it was an important part of the competition to classify, whether the whale is new or not, which turned out to be quite non-trivial.

![image](https://user-images.githubusercontent.com/39425395/158084611-b99375cd-b57d-408a-8ce2-177e01bf6622.png)

The motivation behind this challenge is to help scientists to analyze and meticulously log whale pod dynamics and movement. Automating the process of Identifying whales from surveillance systems will save a lot of time and effort that goes into manually doing this process, and perhaps discover new patterns that were not visible to the naked eye.

## Data set

For this challenge, I will use Happywhale’s database provided by kaggle of over 25,000 images and over 7000 images for testing, gathered from research institutions and public contributors. The dataset is already partitioned into a train and test folders.

Some code snippets have been borrowed from tutorials shown in class.

## Models

I mainly used two classification models for this challenge; a Pretrained ResNet152 and a Pretrained DenseNet121. and then a basic CNN from scratch just to see how it performs against the most widely industry used models.

1. ResNet was trained for 10 epochs with data augmentations. The images were resized to 256, 256, then were randomly cropped, rotated, and nomalized.

2. DensNet was trained for 2, 5 and 10 epochs. Same image transformations were used from above, but hyperparameter such as learning rate were tuned between epochs to see which one gets the best result. DenseNet connect layers together in a feed-forward manner, unlike traditional convolutional networks. DenseNet was also computationally pretty expensive to train.

3. The third model was BasicCNN that had 2 Convolutional layers, a drop out layer. and 2 Linear layers. The activation function was ReLU.

## Results

### BasicCNN

The Basic CNN performed the worst. I trained it for 10 epochs and it only got down to the loss of about 5.93.

![image](https://user-images.githubusercontent.com/39425395/158099067-cea36555-ff28-489b-90be-928d3820134c.png)

### ResNet152

ResNet152 performed really well on the training data but it failed to perform well on the test data. It acheived an accuracy of about 30% when submitted to kaggle. It was a sign of over fitting on the training data.

![image](https://user-images.githubusercontent.com/39425395/158100548-09c0caf6-ff54-4dba-8fd2-879465b7bc38.png)

### DenseNet121

I trained DenseNet121 with varying hyperparameters and fine tuning to prevent overfitting. This time I received a test accuracy of about 53% when submitted to kaggle before i ran out of GPU computation capacity. This was a 23% improvement over the ResNet121. 

![image](https://user-images.githubusercontent.com/39425395/158108336-c0bc0163-c358-441f-8525-533a6a2365e9.png)

## Future work

In this project, I gained a good understand of different CV models, what works, what doesnt work, choosing hyperparameters, etc. Although densenet performed better than Resnet, the resulted model is still not good enough to be used commercially. Future work will be to continue addressing the overfitting problem as well as discovering and understanding ways to work with data with huge imbalances. Overall, this project to me was a huge learning experience, and i will continue on this path even after this class.

## Discussion:

These CNN models take hours to train, and consumes a huge amount of computation resources and time. Therefore, finding the right set of hyperparamaters was a challenge. I relied on the knowledge and experiences from the class when we were building our CV library and chose learning rates and decay accordingly.

GPU capacity was also challenge, I ran out of Google colabs 12 hour time limit. so i had to migrate my code over to kaggle to use their gpus.

Future work will include researching how we can cut down computation time and speed up training. So we quickly experiment with different settings.
