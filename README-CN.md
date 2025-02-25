### ComfyUI_AnyDoor  
你可以使用阿里出品的anydoor 传送门，换衣服，移挪物体等等。。   

AnyDoor的官方地址: [AnyDoor](https://github.com/ali-vilab/AnyDoor)   
----

Tips：    
目前物体遮罩位置的注入没有好的适配节点，迟点新增一个。 
因为魔搭的需求很低，会间接影响其他库，所以最好是直接下载模型文件。
----

1.安装
---
  在ComfyUI的custom_node目录下：  
```
git clone https://github.com/smthemex/ComfyUI_AnyDoor.git
```
或者使用 ComfyUI-Manager 

2.需求文件    
---
```
pip install -r requirements.txt
```
如果安装不了或者提示库缺失，改名 "for_modules_miss_requirements.txt"为 requirements.txt    
然后pip install -r requirements.txt    
这个方法我不大推荐，建议按以下方法 直接安装缺失的库。。 
"pip install missing module"   

3  必须的模型文件   
---
*模型一：*   

<在线模式>    
首次运行会自动下载，因为模型都不在抱脸上，所以会走国内的魔搭社区，自动下载模型。    

<离线模式>   

--如果使用 "origin" 模型，会下载"epoch=1-step=8687.ckpt"(16.8G) : [link](https://huggingface.co/spaces/xichenhku/AnyDoor/tree/main)          
--如果使用 "pruned" 模型，会下载 "epoch=1-step=8687-pruned.ckpt"(4.9G) : [link](https://modelscope.cn/models/bdsqlsz/AnyDoor-Pruned/files)    

*模型二：*   

<在线>   
首次运行会自动下载，因为模型都不在抱脸上，所以会走国内的魔搭社区，自动下载模型。    

<离线>    
--在国内下载 "dinov2_vitg14_pretrain.pth"(4.5G) :[link](https://modelscope.cn/models/bdsqlsz/AnyDoor-Pruned/files)   
or   
--或者在这里（外网）下载 "dinov2_vitg14_pretrain.pth"(4.5G) :[link](https://github.com/facebookresearch/dinov2?tab=readme-ov-file)      

--模型文件的存放目录构成如下:  

```
├── ComfyUI/models/
|      ├──anydoor/
|             ├── dinov2_vitg14_pretrain.pth
|             ├── epoch=1-step=8687.ckpt  (选择origin时)
|             ├── epoch=1-step=8687-pruned.ckpt  (选择pruned时))
```
4使用说明：
--
4.1 image和image_mask 是你要转移的物体，bg_image 和bg_mask是出图的背景，也就是主图;    
4.2 seed 目前是无效的；  
4.3 虽然也可以用comfyUI自带的蒙版，我还是建议用seg 或者sam;     
4.4 如果显存不够，可以考虑开启save_memory;   
4.5 use_interactive_seg 会对mask再次处理，除非你是手动画蒙版，一般不建议打开；      
4.6 模型训练最大是768*768，所以image不建议用超大的图；  
4.7 工作流文件在examples文件夹下； 
4.8 蒙版图片输入的时候，请确保你要替换的物体选区是白色的，然后不想替换的地方是黑色的。      

5 示例
---

示例图片采样了SAM，也就是脱底模型，你可以用你自己喜欢的，但是要注意目标选区是白色的。   
![](https://github.com/smthemex/ComfyUI_AnyDoor/blob/main/examples/example.png)


Citation
---
特别致谢： [青龍聖者@bdsqlsz](https://github.com/sdbds) 的“poch=1-step=8687-pruned.ckpt” 模型

AnyDoor
``` python  
@article{chen2023anydoor,
  title={Anydoor: Zero-shot object-level image customization},
  author={Chen, Xi and Huang, Lianghua and Liu, Yu and Shen, Yujun and Zhao, Deli and Zhao, Hengshuang},
  journal={arXiv preprint arXiv:2307.09481},
  year={2023}
}
```

Citing DINOv2
```python
@misc{oquab2023dinov2,
  title={DINOv2: Learning Robust Visual Features without Supervision},
  author={Oquab, Maxime and Darcet, Timothée and Moutakanni, Theo and Vo, Huy V. and Szafraniec, Marc and Khalidov, Vasil and Fernandez, Pierre and Haziza, Daniel and Massa, Francisco and El-Nouby, Alaaeldin and Howes, Russell and Huang, Po-Yao and Xu, Hu and Sharma, Vasu and Li, Shang-Wen and Galuba, Wojciech and Rabbat, Mike and Assran, Mido and Ballas, Nicolas and Synnaeve, Gabriel and Misra, Ishan and Jegou, Herve and Mairal, Julien and Labatut, Patrick and Joulin, Armand and Bojanowski, Piotr},
  journal={arXiv:2304.07193},
  year={2023}
}
```

```python
@misc{darcet2023vitneedreg,
  title={Vision Transformers Need Registers},
  author={Darcet, Timothée and Oquab, Maxime and Mairal, Julien and Bojanowski, Piotr},
  journal={arXiv:2309.16588},
  year={2023}
}
```
