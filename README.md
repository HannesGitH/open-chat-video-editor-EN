# Open Chat Video Editor

## Introduction

Open Chat Video Editor is an open source short video generation and editing tool with the following overall technical framework:

![sys中文](https://user-images.githubusercontent.com/21036347/236475457-e6104baa-11c2-4fe9-88b3-f328114d0076.png)

## TODO

- [x] **windows, linux different systems more convenient install guidelines**
- [x] **Create docker, easy for everyone to use with one click**
- [ ] **The url that can be experienced directly and quickly online**
- [ ] finetune text model on short video copy data, support more copy styles
- [ ] finetune SD model, enhance the image and video generation effect

Currently has the following features:

- 1) **One-click generation of usable short video**, including: voiceover, background music, subtitles, etc.

- 2) Algorithms and data are based on open source projects, facilitating technical exchange and learning
- 3) Support a variety of input data, convenient for a wide variety of data, one click to short video, currently supports:
  - [x] **short sentences to short video** (Text2Video): according to the short text input, generate short video copy, and synthesize short video
  - [ x ] **Web Link to Short Video** (Url2Video): automatically extract the content of web pages, generate video copy, and generate short videos
  - [ ] **Long Video to Short Video** (Long Video to Short Video): Analyze and summarize the input long video, and generate short video
- 4) Cover a variety of mainstream algorithms and models such as **generative model** and **multimodal retrieval model**, such as: Chatgpt, Stable Diffusion, CLIP, etc.

For text generation, it supports:

- [x] ChatGPT
- [ ] BELLE
- [ ] Alpaca
- [ ] Dolly
and other models

For visual information generation, both image and video modalities are supported, and for generation, both retrieval and generation models are supported, currently there are 6 models:

- [x] image retrieval
- [x] image generation (stable diffusion)
- [x] image retrieval, then image generation based on stable diffusion
- [x] video retrieval
- [ ] Video generation (stable diffusion)
- [ ] Video retrieval followed by video generation based on stable diffusion

## Result display

### 1、Phrase to short video (Text2Video)

The interface is as follows.
![text2video](https://user-images.githubusercontent.com/21036347/236427963-7e9a166b-c085-4af8-b691-5a67f3e865e5.png)
Take the input text: [children with pets] as an example, using the text model (such as: chatgpt, etc.), a longer short video text can be automatically generated as follows:

```
[Children with pets', 'can better enhance the sense of responsibility and independence of children', 'but also to carefully choose the right pet', 'because only after a certain training to raise', 'they can grow up', 'play together and spend a happy time', 'pets can not only accompany children through the lonely time', 'but also to develop children to deal with calm, confident and In the process of having a pet,' 'children can awaken and discover their honed perseverance and endurance' and 'experience firsthand the importance of diligence and persistence.] 
```

According to different video generation modes, different videos can be generated, and the comparison of each mode is as follows.

 **1) Image retrieval**

<https://user-images.githubusercontent.com/21036347/236428839-9c3c3a2d-6163-4577-82f5-5815772f294f.mp4>

**2) Image generation (stable diffusion)**

<https://user-images.githubusercontent.com/21036347/236429111-b151f3b5-64d0-4572-8daa-29a78a3d1f3d.mp4>

**3) Image retrieval first, then image generation based on stable diffusion**

<https://user-images.githubusercontent.com/21036347/236429690-93ea7377-e233-4629-868f-ef953a4dfa4c.mp4>

**4) Video retrieval**

<https://user-images.githubusercontent.com/21036347/236430102-6054b28c-ebeb-42a2-880e-b2656fc32138.mp4>

### 2、Webpage to short video (Url2Video)

The interface is as follows:

![url2video](https://user-images.githubusercontent.com/21036347/236430693-fe9b3d15-8da8-4a50-b7a9-b4dc93614076.png)

1) Enter a url, for example: <https://zh.wikipedia.org/wiki/%E7%BE%8E%E5%9B%BD%E7%9F%AD%E6%AF%9B%E7%8C%AB>
Its content is: Wikipedia of American Shorthair Cat

