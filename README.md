# AICUP (隊伍: CCUML_頂樓集合)

## Introduction
場景文字檢測通常為場景文字辨識的前置步驟，即由畫面的像素中判斷文字出現的位置，以利後續針對該位置辨識可能的文字內容。場景文字檢測直接影響了文字辨識的準確度，本次賽事目標即為定位畫面中肉眼可識的文字位置。場景文字檢測受到許多因素所影響，包括場景中可能出現的多型態文字、多國文字、傾斜招牌文字、不同尺寸文字、外物遮蔽、類文字圖案紋理干擾、光線與陰影等。本賽事的目標場景為台灣市區街景，期望參賽者利用機器學習/深度學習技術，嘗試與開發適當的模型，以確偵測台灣街景畫面中的文字區域。

---

## Configuration Environment
+ Linux Ubuntu 18.04.04 LTS
+ Python 3.7
+ CUDA version: 10.1, V10.1.243

---

## Folder Structure
+ ```dataset```  dir:

Training and validation data are placed here.
```bash=
|__AICUP2021
|  |__TrainDataset
|  |  |__img
|  |  |  |__img_1.jpg
|  |  |__train_gts
|  |  |  |__img_1.txt
|  |  |__train_list.txt
|  |__ValidationDataset
|  |  |__img
|  |  |  |__img_3701.jpg
|  |  |__valid_gts
|  |  |  |__img_3701.txt
|  |  |__valid_list.txt
```

+ ```experiments``` dir:

The YAML file with the name of \*AICUP\*.yaml, used to define the model structure 、 training hyperparameters and data preprocessing.
```bash=
|__seg_detector
|  |__base.yaml
|  |__base_AICUP.yaml
|  |__AICUP_resnet50_deform_thre.yaml
```

---
## Installation requirements library
```python=
pip install -r requirements.txt
```
---

## Running experiments

* Training
```bash=
CUDA_VISIBLE_DEVICES=0 python train.py {config_yaml} \
--num_gpus 1 --epochs 1 --num_workers 4 --batch_size 8
```

* Evaluate
```bash=
CUDA_VISIBLE_DEVICES=0 python eval.py {config_yaml} --resume {model_weight_path} --box_thresh 0.5
```

* Predict
```bash=
CUDA_VISIBLE_DEVICES=0 python origiDemo.py {config_yaml} \
--resume {model_weight_path}} \
--image_path {image_dir_path} \
--box_thresh 0.5 --visualize
```

* Generate Excel Result
```bash=
CUDA_VISIBLE_DEVICES=0 python demo.py {config_yaml} \
--resume {model_weight_path}} \
--image_path {image_dir_path} \
--box_thresh 0.5 \
--visualize \
--output_csvName {csv_name}
```

---

# Reference
1. Liao, M.; Wan, Z.; Yao, C.; Chen, K.; and Bai, X. 2020. Real-Time Scene Text Detection with Differentiable Binarization. In AAAI.
2. He, K., Zhang, X., Ren, S., Sun, J.: Deep Residual Learning for Image Recognition. CoRR abs/1512.03385 (2015)
3. G. Huang, Z. Liu, K. Q. Weinberger, and L. Maaten. Densely connected convolutional networks. In CVPR, 2017

---

# Acknowledgment
**Most of the program code are based on DB([Github](https://github.com/MhLiao/DB)).**

---

# Members
**Chen-Mao Liao**

**Hong-Jia Chen**

**Yu-Ruei Lin**
