# HaloUpscaleProject

![Before vs After](https://raw.githubusercontent.com/CYRiXplaysHalo/HaloUpscaleProject/main/main.png)

This project is dedicated towards using AI to upscale old Halo videos so that they can be a just a little bit easier to watch. You can see the end results on this YouTube channel: https://www.youtube.com/@HaloUpscaleProject

## How does this work?

What I have done is create custom trained [Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN) models based on Halo specific footage. In general what I have done is captured MCC gameplay on my computer at 4K saving the footage at very high bitrates and very low framerates (think 20MB/s 5fps). If you have extremely high quality 4K footage of halo gameplay, please let me know! Training these models requires extremely large datasets and I don't have a lot of free time to play and genere them myself.
 
## How can I run this myself?


These are custom Real-ESRGAN models, so you need to set up an environment that has Real-ESRGAN installed. [Instructions to do that are here](https://github.com/xinntao/Real-ESRGAN#-dependencies-and-installation). 

The approach I have been taking is taking a video, extracting every single frame via ffmpeg like so:

`ffmpeg -i VIDEO_FILE_NAME.mp4 -q:v 1 -qmin 1 -qmax 1 FOLDER_NAME/%0d.png`

That extracts every single frame as a PNG image and is numbered incrementally with 8 leading zeroes. Once you've done that and you've installed Real-ESRGAN you can then run my custom model on that folder of images to generate a new folder of 4x upscaled images like so:

`python inference_realesrgan.py -n RealESRGAN_x4plus --model_path PATH_OF_MODEL/net_g_latest.pth -i INPUT_FOLDER_FULL_PATH -o OUTPUT_FOLDER_FULL_PATH`

That should take some period of time, depending upon your setup. Once it's complete you can then use ffmpeg again to create a video from the series of upscaled output images:

`ffmpeg -framerate FRAME_RATE_NUM -pattern_type glob -i "OUTPUT_FOLDER_FULL_PATH/*.png" -vf format=yuv420p -movflags +faststart UPSCALED_OUTPUT_FILENAME.mp4`

You might also want to add in the original audio track, to do that first extract the audio track from the original video:

`ffmpeg -i ORIGINAL_INPUT_VIDEO.mp4 -c copy -vn ORIGINAL_INPUT_AUDIO.m4a`

Make sure you know what encoders and containers you're working with, otherwise ffmpeg might not be able to extract the audio file properly. So now that you have the extracted audio track, assuming you have generated an upscaled output video with the correct framerate, then you can combine the two like so:

`ffmpeg -i ORIGINAL_INPUT_AUDIO.m4a -i UPSCALED_OUTPUT_FILENAME.mp4 -c copy UPSCALED_OUTPUT_WITH_AUDIO.mp4`

And that's it! You've upscaled an old halo video which makes you an awesome person. Please share the results with me!

Now what I end up doing is using VirtualDub to generate a video file from the upscaled output image folder so I can do things like crop black space, correct colorspace, etc. For the videos I'm uploading to YouTube I am simple saving the video via VirtualDub using the lagarith lossless codec at 960p, and letting YouTube compress that down to 720p. I'm aware this might not be the most optimal approach so feel free to make suggestions.


## Halo 1

The first version of this model takes 320x240 images and upscales them to 1280x960 images. It was trained on 87,000 images across all maps. Eventually I will upload the image datasets as well.

[HUPcy_h1v1.7z](https://drive.google.com/file/d/1u90t0iXwnQX-yv7WudV1TxcLgG0zqfAj/view?usp=sharing) | [Dataset](https://archive.org/details/hupcy_h1v1-dataset)

## Updates

2023.04.20 - Posted h1v1 model. Updated readme. 
