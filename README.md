# EECS738_Final
EECS 738 Final Group Project - Feasibility of backdoor attacks against transfer learning without domain knowledge

## Introduction
In this project, we explore the possibility of backdoor attacks on transfer learning without domain knowledge. Specifically, we aim at attack the target domain by polluting source domain. The transfer learning here refers to the basic model transfer method, which transfers knwoledge by borrowing parameters of the pre-trained feature extractor and fine-tune the last layers. Note transfer learning here is not related with any training losses or metrics using domain adaptation/generalization. 

Technically, we apply the simple trigger in Badnets [\[1\]](https://arxiv.org/pdf/1708.06733.pdf?source=post_page---------------------------) as black-and-white blocks, and adopt two training strategies as compared in TrojanNN [\[2\]](https://docs.lib.purdue.edu/cgi/viewcontent.cgi?article=2782&context=cstech). The first attack strategy is to finetune the model using polluted data, while the second one is to train the polluted model from scratch. We explore the feasibility of attacks on target domain using only source domain knowledge, and compare the influence of several attack vectors, which includes the size of trigger, the label space and strategies. Note that different from CCS paper [\[3\]](https://doi.org/10.1145/3319535.3354209), our attack doesn't require target domain data, and we also don't have manipulation over training process (\[3\] introduces a specialized loss function on features which requires the attacker to be the model producer and publisher. This is a strong assumption on attacker's ability and accessibility. Here we assume that the attacker is only capable of inserting malcious data, which aligns with \[1\].) 

As the attacker has no knowledge of the target domain, targeted attacks aiming at specific labels should be rather difficult and complex. In this project, we only perform untargeted attacks. Whenever an image correctly labelled by the model in a transfer phase gets misclassified after a trigger is attached, it is believed to be a successful attack. This may not be as fancy as targeted attacks, but follows 'no free lunch' principle in a tradeoff between attacker's ability and goals.

## Transfer Learning

## Backdoor Attacks

## Datasets
**Note that MNIST, GTSRB and CIFAR datasets are not needed for manual download as their resources are included in torchvision package and can be downloaded automatically. MNISTM can be downloaded [here](https://drive.google.com/drive/folders/0B_tExHiYS-0vR2dNZEU4NGlSSW8).**
* [Modified National Institute of Standards and Technology database (MNIST)](http://yann.lecun.com/exdb/mnist/). This is possibly one of the most commonly-used and simplest dataset in image tasks in machine learning, which combines with different images of hand-written digits. The sizes of training dataset and testing dataset are 60,000 and 10,000 each. Though the attached webpage link seems not to be working, the dataset can be directly accessed by package [python-mnist](https://github.com/sorki/python-mnist). Images and grey-scale with a size of 28\*28 each. Ten labels in total range from 0, 1, 2... to 9. 
* [The German Traffic Sign Recognition Benchmark (GTSRB)](https://benchmark.ini.rub.de/gtsrb_dataset.html). This is a more challenging dataset with images of traffic signs captured in real street views. Each image contains exactly one traffic sign, usually located right at the middle. There are 43 labels in total, representing different types of traffic signs, and more than 50,000 samples. Recognition of these signs is much more difficult and practically significant, as many of the signs have similar shapes and colors. 
* [MNIST-M](http://yaroslav.ganin.net/): Colorful MNIST handwritten digits images with diverse background. This serves as a close domain to MNIST in this project. 
* [CIFAR](https://www.cs.toronto.edu/~kriz/cifar.html): This dataset consists of 60000 32x32 colour images in 10 classes, with 6000 images per class. There are 50000 training images and 10000 test images. These images are ten categories of different objects in real-world scenes, which includes airplanes, automobiles, birds, cats, deer, dogs, frogs, horses, ships and trucks. This is usually considered as the most tough task among these four listed.

## Environment Setup

## Baseline Model

## Atk against Transfer Learning

## Notes
* For any further discussion, feel free to contact me.

## Reference
* Gu T, Dolan-Gavitt B, Garg S. Badnets: Identifying vulnerabilities in the machine learning model supply chain\[J\]. arXiv preprint arXiv:1708.06733, 2017.
* Liu Y, Ma S, Aafer Y, et al. Trojaning attack on neural networks\[J\]. 2017.
* Yao Y, Li H, Zheng H, et al. Latent backdoor attacks on deep neural networks\[C\]//Proceedings of the 2019 ACM SIGSAC Conference on Computer and Communications Security. 2019: 2041-2055.
