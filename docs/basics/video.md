Here's a breakdown of the basic video customization features on the MiSTer. You can change your resolution, modify the framebuffer to reduce input latency and video stuttering, add some video filters, use shadowmasks, and even gamma correction. Also, you can use 5x overscan mode to push a 1200p image into 1080p for square pixels and nearly the original overscan of a CRT, depending on the game's resolution. There are lots of options to play with, here's some basic ones.

## MiSTer Ini Video Settings

In the `MiSTer.ini` file there are lots of video setttings to mess with. We'll just focus on a couple here for now and you can dive deeper in the [Advanced - Video](../advanced/video.md) section.

First, you can edit the settings in the `MiSTer.ini` file with windows Notepad, Visual Studio Code, Notepad++. Pretty much any text editor will be fine. Alternatively you can run the `ini-settings.sh` script in the scripts folder, this has a simple interface to change options.

### video_mode

A bit of a ways down the .ini file there is a `video_mode` option. Above it the resolutions are commented:

```
; 0 - 1280x720@60
; 1 - 1024x768@60
; 2 - 720x480@60
; 3 - 720x576@50
; 4 - 1280x1024@60
; 5 - 800x600@60
; 6 - 640x480@60
; 7 - 1280x720@50
; 8 - 1920x1080@60
; 9 - 1920x1080@50
;10 - 1366x768@60
;11 - 1024x600@60
;12 - 1920x1440@60
;13 - 2048x1536@60
```

This tells you that `video_mode=0` will set you to 1280x720 resolution at 60hz. For most people they will probably want to use 1920x1080 resolutiono at 60hz, so my advice would be to change this to `video_mode=8`. In the `ini-settings.sh` script it tells you what option does what resolution, so just select the right one for your display.

### vsync_adjust

Another important option is `vsync_adjust`. Most modern displays work fine at 60hz, but some games run at 60.6 hz (like Donkey Kong for the arcades) which is a "non-standard refresh rate". Therefore, MiSTer has what is called a "framebuffer". The game is still running at 60.6hz but the frames are sent at 60hz. So occasionally there is a little "stutter" on the screen to make up for the frames going too fast and being adjusted. To use a framebuffer adds lag, on the MiSTer it is typically about 2-3 frames of lag if you use the most compatible 60hz only option. here's a list of the options and what they do.

```ini
vsync_adjust=0 ; This matches the refresh rate of your monitor (e.g. 60hz) and has about 2-3 frames of lag. Video output can be somewhat jittery.
vsync_adjust=1 ; This makes the video output at exactly the frame rate of the game (e.g. 60.6hz). It has 1 frame of lag, but it is less compatible with modern televisions. Video output is very smooth
vsync_adjust=2 ; This makes the video output draw to the screen as fast as possible (sorta), and can result in sub-frame lag consistently. However this is the least compatible mode. The video output is the most smooth.
```

Generally the rule of thumb is, start at `vsync_adjust=2`, and if a core doesn't work taht you want to play on, then dial it back. 

### Core exceptions

There are also ways to add exceptions. My monitor doesn't play nice with the low lag setting on the Genesis core. So in my MiSter.ini, I added the following override/exception for just the MiSTer core:

```ini
[Genesis]
vsync_adjust=0
```

This makes it so no matter what my `vsync_adjust` setting is in the upper section, when I use the Genesis core, it will force it to use `vsync_adjust=0` (the most compatible mode) every time.

## Filters (and scanlines)

MiSTer has the capability to use upscaling filters and scanlines to help enhance the video output or even make it feel similar to a retro CRT television. If you opened the NES core for the first time after setting the MiSter's video output to 1920x1080p and loaded up Duck Tales, then you should see something like this:

![Duck Tales NES MiSTer FPGA 1920x1080@60 Default Video Output](img/default-video-nes.png)

This can be tweaked a little to make it look a lot nicer to our eyes. First let's go into "Video Processing" in the secondary OSD/Menu (press F12 or the menu button you assigned earlier, and then right to see the secondary menu):

![MiSTer FPGA Video Processing options selection](img/video-processing.png)

When you select this it will show you a screen with a bunch of options. Don't get overwhelmed, it's fairly simple when you follow this guide, and you will understand how they work. I'll give you some recommended settings for most of the cores at the end of this tutorial which should be your go-to for now while you get used to things.

