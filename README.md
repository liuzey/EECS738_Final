# EECS738_Final
EECS 738 Final Group Project - Feasibility of backdoor attacks against transfer learning without domain knowledge

## Introduction
In this project, we explore the possibility of backdoor attacks on transfer learning without domain knowledge. Specifically, we aim at attack the target domain by polluting source domain. The transfer learning here refers to the basic model transfer method, which transfers knwoledge by borrowing parameters of the pre-trained feature extractor and fine-tune the last layers. Note transfer learning here is not related with any training losses or metrics using domain adaptation/generalization. Technically, we apply the simple trigger in Badnets [1]() as black-and-white blocks, and adopt two training strategies as compared in TrojanNN [](). The first attack strategy is to finetune the model using polluted data, while the second one is to train the polluted model from scratch. We explore the feasibility of attacks on target domain using only source domain knowledge, and compare the influence of several attack vectors, which includes the size of trigger, the label space and strategies. Note that different from CCS paper [3](), our attack doesn't require target domain data, and we also don't have manipulation over training process (\[3\] introduces a specialized loss function on features which requires the attacker to be a model producer and publisher. We assume that the attacker is only capable of polluting data.) As the attacker has no knowledge of the target domain, targeted attacks aiming at specific labels should be very difficult and complex. In this project, we only perform untargeted attacks. Whenever an image is 

## Datasets

## Environment Setup

## Baseline Model

## Atk against Transfer Learning

## Notes
* For any further discussion, feel free to contact me.

## Reference
