# Baseline Selection Guide for Spatiotemporal Prediction

本文档为研究人员和从业者提供了OpenSTL库中时空预测模型的基线算法选择指南。我们根据性能、计算效率和使用场景，推荐以下几组基线模型。

This document provides a baseline algorithm selection guide for spatiotemporal prediction models in the OpenSTL library. We recommend several groups of baseline models based on performance, computational efficiency, and usage scenarios.

## 推荐的基线模型 / Recommended Baseline Models

### 1. 经典RNN基线 / Classic RNN Baselines

这些模型是时空预测领域的经典方法，适合作为基础基线。

These models are classic methods in spatiotemporal prediction, suitable as fundamental baselines.

#### ConvLSTM (NeurIPS'2015)
- **优点 / Advantages**: 
  - 经典且广泛使用的架构 / Classic and widely-used architecture
  - 实现简单，易于理解 / Simple implementation, easy to understand
  - 在多个数据集上表现稳定 / Stable performance across multiple datasets
  
- **性能参考 / Performance Reference** (Moving MNIST, 10→10 frames):
  - MSE: 22.41 (2000 epochs)
  - Parameters: 15.0M
  - FPS: 113
  
- **配置文件 / Config**: `configs/mmnist/ConvLSTM.py`

- **推荐用途 / Recommended Use**: 作为所有时空预测任务的基础基线 / As fundamental baseline for all spatiotemporal prediction tasks

#### PredRNN (NeurIPS'2017)
- **优点 / Advantages**:
  - 引入空间记忆流 / Introduces spatiotemporal memory flow
  - 在长期预测中表现更好 / Better performance in long-term prediction
  - 广泛用于视频预测基准 / Widely used in video prediction benchmarks
  
- **性能参考 / Performance Reference** (Moving MNIST, 10→10 frames):
  - MSE: 26.43 (2000 epochs)
  - Parameters: 23.8M
  - FPS: 54
  
- **配置文件 / Config**: `configs/mmnist/PredRNN.py`

- **推荐用途 / Recommended Use**: 作为RNN类方法的标准基线 / As standard baseline for RNN-based methods

### 2. 改进的RNN基线 / Improved RNN Baselines

这些模型在经典RNN基础上进行了改进，提供更强的预测能力。

These models improve upon classic RNNs, providing stronger prediction capabilities.

#### PredRNN++ (ICML'2018)
- **优点 / Advantages**:
  - 采用因果LSTM和梯度高速公路 / Uses Causal LSTM and Gradient Highway
  - 在大多数基准上优于PredRNN / Outperforms PredRNN on most benchmarks
  - 适合作为中等复杂度基线 / Suitable as medium-complexity baseline
  
- **性能参考 / Performance Reference** (Moving MNIST, 10→10 frames):
  - MSE: 14.07 (2000 epochs)
  - Parameters: 38.6M
  - FPS: 38
  
- **配置文件 / Config**: `configs/mmnist/PredRNNpp.py`

- **推荐用途 / Recommended Use**: 作为改进RNN方法的对比基线 / As comparison baseline for improved RNN methods

#### MIM (CVPR'2019)
- **优点 / Advantages**:
  - 模拟运动和内容的交互 / Models interaction between motion and content
  - 在复杂场景中表现优秀 / Excellent performance in complex scenarios
  
- **性能参考 / Performance Reference** (Moving MNIST, 10→10 frames):
  - MSE: 14.73 (2000 epochs)
  - Parameters: 38.0M
  - FPS: 37
  
- **配置文件 / Config**: `configs/mmnist/MIM.py`

- **推荐用途 / Recommended Use**: 作为注意力机制RNN的基线 / As baseline for attention-based RNN methods

### 3. CNN基线 / CNN Baselines

这些基于CNN的方法提供了快速高效的替代方案。

These CNN-based methods provide fast and efficient alternatives.

