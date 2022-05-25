# Classify Leveas

- 基于 resnet 只做简单的数据增强，训练集和验证集为 5:5，可达到的精度是 81.5%

- 算法经过优化后，精度可达 94.5%

### 优化内容

1. 数据增强，训练集占比 0.5
   
   > acc 达 81.5%
   > 
   > 其中，数据增强：随机水平翻转 / 随机垂直翻转 / 随机裁剪
   > 
   > 整个数据集为 18k，即训练集为 9K

2. 训练集占比调整： 0.5 $\to$ 0.8
   
   > acc 升至 88.1%

3. 优化器调整：sgd $\to$ Adam
   
   > acc 再升至 90.2%

4. 学习率降低：1e3  $\to$ 1e4
   
   > acc 再升至 94.5%

### 训练环境

- colab pro

- 框架：PyTorch

竞赛：[Classify Leaves | Kaggle](https://www.kaggle.com/c/classify-leaves)

参考：[simple resnet baseline | Kaggle](https://www.kaggle.com/code/nekokiku/simple-resnet-baseline)

### 坑

- resnet18 + weight decay 的训练速度很慢
  
  > train acc 85% 左右，就很慢了，20 epochs ，train acc 只提升 2 各点，比没有 weight decay 的 resnet18 的提升慢很多
  > 
  > 分析：resnet18 本身的训练精度可达到 99%，所以模型容量是够大的。应该是 weight decay 限制了 w 的取值范围，导致 resnet18 的模型容量变得不够大，则训练集的精度提升就很慢了
