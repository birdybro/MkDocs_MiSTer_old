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

MiSTer has the capability to use upscaling filters and scanlines to help enhance the video output or even make it feel similar to a retro CRT television.





* Brief description of subjects
* Scaler setup: latency and resolution
* Scanlines and shadowmasks
* Gamma
* 5x mode ("requires 1080p", etc...)

## 5x mode video
![type:video](videos/5x.mp4)]

## gamma controls video
![type:video](videos/gamma.mp4)
