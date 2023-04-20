# HaloUpscaleProject

This project is dedicated towards using AI to upscale old Halo videos so that they can be a just a little bit easier to watch. 

## Updates

2023.04.20 - Posted h1v1 model. Updated readme. 

## How does this work?

What I have done is create custom trained [Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN) models based on Halo specific footage. In general what I have done is captured MCC gameplay on my computer at 4K saving the footage at very high bitrates and very low framerates (think 20MB/s 5fps). If you have extremely high quality 4K footage of halo gameplay, please let me know! Training these models requires extremely large datasets and I don't have a lot of free time to play and genere them myself.
 
## Halo 1

The first version of this model takes 320x240 images and upscales them to 1280x960 images. It was trained on 87,000 images across all maps. 

[HUPcy_h1v1.7z](https://drive.google.com/file/d/1u90t0iXwnQX-yv7WudV1TxcLgG0zqfAj/view?usp=sharing)
