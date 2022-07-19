# RBC
[RBC: Rectifying the Biased Context in Continual Semantic Segmentation](https://arxiv.org/abs/2203.08404) ECCV2022.

## Requirements
You need to install the following libraries:
- Python (3.6)
- Pytorch (1.8.1+cu102)
- torchvision (0.9.1+cu102)
- tensorboardX (1.8)
- apex (0.1)
- matplotlib (3.3.1)
- numpy (1.17.2)
- [inplace-abn](https://github.com/mapillary/inplace_abn) (1.0.7)

Note also that apex seems to only work with some CUDA versions, therefore try to install Pytorch (and torchvision) with
the 10.2 CUDA version. You'll probably need anaconda instead of pip in that case, sorry! Do:

```
conda install -y pytorch torchvision cudatoolkit=10.2 -c pytorch
cd apex
pip3 install -v --no-cache-dir --global-option="--cpp_ext" --global-option="--cuda_ext" ./
```

Note that while the code should be runnable without mixed precision (apex), some have reported lower perfs without it. So try with it!

The default is to use a pretraining for the backbone used, that is searched in the pretrained folder of the project. We used the pretrained model released by the authors of In-place ABN (as said in the paper), that can be found here: [link](https://github.com/mapillary/inplace_abn#training-on-imagenet-1k). You can also download the pretrained model by running the script *download_resnet101_iabn_sync.sh* from [link](https://github.com/arthurdouillard/CVPR2021_PLOP/releases/download/v1.0/resnet101_iabn_sync.pth.tar) (uploaded by Arthur Douillard).

## How to perform training
We provide some scripts under the directory `scripts/voc` to reproduce the results in our paper (included tasks are 15-5, 15-1, 19-1 (VOC)).

For example, do

````
bash scripts/voc/rbc_15-1.sh
````

Note that you will need to modify those scripts to include the path where your data.
And all of the provided scripts utilize the overlapped setting as default. If enable the disjoint setting, just delete the "--overlap".

## Thanks
Our code is modified from [PLOP](https://github.com/sntc129/CVPR2021_PLOP).

## Citation
```BibTeX
@article{zhao2022rbc,
  title={RBC: Rectifying the Biased Context in Continual Semantic Segmentation},
  author={Zhao, Hanbin and Yang, Fengyu and Fu, Xinghe and Li, Xi},
  journal={arXiv preprint arXiv:2203.08404},
  year={2022}
}
```
