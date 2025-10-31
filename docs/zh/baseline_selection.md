# 时空预测基线模型选择指南

本文档为研究人员和从业者提供了OpenSTL库中时空预测模型的基线算法选择指南。我们根据性能、计算效率和使用场景，推荐以下几组基线模型。

## 推荐的基线模型

### 1. 经典RNN基线

这些模型是时空预测领域的经典方法，适合作为基础基线。

#### ConvLSTM (NeurIPS'2015)
- **优点**: 
  - 经典且广泛使用的架构
  - 实现简单，易于理解
  - 在多个数据集上表现稳定
  
- **性能参考** (Moving MNIST, 10→10 frames):
  - MSE: 22.41 (2000 epochs)
  - 参数量: 15.0M
  - FPS: 113
  
- **配置文件**: `configs/mmnist/ConvLSTM.py`

- **推荐用途**: 作为所有时空预测任务的基础基线

#### PredRNN (NeurIPS'2017)
- **优点**:
  - 引入空间记忆流
  - 在长期预测中表现更好
  - 广泛用于视频预测基准
  
- **性能参考** (Moving MNIST, 10→10 frames):
  - MSE: 26.43 (2000 epochs)
  - 参数量: 23.8M
  - FPS: 54
  
- **配置文件**: `configs/mmnist/PredRNN.py`

- **推荐用途**: 作为RNN类方法的标准基线

### 2. 改进的RNN基线

这些模型在经典RNN基础上进行了改进，提供更强的预测能力。

#### PredRNN++ (ICML'2018)
- **优点**:
  - 采用因果LSTM和梯度高速公路
  - 在大多数基准上优于PredRNN
  - 适合作为中等复杂度基线
  
- **性能参考** (Moving MNIST, 10→10 frames):
  - MSE: 14.07 (2000 epochs)
  - 参数量: 38.6M
  - FPS: 38
  
- **配置文件**: `configs/mmnist/PredRNNpp.py`

- **推荐用途**: 作为改进RNN方法的对比基线

#### MIM (CVPR'2019)
- **优点**:
  - 模拟运动和内容的交互
  - 在复杂场景中表现优秀
  
- **性能参考** (Moving MNIST, 10→10 frames):
  - MSE: 14.73 (2000 epochs)
  - 参数量: 38.0M
  - FPS: 37
  
- **配置文件**: `configs/mmnist/MIM.py`

- **推荐用途**: 作为注意力机制RNN的基线

### 3. CNN基线

这些基于CNN的方法提供了快速高效的替代方案。

#### SimVP+gSTA (CVPR'2022, ArXiv'2022)
- **优点**:
  - 无RNN架构，训练和推理速度快
  - 参数效率高
  - 在大多数任务上达到SOTA性能
  - 易于扩展和修改
  
- **性能参考** (Moving MNIST, 10→10 frames):
  - MSE: 15.05 (2000 epochs)
  - 参数量: 46.8M
  - FPS: 282
  
- **配置文件**: `configs/mmnist/simvp/SimVP_gSTA.py`

- **推荐用途**: 作为现代CNN方法的主要基线

#### TAU (CVPR'2023)
- **优点**:
  - 使用时间注意力单元
  - 在视频和气象预测中表现优异
  - 计算效率高
  
- **性能参考** (Moving MNIST, 10→10 frames):
  - MSE: 15.69 (2000 epochs)
  - 参数量: 44.7M
  - FPS: 283
  
- **配置文件**: `configs/mmnist/TAU.py`

- **推荐用途**: 作为最新方法的对比基线

### 4. 物理驱动基线

#### PhyDNet (CVPR'2020)
- **优点**:
  - 结合物理先验知识
  - 参数量小，计算效率高
  - 在物理约束场景中表现优秀
  
- **性能参考** (Moving MNIST, 10→10 frames):
  - MSE: 20.35 (2000 epochs)
  - 参数量: 3.1M
  - FPS: 182
  
- **配置文件**: `configs/mmnist/PhyDNet.py`

- **推荐用途**: 作为物理驱动方法的基线

## 按应用场景的推荐

### 视频预测
**推荐组合**:
1. ConvLSTM (基础基线)
2. PredRNN++ (RNN基线)
3. SimVP+gSTA (CNN基线)
4. TAU (SOTA基线)

### 交通流预测
**推荐组合**:
1. ConvLSTM (基础基线)
2. PredRNN (RNN基线)
3. SimVP+gSTA (高效基线)

### 气象预测
**推荐组合**:
1. ConvLSTM (基础基线)
2. PhyDNet (物理驱动基线)
3. SimVP+gSTA (高效基线)
4. TAU (SOTA基线)

## 按计算资源的推荐

### 有限资源 (< 8GB GPU)
1. **PhyDNet**: 3.1M 参数，最轻量
2. **ConvLSTM-S**: 15.0M 参数，平衡性能和速度
3. **SimVP+gSTA**: 46.8M 参数，高性能但需要更多内存

