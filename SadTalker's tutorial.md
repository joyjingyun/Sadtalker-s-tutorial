# SadTalker部署教程

## 一、环境配置

### 新建虚拟环境

- 打开anaconda的Powershell Plompt,conda 创建虚拟环境(sadtalker是你的虚拟环境的名字，python版本为3.8)

```
conda create -n sadtalker python=3.8
```

### github克隆项目

- 在D盘中新建文件夹用来存放你的项目
- 链接打开项目地址：[(https://github.com/OpenTalker/SadTalker)](https://github.com/OpenTalker/SadTalker)

- 点击Code,点击复制的图标

![image](https://github.com/joyjingyun/Sadtalker-s-tutorial/blob/main/image/image-20230615221727366.png)

- 打开刚刚新建的文件夹，鼠标右击空白处，选择-显示更多选项-Git Bash Here

![image](https://github.com/joyjingyun/Sadtalker-s-tutorial/blob/main/image/image-20230615221940916.png)

- 输入git clone 然后右键点击paste

![image](https://github.com/joyjingyun/Sadtalker-s-tutorial/blob/main/image/image-20230609141636697.png)

![image](https://github.com/joyjingyun/Sadtalker-s-tutorial/blob/main/image/image-20230615222205842.png)

- 看到100%就表示克隆成功了



### pythorch安装（gpu版本）

- 在anaconda中激活虚拟环境输入以下命令

```
conda install pytorch==1.12.1 torchvision==0.13.1 torchaudio==0.12.1 cudatoolkit=11.3 -c pytorch
```

注意：这将安装 PyTorch 1.12.1，同时显式指定使用的 CUDA 版本为 11.3。`-c pytorch` 会添加 PyTorch 官方的 conda 频道.

这里可能会出现的问题是pythorch和cuda版本不匹配

可以在https://pytorch.org/官网上找到你的cuda版本所对应的pytorch版本

- 安装完后，你需要测试一下

![image](https://github.com/joyjingyun/Sadtalker-s-tutorial/blob/main/image/image-20230615223350028.png)

### 安装依赖

- 在虚拟环境里进入项目所在文件夹

![image](https://github.com/joyjingyun/Sadtalker-s-tutorial/blob/main/image/image-20230615224035429.png)

- 输入以下命令

```
conda install ffmpeg
pip install -r requirements.txt
```

## 二、下载训练模型（checkpoints和gfpgan权重）

- 下载官方给的预训练模型

![image](https://github.com/joyjingyun/Sadtalker-s-tutorial/blob/main/image/image-20230615225716907.png)

- 解压后放在项目所在的文件夹

![image](https://github.com/joyjingyun/Sadtalker-s-tutorial/blob/main/image/image-20230615231000274.png)

- 输入以下代码，查看虚拟环境的路径

```
conda info
```

- 把D:\pyproject\SadTalker\gfpgan\weights目录下的GFPGANv1.4pth剪切到虚拟环境的Lib\site-packages\gfpgan\weights目录下



## 三、测试

- 把你的语音文件放到SadTalker\examples\driven_audio目录下

- 音频文件可以在以下网址通过你输入的文字合成语音

https://ttsmaker.com/zh-cn

https://remeins.com/index/app/text2voice

- 把图片放到SadTalker\examples\source_image目录下

- 图片可以用AI绘画把人脸图更加3D化

![image](https://github.com/joyjingyun/Sadtalker-s-tutorial/blob/main/image/1687013041622.jpg)

![image](https://github.com/joyjingyun/Sadtalker-s-tutorial/blob/main/image/1687013041608.webp)



- result_dir是结果输出的文件夹
- 输入以下命令开始运行

```
python inference.py --driven_audio D:\pyproject\SadTalker\examples\driven_audio\vedio5.mp3 --source_image D:\pyproject\SadTalker\examples\source_image\image3.webp --result_dir D:\pyproject\SadTalker\output --enhancer gfpgan
```



- 看到以下界面表示训练成功，现在可以在D:\pyproject\SadTalker\output文件夹里看到你的成果了！

![image](https://github.com/joyjingyun/Sadtalker-s-tutorial/blob/main/image/image-20230616083906119.png)



- 输入以下命令还可以生成自然的全身视频

```
python inference.py --driven_audio <audio.wav> \
                    --source_image <video.mp4 or picture.png> \
                    --result_dir <a file to store results> \
                    --still \
                    --preprocess full \
                    --enhancer gfpgan 
```

- 看到以下界面就表示成功了

![image](https://github.com/joyjingyun/Sadtalker-s-tutorial/blob/main/image/image-20230619230259026.png)

- 效果视频展示

![image](https://github.com/joyjingyun/Sadtalker-s-tutorial/blob/main/image/image-20230619230440226.png)

- 最后测试环节可能会出现的问题是缺少Pillow库中的Imaging模块

```
ImportError: DLL load failed while importing _imaging: 找不到指定的模块。
```

解决方法是卸载旧版本的pillow库，重新执行pip
