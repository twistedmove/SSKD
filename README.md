# SSKD
This repo is the implementation of paper Knowledge Distillation Meets Self-Supervision.

## Prerequisite
This repo is tested with Ubuntu 16.04.5, Python 3.7, PyTorch 1.5.0, CUDA 10.2.
Make sure to install pytorch, torchvision, tensorboardX, numpy before using this repo.

## Running

### Teacher Training
An example of teacher training is:
```
python teacher.py --arch wrn_40_2 --lr 0.05 --gpu-id 0
```
where you can specify the architecture via flag `--arch`

### Student Training
An example of student training is:
```
python student.py --t-path ./experiments/teacher_wrn_40_2_seed0/ --s-arch wrn_16_2 --lr 0.05 --gpu-id 0
```
The meanings of flags are:
> `--t-path`: teacher's checkpoint path. Automatically search the checkpoint containing 'best' keyword in its name.

> `--s-arch`: student's architecture.

All the commands can be found in `command.sh`

## Results

### Similar-Architecture

| Teacher <br> Student | wrn40-2 <br> wrn16-2 | wrn40-2 <br> wrn40-1 | resnet56 <br> resnet20 | resnet32x4 <br> resnet8x4 |  vgg13 <br> vgg8 |
|:---------------:|:-----------------:|:-----------------:|:-----------------:|:--------------------:|:-----------:|
| Teacher <br> Student |    76.46 <br> 73.64    |    76.46 <br> 72.24    |    73.44 <br> 69.63    |     79.63 <br> 72.51     | 75.38 <br> 70.68 |
| KD | 74.92 | 73.54 | 70.66 | 73.33 | 72.98 |
| FitNet | 75.75 | 74.12 | 71.60 | 74.31 | 73.54 |
| AT | 75.28 | 74.45 | 71.78 | 74.26 | 73.62 |
| SP | 75.34 | 73.15 | 71.48 | 74.74 | 73.44 |
| VID | 74.79 | 74.20 | 71.71 | 74.82 | 73.96 |
| RKD | 75.40 | 73.87 | 71.48 | 74.47 | 73.72 |
| PKT | 76.01 | 74.40 | 71.44 | 74.17 | 73.37 |
| AB | 68.89 | 75.06 | 71.49 | 74.45 | 74.27 |
| FT | 75.15 | 74.37 | 71.52 | 75.02 | 73.42 |
| CRD | 75.64 | 74.38 | 71.63 | 75.46 | 74.29 |
| SSKD | 76.04 | 76.13 | 71.49 | 76.20 | 75.33 |

### Cross-Architecture

| Teacher <br> Student | vgg13 <br> MobieleNetV2 | ResNet50 <br> MobileNetV2 | ResNet50 <br> vgg8 | resnet32x4 <br> ShuffleV1 |  resnet32x4 <br> ShuffleV2 | wrn40-2 <br> ShuffleV1|
|:---------------:|:-----------------:|:-----------------:|:-----------------:|:--------------------:|:-----------:|:-------------:|
| Teacher <br> Student |    75.38 <br> 65.79    |    79.10 <br> 65.79    |    79.10 <br> 70.68    |    79.63 <br> 70.77     | 79.63 <br> 73.12 | 76.46 <br> 70.77 |
| KD | 67.37 | 67.35| 73.81| 74.07| 74.45| 74.83|
| FitNet |68.58 | 68.54 | 73.84 | 74.82 | 75.11 | 75.55 |
| AT | 69.34 | 69.28 | 73.45 | 74.76 | 75.30 | 75.61 |
| SP | 66.89 | 68.99 | 73.86 | 73.80 | 75.15 | 75.56 |
| VID | 66.91 | 68.88 | 73.75 | 74.28 | 75.78 | 75.36 |
| RKD | 68.50 | 68.46 | 73.73 | 74.20 | 75.74 | 75.45 |
| PKT | 67.89 | 68.44 | 73.53 | 74.06 | 75.18 | 75.51 |
| AB | 68.86 | 69.32 | 74.20 | 76.24 | 75.66 | 76.58 |
| FT | 69.19 | 69.01 | 73.58 | 74.31 | 74.95 | 75.18 |
| CRD | 69.94 | 69.54 | 74.58 | 75.12 | 76.05 | 76.27 |
| SSKD | 71.53 | 72.57 | 75.76 | 78.44 | 78.61 | 77.40 |