### 中等资源 (8-16GB GPU)
1. **ConvLSTM-S**: 基础基线
2. **PredRNN**: 标准RNN基线
3. **SimVP+gSTA**: 主要CNN基线
4. **TAU**: 高性能基线

### 充足资源 (> 16GB GPU)
1. **ConvLSTM-L**: 大型变体
2. **PredRNN++**: 改进RNN
3. **MIM**: 注意力机制
4. **SimVP+gSTA**: 高性能CNN
5. **TAU**: SOTA方法

## 性能对比总结

基于Moving MNIST数据集 (10→10帧预测，2000 epochs):

| 方法 | MSE ↓ | MAE ↓ | SSIM ↑ | 参数量 (M) | FPS | 类型 |
|------|-------|-------|--------|-----------|-----|------|
| PhyDNet | 20.35 | 61.47 | 0.9559 | 3.1 | 182 | 物理 |
| PredRNN++ | 14.07 | 48.91 | 0.9698 | 38.6 | 38 | RNN |
| MIM | 14.73 | 52.31 | 0.9678 | 38.0 | 37 | RNN |
| SimVP+gSTA | 15.05 | 49.80 | 0.9675 | 46.8 | 282 | CNN |
| TAU | 15.69 | 51.46 | 0.9661 | 44.7 | 283 | CNN |
| ConvLSTM-S | 22.41 | 73.07 | 0.9480 | 15.0 | 113 | RNN |
| PredRNN | 26.43 | 77.52 | 0.9411 | 23.8 | 54 | RNN |

## 快速开始

### 训练基线模型

```bash
# ConvLSTM基线
python tools/train.py -d mmnist --lr 1e-3 -c configs/mmnist/ConvLSTM.py --ex_name mmnist_convlstm

# PredRNN基线
python tools/train.py -d mmnist --lr 1e-3 -c configs/mmnist/PredRNN.py --ex_name mmnist_predrnn

# SimVP+gSTA基线
python tools/train.py -d mmnist --lr 1e-3 -c configs/mmnist/simvp/SimVP_gSTA.py --ex_name mmnist_simvp_gsta

# TAU基线
python tools/train.py -d mmnist --lr 1e-3 -c configs/mmnist/TAU.py --ex_name mmnist_tau

# PhyDNet基线
python tools/train.py -d mmnist --lr 1e-3 -c configs/mmnist/PhyDNet.py --ex_name mmnist_phydnet
```

### 测试基线模型

```bash
python tools/test.py -d mmnist -c configs/mmnist/ConvLSTM.py --ex_name mmnist_convlstm
```

## 基线模型配置文件快速索引

为了方便使用，以下是所有推荐基线模型的配置文件路径：

### Moving MNIST数据集
- ConvLSTM: `configs/mmnist/ConvLSTM.py`
- PredRNN: `configs/mmnist/PredRNN.py`
- PredRNN++: `configs/mmnist/PredRNNpp.py`
- MIM: `configs/mmnist/MIM.py`
- PhyDNet: `configs/mmnist/PhyDNet.py`
- SimVP+gSTA: `configs/mmnist/simvp/SimVP_gSTA.py`
- TAU: `configs/mmnist/TAU.py`

### TaxiBJ数据集（交通流预测）
- ConvLSTM: `configs/taxibj/ConvLSTM.py`
- PredRNN: `configs/taxibj/PredRNN.py`
- SimVP+gSTA: `configs/taxibj/simvp/SimVP_gSTA.py`

### WeatherBench数据集（气象预测）
- ConvLSTM: `configs/weather/ConvLSTM.py`
- PhyDNet: `configs/weather/PhyDNet.py`
- SimVP+gSTA: `configs/weather/simvp/SimVP_gSTA.py`
- TAU: `configs/weather/TAU.py`

## 引用

如果您在研究中使用这些基线模型，请引用相应的论文和OpenSTL基准:

```bibtex
@inproceedings{tan2023openstl,
  title={OpenSTL: A Comprehensive Benchmark of Spatio-Temporal Predictive Learning},
  author={Tan, Cheng and Li, Siyuan and Gao, Zhangyang and Guan, Wenfei and Wang, Zedong and Liu, Zicheng and Wu, Lirong and Li, Stan Z},
  booktitle={Conference on Neural Information Processing Systems Datasets and Benchmarks Track},
  year={2023}
}
```

## 参考资源

- [OpenSTL GitHub仓库](https://github.com/chengtan9907/OpenSTL)
- [OpenSTL文档](https://openstl.readthedocs.io/)
- [视频预测基准](../en/model_zoos/video_benchmarks.md)
- [气象预测基准](../en/model_zoos/weather_benchmarks.md)
- [交通预测基准](../en/model_zoos/traffic_benchmarks.md)

## 更新日志

- **2025-10-31**: 初始版本，包含7个推荐基线模型
