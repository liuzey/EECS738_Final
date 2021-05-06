# EECS738_Final
EECS 738 Final Group Project - Feasibility of backdoor attacks against transfer learning without domain knowledge

## Introduction
In this project, we explore the possibility of backdoor attacks on transfer learning without domain knowledge. Specifically, we aim at attack the target domain by polluting source domain. The transfer learning here refers to the basic model transfer method, which transfers knwoledge by borrowing parameters of the pre-trained feature extractor and fine-tune the last layers. Note transfer learning here is not related with any training losses or metrics using domain adaptation/generalization. 

Technically, we apply the simple trigger in Badnets [\[1\]](https://arxiv.org/pdf/1708.06733.pdf?source=post_page---------------------------) as black-and-white blocks, and adopt two training strategies as compared in TrojanNN [\[2\]](https://docs.lib.purdue.edu/cgi/viewcontent.cgi?article=2782&context=cstech). The first attack strategy is to finetune the model using polluted data, while the second one is to train the polluted model from scratch. We explore the feasibility of attacks on target domain using only source domain knowledge, and compare the influence of several attack vectors, which includes the size of trigger, the label space and strategies. Note that different from CCS paper [\[3\]](https://doi.org/10.1145/3319535.3354209), our attack doesn't require target domain data, and we also don't have manipulation over training process (\[3\] introduces a specialized loss function on features which requires the attacker to be the model producer and publisher. This is a strong assumption on attacker's ability and accessibility. Here we assume that the attacker is only capable of inserting malcious data, which aligns with \[1\].) 

As the attacker has no knowledge of the target domain, targeted attacks aiming at specific labels should be rather difficult and complex. In this project, we only perform untargeted attacks. Whenever an image correctly labelled by the model in a transfer phase gets misclassified after a trigger is attached, it is believed to be a successful attack. This may not be as fancy as targeted attacks, but follows 'no free lunch' principle in a tradeoff between attacker's ability and goals.

## Datasets

## Environment Setup

## Baseline Model

## Atk against Transfer Learning

## Notes
* For any further discussion, feel free to contact me.

## Reference
* Gu T, Dolan-Gavitt B, Garg S. Badnets: Identifying vulnerabilities in the machine learning model supply chain\[J\]. arXiv preprint arXiv:1708.06733, 2017.
* Liu Y, Ma S, Aafer Y, et al. Trojaning attack on neural networks\[J\]. 2017.
* Yao Y, Li H, Zheng H, et al. Latent backdoor attacks on deep neural networks\[C\]//Proceedings of the 2019 ACM SIGSAC Conference on Computer and Communications Security. 2019: 2041-2055.
