# YOLOv11 水果目标检测训练项目

本项目用于基于 YOLOv11 训练水果目标检测模型，包含训练 Notebook、训练数据集压缩包以及一次训练后的模型权重和可视化结果。

## 项目结构

```text
.
├── train/
│   ├── train.ipynb             # Kaggle/Python 训练 Notebook
│   └── split_dataset.zip       # 训练用数据集
├── yolov11_output/
│   ├── args.yaml               # 本次训练参数
│   ├── results.csv             # 训练指标日志
│   ├── results.png             # 训练曲线汇总图
│   ├── *_curve.png             # P/R/F1/PR 曲线
│   ├── confusion_matrix*.png   # 混淆矩阵
│   ├── train_batch*.jpg        # 训练批次可视化
│   ├── val_batch*_*.jpg        # 验证集预测可视化
│   └── weights/
│       ├── best.pt             # 最优模型权重
│       └── last.pt             # 最后一轮模型权重
└── README.md
```

## 数据集

训练数据集位于：

```text
train/split_dataset.zip
```

该文件约 5.34 GB。由于 GitHub 普通仓库对单个文件有 100 MB 限制，如果需要把该数据集上传到 GitHub，建议使用 Git LFS 管理大文件。

示例：

```bash
git lfs install
git lfs track "train/split_dataset.zip"
git lfs track "*.pt"
git add .gitattributes train/split_dataset.zip yolov11_output/weights/*.pt
```

## 环境依赖

Notebook 主要使用以下 Python 包：

```bash
pip install ultralytics numpy pandas matplotlib opencv-python seaborn squarify
```

如果在 Kaggle 环境运行，Notebook 中已包含：

```python
%pip install ultralytics
```

## 训练方式

1. 解压或挂载数据集，使 YOLO 数据配置文件可被访问。
2. 打开 `train/train.ipynb`。
3. 根据实际数据集路径修改 `model.train(data=...)` 中的 YAML 路径。
4. 运行 Notebook 开始训练。

Notebook 中使用的基础模型为：

```python
YOLO("yolo11n.pt")
```

主要训练参数可参考 `yolov11_output/args.yaml`，包括：

```text
epochs: 256
imgsz: 640
model: yolo11n.pt
task: detect
```

## 当前训练结果

本仓库保留了一次训练输出，目录为：

```text
yolov11_output/
```

第 256 轮结果摘要：

```text
precision: 0.94789
recall: 0.82076
mAP50: 0.90050
mAP50-95: 0.76199
```

最优权重文件：

```text
yolov11_output/weights/best.pt
```

## GitHub 上传说明

本项目的 `.gitignore` 只忽略系统缓存、Python 缓存、虚拟环境、Jupyter 临时文件和临时训练目录；不会忽略训练数据集、训练输出、图片结果或模型权重。

如果需要完整上传当前数据和模型权重，请先配置 Git LFS，尤其是 `train/split_dataset.zip`。
