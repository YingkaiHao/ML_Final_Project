# ML_Final_Project
The final project for machine learning for cyber security. Contributed by Yunyi Liao, Yingkai Hao and Xiangyu Lu.

## Structure of diractories

```
|____gtsrb-german-traffic-sign
	|____Meta-----------Put Meta dataset in this folder
	|____Test-----------Put Test dataset in this folder
	|____Train----------Put Train dataset in this folder
	|____Meta.csv
	|____Test.csv
	|____Train.csv
|____GRSRB defense.ipynb
|____GRSRB defense.pdf
|____GRSRB.ipynb
|____GRSRB.pdf
```



## How to run our code

Our code separates into two parts. Attack and Defense.

1. The backdoor attack achieves in GTSRB.ipynb.
2. The defense achieves in GTSRB defense.ipynb.

Put all datasets in the file Meta, Test and Train folds.

System enviornment:

1. Python 3.8.3
2. Numpy 1.23.4
3. Tensorflow-gpu 2.5.0
4. Opencv 4.5.1
5. Idx2nump 1.2.3

## Conclusion

<img src="/Users/haoyingkai/Library/Application Support/typora-user-images/image-20221219174120399.png" alt="image-20221219174120399" style="zoom:50%;" />

In this paper, we reproduce the FTorjan attack using both CIFAR10 and GTSRB. We found that the attack success rate on GRSRB is up to 100%. Then, we decided to do a pruning defense for this attack. The result is sufficient to show that, by using pruning defense on the backdoor attack through the frequency domain, the attack success rate decreased from 100% to 26%, which means it successfully mitigates the backdoors. Therefore, we conclude that for this specific attack-FTorjan, pruning defense provides strong protection. 

Currently, we only use pruning defense against the FTorjan attack. However, we still feel that we could extend more in the future. According to our analysis above, we discover that although the attack success rate drops significantly to 26%, the clean validation accuracy also drops to 65%. The reason why the clean validation accuracy also drops this much is the unique channel activations feature in the last pooling layer. We found that the activeness of each channel is almost the same, which means no matter which channel we prune, the overall impact on the clean validation accuracy is almost the same. Therefore, we found that as we start pruning, the clean validation accuracy drops slowly. However, these channels we pruned did not happen to be the ones active in the backdoor attack model. And, when we start pruning the relative active channels in the backdoor attack model, the clean validation accuracy already drops too much. 

In order to solve this problem, we thought we could produce the pruning backed on the activation level in the backdoor attack. We could prune channels from most active in the backdoor attack model to least active. Since all channels' activeness on the clean model is almost the same and we prune most active channels first, the clean validation accuracy will drop slowly, while the attack success rate will decrease significantly. 
