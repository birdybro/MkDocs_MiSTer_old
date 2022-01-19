MiSTer supports Cue/Bin and [CHD](https://github.com/rtissera/libchdr){target=_blank} formats. The way the MiSTer handles CD-based ROMs and images is fairly simple. There are some specifics that need to be described about how the MiSTer handles CDs.

## Will MiSTer ever support USB CD Drives?

The short answer is pretty much **no**. The long answer is that 1) there is too much hardware variation in CD drives and the drivers that go with them for it to be worth it 2) everything added to the Linux image and Main binary for the MiSTer have to be very carefully considered as the goal is to keep it lightweight and not bloated. CD Drive support is not a priority as properly dumped CD-ROM images are bit-perfect where it counts (excluding randomized subchannel data and garbage data fill-in, which don't usually matter for most platforms or software).

## Cue/Bin Folders

If you are using cue/bin files, then you need to place them in their own folder separate from the other cue/bin ROMs