![wiki](https://user-images.githubusercontent.com/21036347/236431138-5fbb6cf2-07c8-41a3-989d-64731a6891d4.png)

2) Parse the page and automatically summarize it into a short video text, the result is as follows:

```
['\n\n American Shorthair', 'a magical and magical breed of pet cat', 'they are elegant and cute', 'incredibly energetic', 'can have up to 80 different head coat colors', 'the most famous is the silver tiger spot', 'its silver coat has a thick black spotting 
'in addition to this', 'they are also very gentle', 'make great family and human pets', 'and have an average lifespan of 15-20 years', 'this lovely cat 
This cute breed of cat', 'is becoming more and more popular', 'Why don't you try getting one too']
```

3) Automatically composing short videos
For example, the results generated in image generation mode are as follows, other modes will not be compared one by one

<https://user-images.githubusercontent.com/21036347/236431745-9f61ebcc-91b5-4157-adf9-abf9c371e461.mp4>

### 3、Long video to short video (Long Video to Short Video)

**To be released soon, stay tuned**

## Installation and use

### Environment installation

According to different needs, choose different installation methods 1, 2, and 3, either one of them.

#### 1、Docker

The current docker environment is not guaranteed to work properly with GPU because everyone's cuda version may be different. However, docker is relatively large and needs to take up more storage (24G).

```
docker pull iamjunhonghuang/open-chat-video-editor:retrival
docker run -it --network=host -v /YourPath/open-chat-video-editor:/YourPath/open-chat-video-editor/ iamjunhonghuang/open-chat-video- editor:retrival bash
conda activate open_editor
```

Or use the Aliyun mirror at

```
docker login --username=xxx registry.cn-hangzhou.aliyuncs.com
docker pull registry.cn-hangzhou.aliyuncs.com/iamjunhonghuang/open-chat-video-editor:retrival
docker run -it --network=host -v /YourPath/open-chat-video-editor:/YourPath/open-chat-video-editor/ registry.cn-hangzhou.aliyuncs.com/ iamjunhonghuang/open-chat-video-editor:retrival bash
conda activate open_editor
```

Note: Chinese subtitles are not supported at the moment, so you need to modify the font settings in the configuration file yaml, for example 'image_by_retrieval_text_by_chatgpt_zh.yaml'

```
  subtitle.
    font: DejaVu-Sans-Bold-Oblique
    # font: Cantarell-Regular
    # font: 华文細黑
```

#### 2、Linux (currently tested in centOS only)

1) first install the python environment based on conda, gcc version installation test is 8.5.0, so try to upgrade to 8 or more

```
conda env create -f env.yaml
conda env update -f env.yaml #If there is an error in the first line, you need to update the command used
```

2) Then install the environment dependencies, the main purpose is to install ImageMagick normally, other linux versions can refer to

```
# yum groupinstall 'Development Tools'
# yum install ghostscript
# yum -y install bzip2-devel freetype-devel libjpeg-devel libpng-devel libtiff-devel giflib-devel zlib-devel ghostscript-devel djvulibre-devel libwmf-devel jasper-devel libtool-ltdl-devel libX11-devel libXext-devel libXt-devel libxml2-devel librsvg2-devel OpenEXR-devel php-devel
# wget https://www.imagemagick.org/download/ImageMagick.tar.gz
# tar xvzf ImageMagick.tar.gz
# cd ImageMagick*
# . /configure
# make
# make install
```

3) You need to change the call path of moviepy, that is, change the following file

```
$HOME/anaconda3/envs/open_editor/lib/python3.8/site-packages/moviepy/config_defaults.py
```

Modify to

```
#IMAGEMAGICK_BINARY = os.getenv('IMAGEMAGICK_BINARY', 'auto-detect')
IMAGEMAGICK_BINARY='/usr/local/bin/magick'
```

