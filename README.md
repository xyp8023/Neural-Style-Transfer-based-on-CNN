### Neural Style Transfer 
This is a Tensorflow implementation for several techniques in the following papers:

["A Neural Algorithm of Artistic Style"](https://arxiv.org/pdf/1508.06576.pdf) by Leon A. Gatys, Alexander S. Ecker, Matthias Bethge

["Image Style Transfer Using Convolutional Neural Networks"](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Gatys_Image_Style_Transfer_CVPR_2016_paper.pdf) by Leon A. Gatys, Alexander S. Ecker, Matthias Bethge

["Preserving Color in Neural Artistic Style Transfer"](https://arxiv.org/pdf/1606.05897.pdf) by Leon A. Gatys, Matthias Bethge, Aaron Hertzmann, Eli Shechtman

["Laplacian-Steered Neural Style Transfer"](https://arxiv.org/pdf/1707.01253.pdf) by Shaohua Li, Xinxing Xu, Liqiang Nie, Tat-Seng Chua

### Setup
This code is based on Tensorflow. It has been tested on Windows 10 and Ubuntu 16.04 LTS.  
Dependencies:  
* Tensowflow
* nmupy
* matplotlib
* scipy
* PIL  

Recommended but optional:  
* CUDA
* cudnn

### Download VGG19 via following URL:
```
http://www.vlfeat.org/matconvnet/models/imagenet-vgg-verydeep-19.mat
```
And please save the file under ``pre_trained_model``

### Commands
  Quick start
```
python run_main.py --content images/01.jpg --style images/starry-night.jpg --output stockholm.jpg
```
  Multi-Style transfer
```
python run_main.py --content images/01.jpg --style images/starry-night.jpg --output stockholm.jpg --multi_style True --style_ratio 0.5 
```

### Arguments

Required:  

* ``--content``: Filename of the content image. *Default:* ``images/tubingen.jpg``
* ``--style``: Filename of the style image. *Default:* ``images/starry-night.jpg``
* ``--output``: Filename of the output image. *Default:* ``result.jpg``

Optional:
* ``--model_path``: Path to the pre-trained VGG model. *Default:* ``pre_trained_model``  
* ``--loss_ratio``: Weight of content-loss relative to style-loss, the alpha over beta in the paper. *Default:* ``0.5``  
* ``--content_layers``: Space-separated VGG-19 layer names used for content loss computation. *Default:* ``conv4_2``  
* ``--style_layers``: Space-separated VGG-19 layer names used for style loss computation. *Default:* ``relu1_1, relu2_1, relu3_1, relu4_1, relu5_1``  
* ``--content_layer_weights``: Space-separated weights of each content layer to the content loss. *Default:* ``1.0``
* ``--style_layer_weights``: Space-separated weights of each style layer to loss. *Default:* ``0.2 0.2 0.2 0.2 0.2``
* ``--initial_type``: The initial image for optimization. (notation in the paper : x) Choices: content, style, random. *Default:* ``content``
* ``--max_size``: Maximum width or height of the input images. *Default:* ``512``
* ``--content_loss_norm_type``: Different types of normalization for content loss. *Choices:* [1](https://arxiv.org/pdf/1508.06576v2.pdf), [2](https://arxiv.org/pdf/1604.08610.pdf), [3](https://github.com/cysmith/neural-style-tf). *Default:* ``3``
* ``--num_iter``: The number of iterations to run. *Default:* ``1000``
* ``--multi_style``: If to use multiple style transfer. *Choices:* ``True/False`` *Default:* ``False``
* ``--style2``: Filename to use multiple style images. *Example:* ``images/kandinsky.jpg``

| Para | Function  |
| ---------- | :-----------:  |
| --model_path  | 预训练的VGG模型的参数文件的路径    |
| --content  | 内容图片的路径    |
| --style  | 风格图片的路径    |
| --output  | 输出图片的路径    |
| --loss_ratio  | 内容损失和风格损失的相对权重，就是论文中公式7的alpha和beta    |
| --content_layers  | 用于计算内容损失的representation    |
| --style_layers  | 用于计算风格损失的representation，这个represention取自很多层，并对它们做一个加权和    |
| --content_layer_weights  | 内容represention的权重，实际上论文中和代码中都只采用了一个representation(4_2)，因此该权重只有一个    |
| --style_layer_weights  | 风格represention的权重，默认有五个，分别对应于每层挑选出来的用于计算风格损失的representation    |
| --initial_type  | 有三个选项，将初时待合成图片设置为内容图片或风格图片或随机白噪声图片(论文中的做法)    |
| --max_size  | 输入图片的最大尺寸，默认512    |
| --content_loss_norm_type  | 该选项用于确定内容损失函数normalization的方式，目测没啥用    |
| --num_iter  | 迭代次数，它默认设置的是1000，但我每次都跑了1000多次。。    |
| --style2  | 第二张风格图片的路径    |
| --multi_style  | True/False 是否进行多风格迁移|
| --style_ratio  | 两个风格图片损失所占的比重    |
| --color_preseving  | True/False, 是否使用color preserving  |
| --color_convert_type  | yuv/ycrcb/luv/lab  |
| --color_preserve_algo  | 1/2, 1 直接替换亮度通道，2 使用论文中的那个公式 |
| --tv  | True/False, 是否添加tv项 |
| --laplace  | True/False, 是否添加laplace项 |
| --lap_lambda  | laplace项的系数 |
| --pooling_size  | ? |


### Parameters

| Para | Function  |
| ---------- | :-----------:  |
| --model_path  | 预训练的VGG模型的参数文件的路径    |
| --content  | 内容图片的路径    |
| --style  | 风格图片的路径    |
| --output  | 输出图片的路径    |
| --loss_ratio  | 内容损失和风格损失的相对权重，就是论文中公式7的alpha和beta    |
| --content_layers  | 用于计算内容损失的representation    |
| --style_layers  | 用于计算风格损失的representation，这个represention取自很多层，并对它们做一个加权和    |
| --content_layer_weights  | 内容represention的权重，实际上论文中和代码中都只采用了一个representation(4_2)，因此该权重只有一个    |
| --style_layer_weights  | 风格represention的权重，默认有五个，分别对应于每层挑选出来的用于计算风格损失的representation    |
| --initial_type  | 有三个选项，将初时待合成图片设置为内容图片或风格图片或随机白噪声图片(论文中的做法)    |
| --max_size  | 输入图片的最大尺寸，默认512    |
| --content_loss_norm_type  | 该选项用于确定内容损失函数normalization的方式，目测没啥用    |
| --num_iter  | 迭代次数，它默认设置的是1000，但我每次都跑了1000多次。。    |



以下是我加的：

| Para | Function  |
| ---------- | :-----------:  |
| --style2  | 第二张风格图片的路径    |
| --multi_style  | True/False 是否进行多风格迁移|
| --style_ratio  | 两个风格图片损失所占的比重    |
| --color_preseving  | True/False, 是否使用color preserving  |
| --color_convert_type  | yuv/ycrcb/luv/lab  |
| --color_preserve_algo  | 1/2, 1 直接替换亮度通道，2 使用论文中的那个公式 |
| --tv  | True/False, 是否添加tv项 |
| --laplace  | True/False, 是否添加laplace项 |
| --lap_lambda  | laplace项的系数 |
| --pooling_size  | ? |



