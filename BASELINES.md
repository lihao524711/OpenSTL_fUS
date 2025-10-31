# Baseline Models Quick Reference / 基线模型快速参考

## English

This document provides a quick reference for selecting baseline spatiotemporal prediction models from the OpenSTL library.

### Recommended Baseline Combinations

**For General Use (Minimum Set)**:
1. **ConvLSTM** - Classic RNN baseline
2. **SimVP+gSTA** - Modern CNN baseline
3. **TAU** - State-of-the-art baseline

**For Comprehensive Comparison**:
1. **ConvLSTM** - Classic RNN baseline
2. **PredRNN** - Standard RNN with spatiotemporal memory
3. **PredRNN++** - Improved RNN with Causal LSTM
4. **PhyDNet** - Physics-driven baseline
5. **SimVP+gSTA** - Efficient CNN baseline
6. **TAU** - SOTA temporal attention baseline
7. **MIM** - Attention-based RNN baseline

### Quick Training Commands

```bash
# Train all recommended baselines on Moving MNIST
python tools/train.py -d mmnist -c configs/mmnist/ConvLSTM.py --ex_name baseline_convlstm
python tools/train.py -d mmnist -c configs/mmnist/simvp/SimVP_gSTA.py --ex_name baseline_simvp
python tools/train.py -d mmnist -c configs/mmnist/TAU.py --ex_name baseline_tau
```

### Performance Summary (Moving MNIST, 2000 epochs)

| Model | MSE ↓ | Params | FPS | Type |
|-------|-------|--------|-----|------|
| PredRNN++ | 14.07 | 38.6M | 38 | RNN |
| MIM | 14.73 | 38.0M | 37 | RNN |
| SimVP+gSTA | 15.05 | 46.8M | 282 | CNN |
| TAU | 15.69 | 44.7M | 283 | CNN |
| PhyDNet | 20.35 | 3.1M | 182 | Physics |
| ConvLSTM | 22.41 | 15.0M | 113 | RNN |

**For detailed information, see**: [docs/en/baseline_selection.md](docs/en/baseline_selection.md)

---

## 中文

本文档为OpenSTL库中时空预测模型的基线选择提供快速参考。

### 推荐的基线组合

**通用场景（最小集合）**:
1. **ConvLSTM** - 经典RNN基线
2. **SimVP+gSTA** - 现代CNN基线
3. **TAU** - 最先进基线

**全面对比**:
1. **ConvLSTM** - 经典RNN基线
2. **PredRNN** - 带时空记忆的标准RNN
3. **PredRNN++** - 带因果LSTM的改进RNN
4. **PhyDNet** - 物理驱动基线
5. **SimVP+gSTA** - 高效CNN基线
6. **TAU** - SOTA时间注意力基线
7. **MIM** - 基于注意力的RNN基线

### 快速训练命令

```bash
# 在Moving MNIST上训练所有推荐基线
python tools/train.py -d mmnist -c configs/mmnist/ConvLSTM.py --ex_name baseline_convlstm
python tools/train.py -d mmnist -c configs/mmnist/simvp/SimVP_gSTA.py --ex_name baseline_simvp
python tools/train.py -d mmnist -c configs/mmnist/TAU.py --ex_name baseline_tau
```

### 性能总结 (Moving MNIST, 2000 epochs)

| 模型 | MSE ↓ | 参数量 | FPS | 类型 |
|------|-------|--------|-----|------|
| PredRNN++ | 14.07 | 38.6M | 38 | RNN |
| MIM | 14.73 | 38.0M | 37 | RNN |
| SimVP+gSTA | 15.05 | 46.8M | 282 | CNN |
| TAU | 15.69 | 44.7M | 283 | CNN |
| PhyDNet | 20.35 | 3.1M | 182 | 物理 |
| ConvLSTM | 22.41 | 15.0M | 113 | RNN |

**详细信息请参考**: [docs/zh/baseline_selection.md](docs/zh/baseline_selection.md)
