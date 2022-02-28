There are multiple advanced networking features that the MiSTer can utilize. Here we will go over quite a few of them.

## CIFS Share Mounting
The MiSTer can mount a network share from another computer or server as if it were storage. There are two scripts that are used by the MiSTer for CIFS mounting and unmounting.

[cifs_mount.sh](https://raw.githubusercontent.com/MiSTer-devel/Scripts_MiSTer/master/cifs_mount.sh){target=_blank}

This script mounts the desired network share to the MiSTer in such a way that any identical folders from `/media/fat` will be put on a lower priority and you will see the ones from the network share in place of the ones on your MicroSD. See [Core Paths](../cores/paths.md) for more specific information as to how this hierarchy functions.

[cifs_umount.sh](https://raw.githubusercontent.com/MiSTer-devel/Scripts_MiSTer/master/cifs_umount.sh){target=_blank}

This script will unmount the network share when ran.

## RetroNAS
A project was launched that makes it easier to get a network attached storage (NAS) device up and running which was focused solely on retro gaming device compatibility. The MiSTer was one of their primary focuses and it works quite well. All you need is a Raspberry Pi4 and some kind of external hard drive storage device. Remember: NAS IS NOT BACKUP! You could lose data if you rely solely on a NAS for important data. They have a good [installation guide](https://github.com/danmons/retronas/wiki/Installing-RetroNAS){target=_blank} that is simple to follow and [MiSTer-specific instructions](https://github.com/danmons/retronas/wiki/MiSTer-FPGA){target=_blank} to help get you started. They also have video guides available on Youtube for [installation](https://www.youtube.com/watch?v=szA-MSabplc){target=_blank} and [MiSTer FPGA-specific configuration](https://www.youtube.com/watch?v=OrTctA-5kqk){target=_blank} if you prefer.
