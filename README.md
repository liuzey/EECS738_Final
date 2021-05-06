# EECS738_Final
EECS 738 Final Group Project - Feasibility of backdoor attacks against transfer learning without domain knowledge

## Introduction
In this project, we explore the possibility of backdoor attacks on transfer learning without domain knowledge. Specifically, we aim at attack the target domain by polluting source domain. The transfer learning here refers to the basic model transfer method, which transfers knwoledge by borrowing parameters of the pre-trained feature extractor and fine-tune the last layers. Note transfer learning here is not related with any training losses or metrics using domain adaptation/generalization. 

Technically, we apply the simple trigger in Badnets [\[1\]](https://arxiv.org/pdf/1708.06733.pdf?source=post_page---------------------------) as black-and-white blocks, and adopt two training strategies as compared in TrojanNN [\[2\]](https://docs.lib.purdue.edu/cgi/viewcontent.cgi?article=2782&context=cstech). The first attack strategy is to finetune the model using polluted data, while the second one is to train the polluted model from scratch. We explore the feasibility of attacks on target domain using only source domain knowledge, and compare the influence of several attack vectors, which includes the size of trigger, the label space and strategies. Note that different from CCS paper [\[3\]](https://doi.org/10.1145/3319535.3354209), our attack doesn't require target domain data, and we also don't have manipulation over training process (\[3\] introduces a specialized loss function on features which requires the attacker to be the model producer and publisher. This is a strong assumption on attacker's ability and accessibility. Here we assume that the attacker is only capable of inserting malcious data, which aligns with \[1\].) 

As the attacker has no knowledge of the target domain, targeted attacks aiming at specific labels should be rather difficult and complex. In this project, we only perform untargeted attacks. Whenever an image correctly labelled by the model in a transfer phase gets misclassified after a trigger is attached, it is believed to be a successful attack. This may not be as fancy as targeted attacks, but follows 'no free lunch' principle in a tradeoff between attacker's ability and goals.

## Transfer Learning

## Backdoor Attacks

## Datasets
**Note that MNISTand CIFAR datasets are not needed for manual download as their resources are included in torchvision package and can be downloaded automatically. GTSRB and MNISTM should be downloaded manually. MNISTM can be downloaded [here](https://drive.google.com/drive/folders/0B_tExHiYS-0vR2dNZEU4NGlSSW8).**
* [Modified National Institute of Standards and Technology database (MNIST)](http://yann.lecun.com/exdb/mnist/). This is possibly one of the most commonly-used and simplest dataset in image tasks in machine learning, which combines with different images of hand-written digits. The sizes of training dataset and testing dataset are 60,000 and 10,000 each. Though the attached webpage link seems not to be working, the dataset can be directly accessed by package [python-mnist](https://github.com/sorki/python-mnist). Images and grey-scale with a size of 28\*28 each. Ten labels in total range from 0, 1, 2... to 9. 
* [The German Traffic Sign Recognition Benchmark (GTSRB)](https://benchmark.ini.rub.de/gtsrb_dataset.html). This is a more challenging dataset with images of traffic signs captured in real street views. Each image contains exactly one traffic sign, usually located right at the middle. There are 43 labels in total, representing different types of traffic signs, and more than 50,000 samples. Recognition of these signs is much more difficult and practically significant, as many of the signs have similar shapes and colors. 
* [MNIST-M](http://yaroslav.ganin.net/): Colored MNIST handwritten digits images with diverse background. This serves as a close but 'advanced' domain to MNIST in this project. 
* [CIFAR](https://www.cs.toronto.edu/~kriz/cifar.html): This dataset consists of 60000 32x32 colour images in 10 classes, with 6000 images per class. There are 50000 training images and 10000 test images. These images are ten categories of different objects in real-world scenes, which includes airplanes, automobiles, birds, cats, deer, dogs, frogs, horses, ships and trucks. This is usually considered as the most tough task among these four listed.

## Setup
### Environment
* Python 3.9
* MacOS or Linux

### Package
* Recommend setting up a virtual environment. Different versions of packages may cause unexpected failures.
* Install packages in **requirements.txt**.
```bash
pip install -r requirements.txt
``` 
## Model Structure.
The model adopted in this paper is a simple CNN with five convolutional layer, one intermediate linear layer and one final linear layer. It shows sufficient performance on a basic study on theese four datasets. More complex models like VGG and ResNet can be studied in exactly the same principles. The influence of model structure remains as futrue work.

| CNN  |
| :-------------: |
| Conv1(channels=32, stride=(1, 1), padding=(0, 0)), BatchNorm(32), Maxpooling(2,2), ReLU |
| Conv2(channels=64, stride=(2, 2), padding=(1, 1)) |
| Conv3(channels=64, stride=(1, 1), padding=(0, 0)), BatchNorm(64), Dropout, Maxpooling(2,2), ReLU |
| Conv4(channels=128, stride=(2, 2), padding=(1, 1)) |
| Conv5(channels=128, stride=(1, 1), padding=(0, 0)), BatchNorm(128), Dropout, Maxpooling(2,2), ReLU |
| FC1(128\*2\*2, 100), BatchNorm(100), ReLU |
| FC2(100, num_class) |

The performance (accuracy) of this model after training for 100 iterations is shown as follows.

| Datasets    | MNIST | MNISTM | CIFAR10 | GTSRB |
| :-------------: |:-------------: |:-------------: |:-------------: |:-------------: |
| Accuracy(%) | 99.66 | 98.65  | 98.84   | 80.15 |

## Baseline Model
In this baseline attack, no transfer is present. We reimplement BadNets on all datasets and show some preliminary results.

### Paras

* If not specified 
### Usage

### Results: Trigger Size

### Results: Poison Ratio

### Results: Strategies
In \[2\], a from-scratch strategy is better than the tuning strategy as the from-scratch strategy is more resilient to mitigation using fine-tuning. However, we don't concentrate on robustness against defenses in this project. We are interested in whether the strategy helps trigger to survive across domains. Theoretically, tuning on a well-trained model tend to embed trigger by creating a individual cluster for trigger in the same label name, which means that images stand out in feature space when patched with triggers. However, from-scratch tend to combines the images with triggers with images in the target label, which means combining a distribution in boundary division. This makes the tuning more fragile to unlearning. However, it is likely that tuning will outperforms from-scratch as it creates a individual branch in feature extraction, which will be more useful when domain changes and boundary shuffles. We will verify this guessing in later part. In baseline model, we need to do preliminary experiments to show that these two strategies both show great performance and same time overhead and negative effects on model functioning. This is a important basis for future analysis. 

Here results are shown when adopting two different strategies, **s** for from-scratch strategy, and **t** for tuning strategy. Degrade in accuracy means model performance over clean data after embedding a backdoor. For tuning strategy, the model is trained over poisoned data for 10 iterations. For from-scratch strategy, the model is trained for 110 iterations aligned with tuning strategy (plus clean training).

| Datasets    | MNIST(**s**\\**t**) | MNISTM(**s**\\**t**) | CIFAR10(**s**\\**t**) | GTSRB(**s**\\**t**) |
| :-------------: |:-------------: |:-------------: |:-------------: |:-------------: |
| Atk Suc Rate(%) | 99.98\99.99 | 99.86\99.98  | 100.00\100.00   | 99.92\99.71 |
| Acc Degrade(%)  | 0.18\0.17 | 0.07\0.13  | 0.06\0.16    | 0.08\0.04 |


## Atk against Transfer Learning

## Notes
* In some cases, it shows that the transferability of trigger is stronger when two domains are close, e.g. between CIFAR and GTSRB than CIFAR and MNISTM. This follows a rough intuition. However, this is not always the situation. Also, domain difference are not quantified in this project. We remain this as our future work.
* For any further discussion, feel free to contact me.

## Reference
* Gu T, Dolan-Gavitt B, Garg S. Badnets: Identifying vulnerabilities in the machine learning model supply chain\[J\]. arXiv preprint arXiv:1708.06733, 2017.
* Liu Y, Ma S, Aafer Y, et al. Trojaning attack on neural networks\[J\]. 2017.
* Yao Y, Li H, Zheng H, et al. Latent backdoor attacks on deep neural networks\[C\]//Proceedings of the 2019 ACM SIGSAC Conference on Computer and Communications Security. 2019: 2041-2055.
