# Computer Network In General

## Background

(A few weeks ago(as of 2019 March 23rd), I got interested in p2p. So I attempted to build a p2p bootstrap POC with Rust. Because I always believe that's the best way to expose what I am lacking in understanding p2p as a whole.

The POC works well at the beginning. I created a basic protocol over UDP to bootstrap a p2p network. The first thing I learned is no matter how decentralized the network is, the bootstrap process will require a centralized server of some sort. unless it's a private network where broadcasting message is possible. I let the central server send the address of last 10 nodes that signaled it's start to a requesting node as seeds to find its peers.

Then I stuck on how peer can communicate with each other. TCP seems a overkill to pass little information but UDP would be too difficult implement.

I quit implementing this POC and started to look over popular p2p implementation on Github. _Libp2p_ is my natural choice.

There are tons of things I have learned about _libp2p_ this week. This frame work is very popular. Especially its Go, Rust, JS implementations. Go implementation is obviously the best one and the easiest for me to read. My goal is to evetually read its implementation in Rust.

Just some entries to keep track of what I learned and they can be expanded later.

1. [zeroconf](https://en.wikipedia.org/wiki/Zero-configuration_networking). Best examples: DHCP and DNS
2. [DHCP discovery](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol#DHCP_discovery) is very interesting as it relies on broadcasting across network.
3. [mDNS](https://en.wikipedia.org/wiki/Multicast_DNS)
4. [UPNP](https://en.wikipedia.org/wiki/Universal_Plug_and_Play) and especailly its NAT travesal protocol: [IGDP](https://en.wikipedia.org/wiki/Internet_Gateway_Device_Protocol)
5. Go NAT port mapping library: [go-nat](https://github.com/fd/go-nat). Very interesting.

```go
package main

import (
    "context"
    "log"

    nat "github.com/libp2p/go-libp2p-nat"
)

func main() {
    ctx := context.Background()
    n, err := nat.DiscoverNAT(ctx)
    if err != nil {
        log.Fatalln(err)
    }
    defer n.Close()

    m, err := n.NewMapping("tcp", 54321)
    if err != nil {
        log.Fatalln(err)
    }
    defer m.Close()

    maps := n.Mappings()
    for _, m := range maps {
        extAddr, err := m.ExternalAddr()
        if err != nil {
            log.Println("failed to get external address")
        }
        log.Printf("External: %s, Internal port: %d, Protocol: %s\n", extAddr, m.InternalPort(), m.Protocol())
    }
}
```

The above snippet is using the libp2p wrapper of go-nat.
Fun to play with. But this wrapper hides the type of NAT being used. Definitely need to try the actually _go-nat_ library.

Besides above, I have learned so much from libp2p-go. The structure of the entire framework, the configuration pattern, the idea of multi-formats, the design of the specification, the documentation style and so much more. I'll go into detail in future TILs.
