# 基本概念

1. **神经网络（Neural Networks）**：这是深度学习的基础，包含输入层、隐藏层和输出层。每层都包含许多神经元，每个神经元都有权重和偏置，通过激活函数进行非线性转换。
2. **反向传播（Backpropagation）**：这是神经网络学习的主要算法，它通过计算目标函数关于权重的梯度，然后按梯度的反方向更新权重。
3. **激活函数（Activation Functions）**：这些函数用于引入非线性因素，使得神经网络可以学习更复杂的模式。常见的有ReLU、sigmoid和tanh等。
4. **损失函数（Loss Functions）**：这些函数用于评估模型的预测结果与真实值之间的差距。常见的有均方误差、交叉熵等。
5. **优化器（Optimizers）**：这些算法用于更新网络的权重和偏置以最小化损失函数。常见的有SGD、Adam和RMSprop等。
6. **卷积神经网络（Convolution Neural Networks, CNNs）**：这是一种特别适合处理图像数据的神经网络。通过卷积层、池化层和全连接层，CNN能够有效地提取图像的局部特征和全局特征。
7. **递归神经网络（Recurrent Neural Networks, RNNs）**：这是一种特别适合处理序列数据的神经网络，通过保存前一状态的信息，RNN可以处理具有时间依赖性的数据。
8. **长短期记忆（Long Short-Term Memory, LSTM）**：是一种特殊的RNN，设计用来避免传统RNN的长期依赖问题。
9. **变压器（Transformer）**：这是一种在自然语言处理中非常流行的模型，它使用自注意力机制（Self-Attention）处理序列数据，解决了RNN计算复杂性高和无法并行化的问题。BERT和GPT等模型都基于此。
10. **生成对抗网络（Generative Adversarial Networks, GANs）**：这是一种可以生成新数据的网络，由两部分组成：生成器和判别器。生成器尝试生成尽可能真实的假数据，而判别器的目标是尽可能分辨出真实数据和假数据。
11. **目标检测（Object detection）**：这是计算机视觉的一个重要任务，目标是找出图像中所有目标的位置和类别。YOLO（You Only Look Once）和SSD（Single Shot MultiBox Detector）是两种流行的目标检测算法。

目标检测算法:

- IOU(Intersection over Union):用于衡量预测框和真值框的重合程度,值越大表示预测越准确。
- NMS(Non-Maximum Suppression):去除重复的预测框,仅保留概率最大的预测框。
- Anchor:预先定义的用于匹配真值框的默认框,通常有不同尺度和宽高比。

分割算法:

- mIoU(Mean Intersection over Union):用于衡量分割结果的准确性,对每个类别单独计算IoU,然后取平均。

NLP算法:

- Transformer:利用Attention机制的编码器-解码器结构,不依赖RNN,更好的捕获全局依赖关系。
- BERT:双向transformer,通过Masked LM和Next Sentence Prediction任务进行预训练,可fine-tune到下游任务。

度量标准:

- Precision/Recall:预测结果的准确率和召回率。
- PR曲线:Precision-Recall曲线,度量各阈值下的P和R。
- mAP(Mean Average Precision):对不同召回率下的平均精度进行均值,度量目标检测的性能。

损失函数:

- CE(Cross-Entropy Loss):常用于分类问题,衡量预测概率分布和真实分布的差异。
- Focal Loss:解决分类数据不均衡问题,降低易分类样本的损失权重。

优化方法:

- SGD(Stochastic Gradient Descent):随机梯度下降,每次仅使用一个样本进行参数更新。
- Adam:自适应学习率的优化算法,结合了Momentum和RMSProp。

