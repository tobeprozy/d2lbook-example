# StableDiffusionV1.5

## 目录
* [1. 简介](#1-简介)

* [2. 准备模型](#2-准备模型)

  ​    [2.1 自己下载并且编译模型](2.1 自己下载并且编译模型)
  
  ​    [2.2 使用准备好的模型文件](2.2 使用准备好的模型文件)

* [3. 程序运行](#3-程序运行)

  ​    [3.1-python](#3.1-python)

## 1. 简介
StableDiffusion 是开源AIGC模型(Huggingface官网：https://huggingface.co/runwayml/stable-diffusion-v1-5），可以用来生成各种各样的图像内容。

该例程可以在x86和盒子上正常运行，目前只提供了python版本

## 2. 准备模型
该模型目前只支持在1684X上运行，模型来源于开源的Huggingface，可以在scirpt目录下运行 get_model_fromHuggingface.py 将模型从Huggingface下载 (下载前请先安装requirements.txt里
对应的包：pip3 install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple)

## 2.1 自己下载并且编译模型
之后在script路径下运行 export_pt_from_Huggingface.py 即可将Huggingface上pipeline中的模型以pt/onnx的方式存在本地路径下；

模型编译前需要安装TPU-MLIR，具体可参考[TPU-MLIR环境搭建](../../docs/Environment_Install_Guide.md#1-tpu-mlir环境搭建)。安装好后需在TPU-MLIR环境中进入例程目录。使用TPU-MLIR将onnx模型编译为BModel，具体方法可参考《TPU-MLIR快速入门手册》的“3. 编译ONNX模型”(请从[算能官网](https://developer.sophgo.com/site/index/material/31/all.html)相应版本的SDK中获取)。

最后参考TPU-MLIR工具的使用方式激活对应的环境，激活后运行script下的四个脚本文件（get_text_encoder_bmodel.sh， get_vae_encoder_bmodel.sh，get_vae_decoder_bmodel.sh
get_unet_bmodel.sh），会将当前路径下的onnx/pt文件转换为bmodel。

## 2.2 使用准备好的模型文件
使用script路径下的download_singlize_bmodel.sh，运行结束后会在 ../models/singlize路径下创建出Stable Diffusion V1.5所需要的完整bmodels（位于../models/singlize/bmodels中）
同时也会将下载好的pt/onnx 文件放到../models/singlize/onnx_pt 中，用户可以使用准备好的bmodel，也可以运用MLIR工具自行编译onnx_pt中的模型。

除此之外，用户还可以使用script路径下的download_multilize_bmodel.sh，脚本执行完毕后，会在../models/multilize路径下生成bmodels和controlnet两个文件夹，并且存放了对应的bmodel文件。multilize和singlize的区别在于singlize只集成了512x512的输出图像，在multilize中集成了
[(768	768), (896	512), (512	896), (832	512), (512	832), (512	768), (768	512), (704	512), (512	704), ... （128 384)] 共计46钟不同尺度的输出，
并且适配了对应尺度下的controlnet模块。 由于多尺度的转换和controlnet的转换相对复杂，因此在本例程中只提供使用的demo，不提供如何转换的教程。

在script目录下执行两个download脚本后
当前目录下的文件如下：

```
.
├── models
│   └── singlize                            #singlize bmodel、pt/onnx 文件
│       ├── bmodels                         #singlize bmodel
│       └── onnx_pt                         #singlize pt/onnx 文件
│   └── multilize                           #multilize bmodel、controlnet 文件
│       ├── bmodels                         #multilize bmodel
│       └── controlnet                      #multilize controlnet
├── python
│   ├── run.py                           #主程序
│   ├── sd_engine.py                     #TPU engine
│   └── stable_diffusion.py              #SD的类文件 
├── README.md                            #使用说明
├── requirements.txt                     #所需依赖的包
└── script
    ├── get_model_fromHuggingface.py                 #从Huggingface下载模型
    ├── export_pt_from_Huggingface.py                #Huggingface模型转为pt/onnx模型
    ├── get_text_encoder_bmodel.sh                   #text_encoder bmodel生成脚本
    ├── get_unet_bmodel.sh                           #unet bmodel 生成脚本
    ├── get_vae_decoder_bmodel.sh                    #vae decoder bmodel 生成脚本
    ├── get_vae_encoder_bmodel.sh                    #vae encoder bmodel 生成脚本
    ├── download_multilize_bmodel.sh                 #multilize模型下载脚本
    └── download_singlize_bmodel.sh                  #singlize模型下载脚本
```

## 3. 程序运行

本例程只包含python版本，在x86上需要配置好sophon sdk环境，在soc上由于环境已经配置完毕，可以直接使用。两者使用方式相同

## 3.1 python
```
cd python
```
执行程序：
```
python3 run.py
```