#### SimVP+gSTA (CVPR'2022, ArXiv'2022)
- **优点 / Advantages**:
  - 无RNN架构，训练和推理速度快 / RNN-free architecture, fast training and inference
  - 参数效率高 / Parameter efficient
  - 在大多数任务上达到SOTA性能 / Achieves SOTA performance on most tasks
  - 易于扩展和修改 / Easy to extend and modify
  
- **性能参考 / Performance Reference** (Moving MNIST, 10→10 frames):
  - MSE: 15.05 (2000 epochs)
  - Parameters: 46.8M
  - FPS: 282
  
- **配置文件 / Config**: `configs/mmnist/simvp/SimVP_gSTA.py`

- **推荐用途 / Recommended Use**: 作为现代CNN方法的主要基线 / As primary baseline for modern CNN methods

#### TAU (CVPR'2023)
- **优点 / Advantages**:
  - 使用时间注意力单元 / Uses Temporal Attention Unit
  - 在视频和气象预测中表现优异 / Excellent performance in video and weather prediction
  - 计算效率高 / High computational efficiency
  
- **性能参考 / Performance Reference** (Moving MNIST, 10→10 frames):
  - MSE: 15.69 (2000 epochs)
  - Parameters: 44.7M
  - FPS: 283
  
- **配置文件 / Config**: `configs/mmnist/TAU.py`

- **推荐用途 / Recommended Use**: 作为最新方法的对比基线 / As comparison baseline for latest methods

### 4. 物理驱动基线 / Physics-Driven Baseline

#### PhyDNet (CVPR'2020)
- **优点 / Advantages**:
  - 结合物理先验知识 / Incorporates physical priors
  - 参数量小，计算效率高 / Small parameter count, high computational efficiency
  - 在物理约束场景中表现优秀 / Excellent in physically-constrained scenarios
  
- **性能参考 / Performance Reference** (Moving MNIST, 10→10 frames):
  - MSE: 20.35 (2000 epochs)
  - Parameters: 3.1M
  - FPS: 182
  
- **配置文件 / Config**: `configs/mmnist/PhyDNet.py`

- **推荐用途 / Recommended Use**: 作为物理驱动方法的基线 / As baseline for physics-driven methods

## 按应用场景的推荐 / Recommendations by Application Scenario

### 视频预测 / Video Prediction
**推荐组合 / Recommended Set**:
1. ConvLSTM (基础基线 / Basic baseline)
2. PredRNN++ (RNN基线 / RNN baseline)
3. SimVP+gSTA (CNN基线 / CNN baseline)
4. TAU (SOTA基线 / SOTA baseline)

### 交通流预测 / Traffic Flow Prediction
**推荐组合 / Recommended Set**:
1. ConvLSTM (基础基线 / Basic baseline)
2. PredRNN (RNN基线 / RNN baseline)
3. SimVP+gSTA (高效基线 / Efficient baseline)

### 气象预测 / Weather Forecasting
**推荐组合 / Recommended Set**:
1. ConvLSTM (基础基线 / Basic baseline)
2. PhyDNet (物理驱动基线 / Physics-driven baseline)
3. SimVP+gSTA (高效基线 / Efficient baseline)
4. TAU (SOTA基线 / SOTA baseline)

## 按计算资源的推荐 / Recommendations by Computational Resources

### 有限资源 / Limited Resources (< 8GB GPU)
1. **PhyDNet**: 3.1M params, 最轻量 / Most lightweight
2. **ConvLSTM-S**: 15.0M params, 平衡性能和速度 / Balanced performance and speed
3. **SimVP+gSTA**: 46.8M params, 高性能但需要更多内存 / High performance but requires more memory

### 中等资源 / Medium Resources (8-16GB GPU)
1. **ConvLSTM-S**: 基础基线 / Basic baseline
2. **PredRNN**: 标准RNN基线 / Standard RNN baseline
3. **SimVP+gSTA**: 主要CNN基线 / Primary CNN baseline
4. **TAU**: 高性能基线 / High-performance baseline

