# VideoFlow based video frame interpolation
## Introduction
This is a video frame interpolation algorithm implemented using [VideoFlow](https://github.com/XiaoyuShi97/VideoFlow), which uses multiple frame inputs and ranked first in [Sintel Clean](http://sintel.is.tue.mpg.de/quant?metric_id=0&selected_pass=1).

---

**2023-10-04: We have updated an anime model and trained it for 60 epochs on our proprietary dataset, and we will soon release a new model that can better gather spatiotemporal information.**

---

## CLI Usage

### Installation

```
git clone https://github.com/hyw-dev/VFSS.git
cd VFSS
pip3 install -r requirements.txt
```

* Download the pretrained models from [here](https://drive.google.com/drive/folders/14ipRJCDBaiS1JUW-iGetTzAXgdeLVTB0?usp=sharing). 
* Move the 'anime' and 'real' folders to train_log/\*

### Run

You can use [demo video](https://drive.google.com/file/d/1i3xlKb7ax7Y70khcTcuePi6E7crO_dFc/view?usp=sharing) or your own video. 
```
python3 inference_video.py --exp=1 --video=video.mp4 --model_type [anime/real]
```
(generate video_2X_xxfps.mp4)
```
python3 inference_video.py --exp=2 --video=video.mp4 --model_type [anime/real]
```
(for 4X interpolation)
```
python3 inference_video.py --exp=1 --video=video.mp4 --scale=0.5 --model_type [anime/real]
```
(If your video has very high resolution such as 4K, we recommend set --scale=0.5 (default 1.0). If you generate disordered pattern on your videos, try set --scale=2.0. This parameter control the process resolution for optical flow model.)
```
python3 inference_video.py --exp=2 --img=input/ --model_type [anime/real]
```
(to read video from pngs, like input/0.png ... input/612.png, ensure that the png names are numbers)
```
python3 inference_video.py --exp=2 --video=video.mp4 --fps=60 --model_type [anime/real]
```
(add slomo effect, the audio will be removed)
```
python3 inference_video.py --video=video.mp4 --montage --png --model_type [anime/real]
```
(if you want to montage the origin video and save the png format output)

## Training
Download [Vimeo90K dataset(septuplet)](http://toflow.csail.mit.edu/index.html#septuplet).

We use 1xV100 for training **(Note that our real model only trained 12 epoch on the vimeo septuplet)**: 
```
python train.py
```

## Reference

Optical Flow:
[VideoFlow](https://github.com/XiaoyuShi97/VideoFlow)

Video Interpolation: 
[GMFSS](https://github.com/98mxr/GMFSS_Fortuna)   [RIFE](https://github.com/megvii-research/ECCV2022-RIFE)   [softsplat](https://github.com/sniklaus/softmax-splatting)

## Acknowledgment
This project is sponsored by [SVFI](https://steamcommunity.com/app/1692080) [Development Team](https://github.com/Justin62628/Squirrel-RIFE)
