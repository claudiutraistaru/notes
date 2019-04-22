# Docker

## Fundamentals

On Linux, Docker uses [cgroups](https://en.wikipedia.org/wiki/Cgroups), [kernel namespaces](https://en.wikipedia.org/wiki/Linux_namespaces) and others to allow independent containers to run within a single Linux instance, avoiding the overhead of starting and maintaining virtual machines.
On MacOS, the equivalent of Linux cgroups, kernel namespaces, etcs is Apple's [Hypervisor framework](https://developer.apple.com/documentation/hypervisor).

## Other contents

- [docker network](network.md)