### 充足资源 / Abundant Resources (> 16GB GPU)
1. **ConvLSTM-L**: 大型变体 / Large variant
2. **PredRNN++**: 改进RNN / Improved RNN
3. **MIM**: 注意力机制 / Attention mechanism
4. **SimVP+gSTA**: 高性能CNN / High-performance CNN
5. **TAU**: SOTA方法 / SOTA method

## 性能对比总结 / Performance Comparison Summary

基于Moving MNIST数据集 (10→10帧预测，2000 epochs):

Based on Moving MNIST dataset (10→10 frames prediction, 2000 epochs):

| Method | MSE ↓ | MAE ↓ | SSIM ↑ | Params (M) | FPS | Type |
|--------|-------|-------|--------|------------|-----|------|
| PhyDNet | 20.35 | 61.47 | 0.9559 | 3.1 | 182 | Physics |
| PredRNN++ | 14.07 | 48.91 | 0.9698 | 38.6 | 38 | RNN |
| MIM | 14.73 | 52.31 | 0.9678 | 38.0 | 37 | RNN |
| SimVP+gSTA | 15.05 | 49.80 | 0.9675 | 46.8 | 282 | CNN |
| TAU | 15.69 | 51.46 | 0.9661 | 44.7 | 283 | CNN |
| ConvLSTM-S | 22.41 | 73.07 | 0.9480 | 15.0 | 113 | RNN |
| PredRNN | 26.43 | 77.52 | 0.9411 | 23.8 | 54 | RNN |

## 快速开始 / Quick Start

### 训练基线模型 / Training Baseline Models

```bash
# ConvLSTM基线 / ConvLSTM Baseline
python tools/train.py -d mmnist --lr 1e-3 -c configs/mmnist/ConvLSTM.py --ex_name mmnist_convlstm

# PredRNN基线 / PredRNN Baseline
python tools/train.py -d mmnist --lr 1e-3 -c configs/mmnist/PredRNN.py --ex_name mmnist_predrnn

# SimVP+gSTA基线 / SimVP+gSTA Baseline
python tools/train.py -d mmnist --lr 1e-3 -c configs/mmnist/simvp/SimVP_gSTA.py --ex_name mmnist_simvp_gsta

# TAU基线 / TAU Baseline
python tools/train.py -d mmnist --lr 1e-3 -c configs/mmnist/TAU.py --ex_name mmnist_tau

# PhyDNet基线 / PhyDNet Baseline
python tools/train.py -d mmnist --lr 1e-3 -c configs/mmnist/PhyDNet.py --ex_name mmnist_phydnet
```

### 测试基线模型 / Testing Baseline Models

```bash
python tools/test.py -d mmnist -c configs/mmnist/ConvLSTM.py --ex_name mmnist_convlstm
```

## 引用 / Citations

如果您在研究中使用这些基线模型，请引用相应的论文和OpenSTL基准:

If you use these baseline models in your research, please cite the corresponding papers and OpenSTL benchmark:

```bibtex
@inproceedings{tan2023openstl,
  title={OpenSTL: A Comprehensive Benchmark of Spatio-Temporal Predictive Learning},
  author={Tan, Cheng and Li, Siyuan and Gao, Zhangyang and Guan, Wenfei and Wang, Zedong and Liu, Zicheng and Wu, Lirong and Li, Stan Z},
  booktitle={Conference on Neural Information Processing Systems Datasets and Benchmarks Track},
  year={2023}
}
```

## 参考资源 / Reference Resources

- [OpenSTL GitHub Repository](https://github.com/chengtan9907/OpenSTL)
- [OpenSTL Documentation](https://openstl.readthedocs.io/)
- [Video Prediction Benchmarks](./model_zoos/video_benchmarks.md)
- [Weather Prediction Benchmarks](./model_zoos/weather_benchmarks.md)
- [Traffic Prediction Benchmarks](./model_zoos/traffic_benchmarks.md)

## 更新日志 / Changelog

- **2025-10-31**: 初始版本，包含7个推荐基线模型 / Initial version with 7 recommended baseline models
