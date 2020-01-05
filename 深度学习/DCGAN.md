## DCGAN
深度卷积生成对抗网络（Deep Convolutional Generative Adversarial Network）结合了深度卷积神经网络和GAN,并对GAN进行了扩展。

- 用不同步长的卷积层替换所有Pooling层。
- 在D和G中均使用BatchNorm层。
- 在G网络中,除最后一层使用tanh以外,其余层均使用ReLU作为激活函数。
- D网络均使用LeakyRelu作为激活函数。