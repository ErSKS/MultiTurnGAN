# MultiTurnGAN
Multi-turn Generative Adversarial Networks

# Related Research Works
- AttnGAN: Fine-Grained Text to Image Generation with Attentional Generative Adversarial Networks [[Paper]](https://arxiv.org/abs/1711.10485)  [[Code]](https://github.com/taoxugit/AttnGAN)
- StackGAN++: Realistic Image Synthesis with Stacked Generative Adversarial Networks [[Paper]](https://arxiv.org/abs/1710.10916) [[Code]](https://github.com/hanzhanggit/StackGAN-v2)
- Unsupervised Representation Learning with Deep Convolutional Generative Adversarial Networks [[Paper]](https://arxiv.org/abs/1511.06434)  [[Code]](https://github.com/carpedm20/DCGAN-tensorflow)
- Generative Adversarial Text-to-Image Synthesis [[Paper]](https://arxiv.org/abs/1605.05396) [Code](https://github.com/reedscot/icml2016)
- Learning Deep Representations of Fine-grained Visual Descriptions [[Paper]](https://arxiv.org/abs/1605.05395) [Code](https://github.com/reedscot/cvpr2016)

# Experimental Tool Setup
- Hardware Setup
  - GPU: 2x RTX 2080 Ti
  - CPU: 64GB DDR6
  - Chipset: 
  - HDD#1: 1TB SSD
  - HDD#2: 4TB SATA
- Software Setup
  - PyCharm Installation - `sudo snap install pycharm-community --classic`
  - Tensorflow Installation
  - PyTorch Installation
  - ElectronJS Installation
- Ubuntu Shortcut
  - Paste Command - Ctrl + Shift + V
  - Windows Screenshot - Alt + PtrScr
  - Change Machine Name - `sudo hostnamectl set-hostname AI_Lab` view change - `hostnamectl`

### Dependencies
python 2.7

Pytorch

In addition, please add the project folder to PYTHONPATH and `pip install` the following packages:
- `python-dateutil`
- `easydict`
- `pandas`
- `torchfile`
- `nltk`
- `scikit-image`



**Data**

1. Download our preprocessed metadata for [birds](https://drive.google.com/open?id=1O_LtUP9sch09QH3s_EBAgLEctBQ5JBSJ) [coco](https://drive.google.com/open?id=1rSnbIGNDGZeHlsUlLdahj0RJ9oo6lgH9) and save them to `data/`
2. Download the [birds](http://www.vision.caltech.edu/visipedia/CUB-200-2011.html) image data. Extract them to `data/birds/`
3. Download [coco](http://cocodataset.org/#download) dataset and extract the images to `data/coco/`



**Training**
- Pre-train DMS models:
  - For bird dataset: `python pretrain_DMS.py --cfg cfg/DMS/bird.yml --gpu 0`
  - For coco dataset: `python pretrain_DMS.py --cfg cfg/DMS/coco.yml --gpu 0`
 
- Train AttnGAN models:
  - For bird dataset: `python main.py --cfg cfg/bird_mt.yml --gpu 0`
  - For coco dataset: `python main.py --cfg cfg/coco_mt.yml --gpu 0`

- `*.yml` files are example configuration files for training/evaluation our models.



**Pretrained Model**
- [DMS for bird](https://drive.google.com/open?id=1GNUKjVeyWYBJ8hEU-yrfYQpDOkxEyP3V). Download and save it to `DMSencoders/`
- [DMS for coco](https://drive.google.com/open?id=1zIrXCE9F6yfbEJIbNP5-YrEe2pZcPSGJ). Download and save it to `DMSencoders/`
- [AttnGAN for bird](https://drive.google.com/open?id=1lqNG75suOuR_8gjoEPYNp8VyT_ufPPig). Download and save it to `models/`
- [AttnGAN for coco](https://drive.google.com/open?id=1i9Xkg9nU74RAvkcqKE-rJYhjvzKAMnCi). Download and save it to `models/`

- [AttnDCGAN for bird](https://drive.google.com/open?id=19TG0JUoXurxsmZLaJ82Yo6O0UJ6aDBpg). Download and save it to `models/`
  - This is an variant of AttnGAN which applies the propsoed attention mechanisms to DCGAN framework. 

**Sampling**
- Run `python main.py --cfg cfg/eval_bird.yml --gpu 0` to generate examples from captions in files listed in "./data/birds/example_filenames.txt". Results are saved to `DMSencoders/`. 
- Change the `eval_*.yml` files to generate images from other pre-trained models. 
- Input your own sentence in "./data/birds/example_captions.txt" if you wannt to generate images from customized sentences. 

**Validation**
- To generate images for all captions in the validation dataset, change B_VALIDATION to True in the eval_*.yml. and then run `python main.py --cfg cfg/eval_bird.yml --gpu 0`
- We compute inception score for models trained on birds using [StackGAN-inception-model](https://github.com/hanzhanggit/StackGAN-inception-model).
- We compute inception score for models trained on coco using [improved-gan/inception_score](https://github.com/openai/improved-gan/tree/master/inception_score).
