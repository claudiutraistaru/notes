# Device File/Special File

Everything is a file in Unix.

## [char special file vs. block special file](https://unix.stackexchange.com/questions/60034/what-are-character-special-and-block-special-files-in-a-unix-system)

When data is read or written to a device file, the request is handled by the driver for that device. Each device file has an associated number which identifies the driver to use. What the device does with the data is its own business.

### Block device

It is more like regular file. Reads and writes need to specify location. It is seekable. Data from device can be cached in memory. And writes to device and be buffered.

### Char device

It behaves like pipe and serial port. Reads and writes are immediate actions.
