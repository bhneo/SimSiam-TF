# SimSiam-TF

This is an unofficial implementation of SimSiam ([Exploring Simple Siamese Representation Learning, CVPR 2021.](https://arxiv.org/abs/2011.10566)).

## Requirements
- python >= 3.6
- tensorflow >= 2.2

## Training
```
python main.py \
    --task pretext \
    --stop_gradient \
    --proj_bn_hidden \
    --proj_bn_output \
    --pred_bn_hidden \
    --weight_decay 0.0001 \
    --batch_size 256 \
    --epochs 200 \
    --lr_mode cosine \
    --data_path /path/of/your/data \
    --gpus gpu id(s) which will be used
```
### or 
```
python main.py \
    --task pretext \
    --stop_gradient \
    --proj_bn_hidden \
    --proj_bn_output \
    --pred_bn_hidden \
    --weight_decay 0.0005 \
    --batch_size 512 \
    --epochs 800 \
    --lr_mode cosine \
    --data_path data \
    --dataset cifar10 \
    --backbone resnet18 \
    --img_size 32 \
    --classes 10 \
    --filters 64 \
    --evaluate  \
    --checkpoint  \
    --history  \
    --tensorboard \
    --tb_interval 10 \
    --tb_histogram 10 \
    --gpu 0 \
    --resume \
    --proj_dim 512 \
    --pred_dim 512 \
    --stamp 210922_Wed_10_59_34
```

## Evaluation
To evaluate pre-trained model with linear classification,
```
python main.py \
    --task lincls \
    --batch_size 256 \
    --epochs 90 \
    --lr 30 \
    --lr_mode cosine \
    --data_path /path/of/your/data \
    --snapshot /path/of/checkpoint \
    --gpus gpu id(s) which will be used
```
### or
```
python main.py \
    --task lincls \
    --batch_size 512 \
    --epochs 90 \
    --lr_mode cosine \
    --data_path data \
    --snapshot result/pretext/210918_Sat_16_54_19/checkpoint \
    --dataset cifar10 \
    --backbone resnet18 \
    --img_size 32 \
    --classes 10 \
    --filters 32 \
    --evaluate  \
    --checkpoint  \
    --history  \
    --tensorboard \
    --tb_interval 10 \
    --tb_histogram 10 \
    --gpu 0 \
    --freeze \
    --pred_layer proj_fc3
```

## Results
### ImageNet
|         Model         | batch | Accuracy (paper) | Accuracy (ours) |
| --------------------- | ----- | ---------------- | --------------- |
| ResNet50 (200 epochs) |  256  |       68.1       |       -         |

### CIFAR10
|         Model         | batch | Accuracy (paper) | Accuracy (ours) |
| --------------------- | ----- | ---------------- | --------------- |
| ResNet50 (800 epochs) |  256  |       91.1       |       90.7      |
<img width=70% height=70% src='./result_cifar10.png'>

## Citation
```
@article{Chen2020ExploringSS,
  title={Exploring Simple Siamese Representation Learning},
  author={Xinlei Chen and Kaiming He},
  journal={ArXiv},
  year={2020},
  volume={abs/2011.10566}
}
```
