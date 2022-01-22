The [MiSTer.ini configuration file](https://github.com/MiSTer-devel/Main_MiSTer/blob/master/MiSTer.ini){target=_blank} contains global settings and is capable of storing core-specific settings for the MiSTer. We'll go over each of the Global settings here and then show you how to make exceptions for those global settings for each core. Then we'll describe some core-specific settings that can be used for core exceptions only.

## Video Ini Settings

`forced_scandoubler` - VGA output will always run in 31kHz mode (scandoubled) if this setting is turned on, useful for computer CRT's.

`ypbpr` - Changes the VGA output to a YPbPr signal.

`composite_sync` - Sends the sync signal on Hsync over VGA output, needed for certain configurations.

`vga_scaler` - Sends the scaler output to the VGA port (either Analog IO or Direct Video). This is usually used with computer CRTs and other 31kHz displays which are not compatible with 240p TV signals.

`video_mode` - Sets the resolution for HDMI and VGA_Scaler

## Audio Ini Settings

`hdmi_audio_96k` - Changes the HDMI audio sampling rate from 48kHz (default) to 96kHz. This can help with the audio of some systems that have strange sampling rates (like Turbografx-16's sampling rate of 32.088kHz for instance).

## 