4) Chinese subtitles are not supported at the moment, so you need to modify the font settings in the configuration file yaml, for example 'image_by_retrieval_text_by_chatgpt_zh.yaml'

```
  subtitle.
    font: DejaVu-Sans-Bold-Oblique
    # font: Cantarell-Regular
    # font: 华文細黑
```

#### 3. Windows

1) It is recommended to use python version 3.8.16:

```
conda create -n open_editor python=3.8.16
```

2) Install pytorch

```
# GPU version
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu117

# CPU version
pip3 install torch torchvision torchaudio

```

3) Install other dependencies

```pip install -r requirements.txt```

4) Install clip

```pip install git+<https://github.com/openai/CLIP.git```

5) Install faiss

```conda install -c pytorch faiss-cpu```

### Code execution

1) Select different configuration files according to actual needs

| configuration file | description |
| ---- | ---- |
| configs/text2video/image_by_retrieval_text_by_chatgpt_zh.yaml | short text to video, video text using chatgpt generation, visual part using image retrieval to generate |
| configs\text2video\image_by_diffusion_text_by_chatgpt_zh.yaml | short text to video, video text using chatgpt generation, visual part using image stable diffusion to generate |
configs\text2video\image_by_retrieval_then_diffusion_chatgpt_zh.yaml | short_text_to_video,\video_text_by_chatgpt_zh.yaml | short_text_to_video,\video_text_by_retrieval_then_diffusion_chatgpt_zh.yaml | short_text_to_video,\video_text_by_chatgpt_zh.yaml generate|
|configs\text2video\video_by_retrieval_text_by_chatgpt_zh.yaml|short_text_to_video, video_text_by_chatgpt_generation, visual_part_by_video_retrieval_to_generate|
| configs\url2video\image_by_retrieval_text_by_chatgpt.yaml | url to video, video text using chatgpt generation, visual part using image retrieval to generate|
| configs\url2video\image_by_diffusion_text_by_chatgpt.yaml|url-to-video,video_text_by_chatgpt,visual_parts_by_image_stable_diffusion to generate|
|configs\url2video\image_by_retrieval_then_diffusion_chatgpt.yaml|url-to-video,video_text_by_chatgpt,video_copy_by_chatgpt,visual_part_by_image_retrieval_then_diffusion_based_stable_diffusion_to_generate|
|configs\url2video\video_by_retrieval_text_by_chatgpt.yaml|url-to-video,video_text_by_chatgpt,video_by_retrieval_text_by_chatgpt.yaml|url-to-video,video_text_by_chatgpt,video_by_retrieval_text_by_chatgpt.yaml

**Note: If you want to use ChatGPT to generate the text, you need to add the organization_id (to be checked in the Organization settings, not directly enter "personal") and api_ key**

2) Download the data index and meta information [data.tar](https://pan.quark.cn/s/19fa46ceb2cb), and extract it to the data/index directory.

3) Execute the script

```
# Text to video 
python app/app.py --func Text2VideoEditor --cfg ${cfg_file}


# URL to video 
python app/app.py --func URL2VideoEditor --cfg ${cfg_file}

```

## Declaration

1. Data source
Image retrieval data from: [LAION-5B](https://laion.ai/blog/laion-5b/)

Video retrieval data from: [webvid-10m](https://m-bain.github.io/webvid-dataset/)

Please note that we do not own the copyright of the data

2. This project is only for communication and learning, not for commercial use, and other uses that will bring harm to society.

## Exchange and Learning

Welcome to communicate and learn with us through [Discard](https://discord.gg/yWt59JUd) or WeChat

Group 1 is full with 200 people.

The second group is full with 200 people.

The third group is full with 200 people.

The fourth group is full with 200 people.

Please join group 5: !

![image](https://github.com/SCUTlihaoyu/open-chat-video-editor/assets/26428693/a06ec564-cdd4-4470-ada6-b59ff99a8f6a)
