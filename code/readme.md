### 1. anaconda虚拟环境创建与激活

创建并激活一个anaconda的虚拟环境，你需要以下命令：

```python
conda create --name SRGAN_Pytorch python=3.9# 创建新环境
conda activate SRGAN_Pytorch# 激活SRGAN_Pytorch环境
```

### 2. 依赖库安装

1. pytorch（最新版即可）：

```python
pip3 install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu117
```

2. 安装其他库，执行如下命令即可：

```python
pip install torchvision # pytorch需要用到的数据处理库
pip install tensorboard_logger #为tensorflow训练可视化开发的，但是pytorch也可以用
pip install tqdm # 训练过程中的进度条打印
```

###  3.程序运行

1. 训练原始的SRGAN模型，其中`train_set`是训练数据集的相对路径：

```python
python train.py --train_set=data/train
```

2. 训练原始的SRWGAN-GP（WGAN with gradient penalty）模型，其中`train_set`是训练数据集的相对路径：

```python
python train-wgangp.py --train_set=data/train
```

3. 测试训练好的模型，其中`val_set`指定验证集的地址，在第1个epoch到第100个epoch的模型上测试（存放在checkpoint中），epoch的interval为1：

```python
python eval.py --val_set=data/val --start=1 --end=100 --interval=1
```

4. 对单幅照片进行超分辨，`lr.png`是指定的图片：

```python
python sr.py --lr=lr.png
```

5. 比较所有的模型，其中`val_set`是最终测试图片的相对路径：

```python
python eval-compare.py --val_set=results/Original
```

### 注意

- 由于checkpoint中模型占用内存过大，因此提交的文件中仅保留150epoch后的训练好的模型。

- 如果需要可视化训练过程，需要额外安装`tensorboard`。
