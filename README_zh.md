## SMPL-X: 一个人体、面部和手部联合的3D模型

[[论文页面](https://smpl-x.is.tue.mpg.de)] [[论文](https://ps.is.tuebingen.mpg.de/uploads_file/attachment/attachment/497/SMPL-X.pdf)]
[[补充材料](https://ps.is.tuebingen.mpg.de/uploads_file/attachment/attachment/498/SMPL-X-supp.pdf)]

![SMPL-X 示例](./images/teaser_fig.png)

## 目录
  * [许可证](#许可证)
  * [描述](#描述)
  * [新闻](#新闻)
  * [安装](#安装)
  * [下载模型](#下载模型)
  * [加载SMPL-X、SMPL+H和SMPL](#加载smpl-x-smplh和smpl)
    * [SMPL和SMPL+H设置](#smpl和smplh设置)
    * [模型加载](https://github.com/vchoutas/smplx#model-loading)
  * [MANO和FLAME对应关系](#mano和flame对应关系)
  * [示例](#示例)
  * [修改模型的全局姿态](#修改模型的全局姿态)
  * [引用](#引用)
  * [致谢](#致谢)
  * [联系方式](#联系方式)

## 许可证

用于**非商业科学研究目的**的软件版权许可。
请仔细阅读[条款和条件](https://github.com/vchoutas/smplx/blob/master/LICENSE)和任何随附文档，然后再下载和/或使用SMPL-X/SMPLify-X模型、数据和软件(以下简称"模型和软件")，包括3D网格、混合权重、混合形状、纹理、软件、脚本和动画。通过下载和/或使用模型和软件(包括下载、克隆、安装和使用此github存储库的任何其他用途)，您承认您已阅读这些条款和条件，理解它们，并同意受其约束。如果您不同意这些条款和条件，则不得下载和/或使用模型和软件。违反本协议条款的任何行为将自动终止您根据此[许可证](./LICENSE)享有的权利。

## 免责声明

论文图1和图2中使用的原始图像可在该链接找到。
论文中的图像是在gettyimages.com的许可下使用的。
我们已获得在出版物中使用它们的权利，但不允许重新分发。
请按照给定链接上的说明获取使用权。
我们的结果是在原始图像的483 × 724像素分辨率上获得的。

## 描述

*SMPL-X* (SMPL eXpressive) 是一个统一的身体模型，其形状参数联合训练了
面部、手部和身体。*SMPL-X* 使用基于标准顶点的线性混合蒙皮与学习的校正混合
形状，具有N = 10,475个顶点和K = 54个关节，
其中包括颈部、下巴、眼球和手指的关节。
SMPL-X由函数M(θ, β, ψ)定义，其中θ是姿态参数，β是形状参数，
ψ是面部表情参数。

## 新闻

- 2020年11月3日：我们发布了在
  SMPL系列模型之间转换的代码。有关代码的更多详情，请转到此[自述
  文件](./transfer_model/README.md)。关于如何
  提取映射的详细解释可[在此](./transfer_model/docs/transfer.md)找到。
- 2020年9月23日：现在为SMPL-X提供UV贴图，请检查网站的
  下载部分。
- 2020年8月20日：现在提供SMPL-X的完整形状和表情空间。

## 安装

要安装模型，请按指定的顺序执行以下步骤：
1. 要从PyPi安装只需运行：
  ```Shell
  pip install smplx[all]
  ```
2. 克隆此存储库并使用*setup.py*脚本安装：
```Shell
git clone https://github.com/vchoutas/smplx
python setup.py install
```

## 下载模型

要下载*SMPL-X*模型，请前往[此项目网站](https://smpl-x.is.tue.mpg.de)并注册以获得下载部分的访问权限。

要下载*SMPL+H*模型，请前往[此项目网站](http://mano.is.tue.mpg.de)并注册以获得下载部分的访问权限。

要下载*SMPL*模型，请前往[此](http://smpl.is.tue.mpg.de)(男性和女性模型)和[此](http://smplify.is.tue.mpg.de)(性别中性模型)项目网站并注册以获得下载部分的访问权限。

## 加载SMPL-X、SMPL+H和SMPL

### SMPL和SMPL+H设置

加载器可以选择使用任何SMPL-X、SMPL+H、SMPL和MANO模型。根据您想使用的模型，请遵循相应的下载说明。要在MANO、SMPL、SMPL+H和SMPL-X之间切换，只需更改*model_path*或*model_type*参数。有关更多详情，请查看模型类的文档。
在使用SMPL和SMPL+H之前，您应遵循[tools/README.md](./tools/README.md)中的说明删除两个模型pkls中的
Chumpy对象，并合并MANO参数与SMPL+H。

### 模型加载

您可以使用来自[body_models](./smplx/body_models.py)的[create](https://github.com/vchoutas/smplx/blob/c63c02b478c5c6f696491ed9167e3af6b08d89b1/smplx/body_models.py#L54)
函数或直接调用
[SMPL](https://github.com/vchoutas/smplx/blob/c63c02b478c5c6f696491ed9167e3af6b08d89b1/smplx/body_models.py#L106)、
[SMPL+H](https://github.com/vchoutas/smplx/blob/c63c02b478c5c6f696491ed9167e3af6b08d89b1/smplx/body_models.py#L395)和
[SMPL-X](https://github.com/vchoutas/smplx/blob/c63c02b478c5c6f696491ed9167e3af6b08d89b1/smplx/body_models.py#L628)模型的构造函数。模型的路径可以是指向参数文件的路径，也可以是具有以下结构的目录：
```bash
models
├── smpl
│   ├── SMPL_FEMALE.pkl
│   └── SMPL_MALE.pkl
│   └── SMPL_NEUTRAL.pkl
├── smplh
│   ├── SMPLH_FEMALE.pkl
│   └── SMPLH_MALE.pkl
├── mano
|   ├── MANO_RIGHT.pkl
|   └── MANO_LEFT.pkl
└── smplx
    ├── SMPLX_FEMALE.npz
    ├── SMPLX_FEMALE.pkl
    ├── SMPLX_MALE.npz
    ├── SMPLX_MALE.pkl
    ├── SMPLX_NEUTRAL.npz
    └── SMPLX_NEUTRAL.pkl
```

## MANO和FLAME对应关系

SMPL-X与MANO、FLAME之间的顶点对应关系可从
[项目网站](https://smpl-x.is.tue.mpg.de)下载。如果您已将
对应数据提取到*correspondences*文件夹中，则使用以下
脚本来可视化它们：

1. 要查看MANO对应关系，请运行以下命令：

```
python examples/vis_mano_vertices.py --model-folder $SMPLX_FOLDER --corr-fname correspondences/MANO_SMPLX_vertex_ids.pkl
```

2. 要查看FLAME对应关系，请运行以下命令：

```
python examples/vis_flame_vertices.py --model-folder $SMPLX_FOLDER --corr-fname correspondences/SMPL-X__FLAME_vertex_ids.npy
```

## 示例

安装*smplx*包并下载模型参数后，您应该能够运行*demo.py*
脚本来可视化结果。对于此步骤，您必须安装[pyrender](https://pyrender.readthedocs.io/en/latest/index.html)和[trimesh](https://trimsh.org/)包。

`python examples/demo.py --model-folder $SMPLX_FOLDER --plot-joints=True --gender="neutral"`

![SMPL-X 示例](./images/example.png)

## 修改模型的全局姿态

如果要修改模型的全局姿态，例如，根旋转和
平移到新的坐标系，例如，您需要考虑到
模型旋转使用骨盆作为旋转中心。更详细的描述可
在此[链接](https://www.dropbox.com/scl/fi/zkatuv5shs8d4tlwr8ecc/Change-parameters-to-new-coordinate-system.paper?dl=0&rlkey=lotq1sh6wzkmyttisc05h0in0)中找到。
如果有什么不清楚的地方，请告诉我，以便我可以更新
描述。

## 引用

根据您项目中加载的模型，即SMPL-X或SMPL+H或SMPL，请按以下顺序引用最相关的作品：

```
@inproceedings{SMPL-X:2019,
    title = {Expressive Body Capture: 3D Hands, Face, and Body from a Single Image},
    author = {Pavlakos, Georgios and Choutas, Vasileios and Ghorbani, Nima and Bolkart, Timo and Osman, Ahmed A. A. and Tzionas, Dimitrios and Black, Michael J.},
    booktitle = {Proceedings IEEE Conf. on Computer Vision and Pattern Recognition (CVPR)},
    year = {2019}
}
```

```
@article{MANO:SIGGRAPHASIA:2017,
    title = {Embodied Hands: Modeling and Capturing Hands and Bodies Together},
    author = {Romero, Javier and Tzionas, Dimitrios and Black, Michael J.},
    journal = {ACM Transactions on Graphics, (Proc. SIGGRAPH Asia)},
    volume = {36},
    number = {6},
    series = {245:1--245:17},
    month = nov,
    year = {2017},
    month_numeric = {11}
}
```

```
@article{SMPL:2015,
    author = {Loper, Matthew and Mahmood, Naureen and Romero, Javier and Pons-Moll, Gerard and Black, Michael J.},
    title = {{SMPL}: A Skinned Multi-Person Linear Model},
    journal = {ACM Transactions on Graphics, (Proc. SIGGRAPH Asia)},
    month = oct,
    number = {6},
    pages = {248:1--248:16},
    publisher = {ACM},
    volume = {34},
    year = {2015}
}
```

此存储库最初是为SMPL-X / SMPLify-X (CVPR 2019)开发的，您可能有兴趣查看：[https://smpl-x.is.tue.mpg.de](https://smpl-x.is.tue.mpg.de)。

## 致谢

### 面部轮廓

特别感谢[Soubhik Sanyal](https://github.com/soubhiksanyal)分享用于面部
标记的Tensorflow代码。

## 联系方式

此存储库的代码由[Vassilis Choutas](vassilis.choutas@tuebingen.mpg.de)实现。

如有问题，请联系[smplx@tue.mpg.de](smplx@tue.mpg.de)。

对于商业许可(以及所有商业应用的相关问题)，请联系[ps-licensing@tue.mpg.de](ps-licensing@tue.mpg.de)。