本项目采用Keras和Keras-bert实现文本多标签分类任务。

### 维护者

- jclian91

### 数据集

#### 2020语言与智能技术竞赛：事件抽取任务

本项目以 2020语言与智能技术竞赛：事件抽取任务 中的数据作为多分类标签的样例数据，借助多标签分类模型来解决。

### 代码结构

```
.
├── chinese_L-12_H-768_A-12（BERT中文预训练模型）
│   ├── bert_config.json
│   ├── bert_model.ckpt.data-00000-of-00001
│   ├── bert_model.ckpt.index
│   ├── bert_model.ckpt.meta
│   └── vocab.txt
├── data（数据集）
├── label.json（类别词典，生成文件）
├── model_evaluate.py（模型评估脚本）
├── model_predict.py（模型预测脚本）
├── model_train.py（模型训练脚本）
└── requirements.txt
```
### 模型结构

```
__________________________________________________________________________________________________
Layer (type)                    Output Shape         Param #     Connected to                     
==================================================================================================
input_1 (InputLayer)            (None, None)         0                                            
__________________________________________________________________________________________________
input_2 (InputLayer)            (None, None)         0                                            
__________________________________________________________________________________________________
model_2 (Model)                 (None, None, 768)    101677056   input_1[0][0]                    
                                                                 input_2[0][0]                    
__________________________________________________________________________________________________
lambda_1 (Lambda)               (None, 768)          0           model_2[1][0]                    
__________________________________________________________________________________________________
dense_1 (Dense)                 (None, 65)           49985       lambda_1[0][0]                   
==================================================================================================
Total params: 101,727,041
Trainable params: 101,727,041
Non-trainable params: 0
__________________________________________________________________________________________________
```

## 模型效果

#### 事件抽取任务数据集

- chinese_L-12_H-768_A-12

模型参数: batch_size = 8, maxlen = 256, epoch=10

使用chinese_L-12_H-768_A-12预训练模型，评估结果如下:

```
              precision    recall  f1-score   support

           0     1.0000    0.8947    0.9444        19
           1     0.8750    1.0000    0.9333        21
           2     0.9091    1.0000    0.9524        10
           3     1.0000    0.8537    0.9211        41
           4     0.9462    1.0000    0.9724        88
           5     1.0000    1.0000    1.0000         8
           6     0.9726    1.0000    0.9861        71
           7     1.0000    1.0000    1.0000         7
           8     0.8761    0.9340    0.9041       106
           9     1.0000    0.9000    0.9474        10
          10     0.9333    1.0000    0.9655        14
          11     1.0000    1.0000    1.0000         8
          12     0.8333    1.0000    0.9091         5
          13     0.8636    1.0000    0.9268        19
          14     1.0000    1.0000    1.0000        36
          15     0.8438    1.0000    0.9153        27
          16     0.9697    1.0000    0.9846        32
          17     1.0000    1.0000    1.0000        12
          18     1.0000    1.0000    1.0000        29
          19     0.8824    0.8571    0.8696        35
          20     0.9091    0.9091    0.9091        11
          21     1.0000    1.0000    1.0000         4
          22     0.6667    0.8000    0.7273         5
          23     1.0000    0.8889    0.9412         9
          24     0.8571    0.6667    0.7500         9
          25     0.9737    0.9867    0.9801       150
          26     1.0000    1.0000    1.0000        12
          27     0.9394    0.9688    0.9538        32
          28     0.8462    1.0000    0.9167        11
          29     0.8387    0.9286    0.8814        56
          30     0.9487    0.8605    0.9024        43
          31     0.9231    0.8000    0.8571        15
          32     1.0000    1.0000    1.0000        24
          33     1.0000    0.6250    0.7692         8
          34     1.0000    0.9375    0.9677        16
          35     0.8421    0.9697    0.9014        33
          36     0.8500    0.7727    0.8095        22
          37     0.9231    1.0000    0.9600        24
          38     0.9591    0.9906    0.9746       213
          39     0.9118    0.8857    0.8986        35
          40     1.0000    1.0000    1.0000         7
          41     1.0000    0.9000    0.9474        10
          42     0.8333    0.7692    0.8000        13
          43     0.8947    0.9444    0.9189        18
          44     0.9167    1.0000    0.9565        11
          45     1.0000    1.0000    1.0000        14
          46     0.9000    1.0000    0.9474         9
          47     1.0000    1.0000    1.0000         9
          48     0.7895    0.8333    0.8108        18
          49     0.9706    1.0000    0.9851        33
          50     1.0000    1.0000    1.0000         9
          51     1.0000    1.0000    1.0000         3
          52     0.9286    1.0000    0.9630        13
          53     1.0000    1.0000    1.0000        14
          54     0.8571    1.0000    0.9231         6
          55     1.0000    1.0000    1.0000        15
          56     0.8421    1.0000    0.9143        16
          57     1.0000    1.0000    1.0000        14
          58     0.9000    1.0000    0.9474         9
          59     1.0000    1.0000    1.0000        27
          60     0.8824    0.9375    0.9091        16
          61     0.7778    1.0000    0.8750        14
          62     1.0000    0.7500    0.8571         4
          63     1.0000    0.9375    0.9677        16
          64     0.9000    1.0000    0.9474         9

   micro avg     0.9341    0.9578    0.9458      1657
   macro avg     0.9336    0.9462    0.9370      1657
weighted avg     0.9367    0.9578    0.9456      1657
 samples avg     0.9520    0.9672    0.9531      1657

accuracy:  0.8985313751668892
hamming loss:  0.001869158878504673
```

- chinese_wwm_ext_L-12_H-768_A-12

模型参数: batch_size = 8, maxlen = 256, epoch=10

使用chinese_wwm_ext_L-12_H-768_A-12预训练模型，评估结果如下：

```
   micro avg     0.9403    0.9608    0.9504      1657
   macro avg     0.9322    0.9542    0.9404      1657
weighted avg     0.9446    0.9608    0.9510      1657
 samples avg     0.9598    0.9713    0.9595      1657

accuracy:  0.9092122830440588
hamming loss:  0.0017048372188559105
```

- chinese_roberta_wwm_large_ext_L-24_H-1024_A-16

模型参数: batch_size = 2, maxlen = 256, epoch=10

使用chinese_roberta_wwm_large_ext_L-24_H-1024_A-16预训练模型，评估结果如下：

```
   micro avg     0.9385    0.9584    0.9483      1657
   macro avg     0.9372    0.9482    0.9383      1657
weighted avg     0.9428    0.9584    0.9488      1657
 samples avg     0.9581    0.9700    0.9579      1657

accuracy:  0.9065420560747663
hamming loss:  0.001776727944952244
```

### 项目启动

1. 将BERT中文预训练模型chinese_L-12_H-768_A-12放在chinese_L-12_H-768_A-12文件夹下
2. 所需Python第三方模块参考requirements.txt文档
3. 自己需要分类的数据按照data/train.py的格式准备好
4. 调整模型参数，运行model_train.py进行模型训练
5. 运行model_evaluate.py进行模型评估
6. 运行model_predict.py对新文本进行评估