By default "Video Filter:" is set to "NearNeighbour". This is a nearest neighbour filter. Basically, to turn 240p video into 1080p video requires these pixels to be made larger. Since 240 doesn't divide evenly into 1080 (1080 / 240 = 4.5), then some of these pixels won't be perfectly square. Nearest neighbour helps fool your eyes into making them seem more square than they actually are. It's filtering the video before it reaches your eyes to make it look better! 

Select Video filter to change it so you can select a filters file. You will notice the text changes from `Video Filter:` to `Horz filter:`. Don't worry about this too much, for any normal rotation games, Horz is for your upscaling filters that soften or sharpen the image.

Select the `<none>` below to browse. It should show you quite a few options. For now select `Interpolation (Medium).txt`. This is a filter which gives you some softer edges while still maintaining an illusion of square pixels.

![MiSTer FPGA Horizontal Interpolation filter horz filter:](img/horz-filter.png)

There we go, those pixels are a bit smoother now:

![Mister FPGA Horizontal Interpolation Medium filter horz filter: NES duck tales](img/interpolation-medium.png)

Another added benefit to interpolation is the scrolling looks smoother to the eye when compared to sharper filters like the default Nearest Neighbour setting.

Now let's say you want some scanlines, sorta like what CRT's had and some emulators have an option for. Well to do that, we just need to setup the `Vert Filter:` option like we did the horz filter. You see, we will be filtering horizontal lines from top to bottom (vertically) on the video output. Inside `Vert Filter`'s `From File` option, select `Scanlines - Brighter.txt`. You should see something like this as your options:

![MiSTer FPGA's Vertical filter Scanlines - Brighter vert filter](img/scanlines-brighter.png)

## 5x Vertical Crop

**Note: this feature only works if your output resolution in your MiSTer.ini is set to a 1080p option!!** 

If you have been following along on your MiSTer, you might notice that the scanlines look darker occasionally. This is because 240p (this game's resolution) doesn't divide equally into 1080p (your resolution on your MiSTer). But 240 does divide into 1200 equally, 5 times 240 equals 1200. So to fix these scanlines looking uneven, we can stretch the image vertically to make all the pixels perfectly square. Go back into the regular core menu and select `Video & Audio`. There is an option called `Vertical Crop`. Not all cores have this, but the NES core does happen to, so it's a good example. Go ahead and select the `Vertical Crop` option to change `Disabled` to `(216p)5X`. 

![MiSTer FPGA Vertical Crop 5x mode 1080p to 1200p 216p to 5x with overscan](img/5x-vertical-crop.png)

You will see just a few lines off the top and bottom get cut off. This is okay, original CRT's cut off about the same amount from the top and bottom anyways. Most games don't have information missing at the edge of the top and bottom.

Now your `vert filter: scanlines - brighter.txt` option should have evenly spaced scanlines vertically, and the image will look a lot better.

## Shadowmasks

MiSTer FPGA also has another layer options available to use called `Shadowmasks`. These attempt to simulate the appearance of the grille or mask on an old CRT screen. There are lots of options, but we are just going to use personally one of the most versatile color shadowmasks for this tutorial, `Squished VGA Bright v2.txt`. This shadowmask attempts to resemble consumer computer monitors and some tv's which had red, green, and blue phosphors in a particular pattern. Here is a picture of the options after I've added this Shadowmask to the same game's video processing menu:

[![MiSTer FPGA Shadowmasks / Shadow Masks Squished VGA Bright v2.txt 1200p 5x overscan to 1080p with scanlines - brighter.txt](img/squished-vga-bright-v2.txt)](img/squished-vga-bright-v2.txt){target=_blank}

## Gamma

Gamma is a bit of a tricky thing to explain. Basically, gamma on an old CRT is the relationship between voltage and brightness. Think of a graph, the x-axis is voltage and the y-axis is the brightness. Modern televisions are (ideally) a totally straight line. Old CRT's have a curve. At lower voltage it is a lot less brightness than you'd expect. And at higher voltage, it's a lot higher than you'd expect. And typically, in the mid-range it's about the same or lower.




* Brief description of subjects
* Scaler setup: latency and resolution
* Scanlines and shadowmasks
* Gamma
* 5x mode ("requires 1080p", etc...)

## 5x mode video
![type:video](videos/5x.mp4)]

## gamma controls video
![type:video](videos/gamma.mp4)
