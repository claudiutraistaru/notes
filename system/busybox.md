# Busybox

## mount

To understand `mount`, I did some research. It is part of [Busybox](https://busybox.net/), the swiss army knife of embedded linux. This single piece of software contains all the basic GNU software. Since everything is in the same code base, it's size is tiny. `mount` is one of them along with `mountpoint`. You can mount onto a file system with a mount point. So with `mountpoint [dirname]` you can find out if a directory is a mountpoint inside alpine. Real convenient.
The usage about these commands can be found [here](https://busybox.net/downloads/BusyBox.html).
