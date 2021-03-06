# libp2p notes & analysis

## libp2p-go default host construct

libp2p's main entry function `func New(ctx context.Context, opts ...Option) (host.Host, error)` is quite unique. Similarly, it uses a [Config struct](https://github.com/libp2p/go-libp2p/blob/9a5a43777294ea1f4337ae90604c26c2aad8765a/config/config.go#L44) to build the _Host_, just like most of services. Differently, libp2p use chain of callback functions called [_Option_](https://github.com/libp2p/go-libp2p/blob/9a5a43777294ea1f4337ae90604c26c2aad8765a/config/config.go#L226) to be _applied_ on an empty Config. In another word, user can't just provide a Config instance(the _New_ construct simply doesn't take Config). Instead, user need to provide a slice of _Option_ s that will be applied on to an initially empty Config during construction. I think the rationale behind it is that a framework like libp2p requires a lot of customization and flexibity and a simple Config instance just wouldn't do. Might as well just chain callbacks.

Diving in the [FallbackDefaults](https://github.com/libp2p/go-libp2p/blob/9a5a43777294ea1f4337ae90604c26c2aad8765a/defaults.go#L130), I easily found out default Options are mostly default implementations of the major components of libp2p. I found out the main defaults [here](https://github.com/libp2p/go-libp2p/blob/9a5a43777294ea1f4337ae90604c26c2aad8765a/defaults.go#L82): DefaultListenAddrs, DefaultTransports, DefaultMuxers, DefaultSecurity, RandomIdentity, DefaultPeerstore, DefaultEnableRelay.

In order to understand the default Host, I need to dive into those default Option callbacks above.

- __DefaultListenAddrs__
Basically appends the two default MultiAddrs: "/ip4/0.0.0.0/tcp/0" and "/ip6/::/tcp/0" to Config.ListenAddrs
- __DefaultTransports__
Appends two default Transport protocol _constructors_ to Config.Transports. They are [tcp](https://github.com/libp2p/go-tcp-transport) and [websocket](https://github.com/libp2p/go-ws-transport).
- __DefaultMuxers__
Appends two default Muxer _constructor_ to Config.Muxers. They are [/yamux/1.0.0](https://github.com/whyrusleeping/go-smux-yamux) and [/mplex/6.7.0](https://github.com/whyrusleeping/go-smux-multiplex).
- __DefaultSecurity__
Appends the default security constructor too Config.SecurityTransports. It is [libp2p-secio](https://github.com/libp2p/go-libp2p-secio)
- __RandomIdentity__
Uses [libp2p-crypto] to generate an RSA private key and set it as Config.PeerKey.
- __DefaultPeerstore__
Creates an instance of [peerstore](https://github.com/libp2p/go-libp2p-peerstore) and set it as Config.Peerstore. This really isn't much of decision as it's the only choice.
- __DefaultEnableRelay__
Enables relay by setting Config.RelayCustom = true, Config.Relay = true and Config.RelayOpts to []circuit.RelayOpt{}. This list of RelayOpt is empty in this default environment.

After all the elements are set in place for the instance of Config thru several Options, a new Node can be constructed.
At the end of `New(...)`, [func (cfg *Config) NewNode(ctx context.Context) (host.Host, error)](https://github.com/libp2p/go-libp2p/blob/9a5a43777294ea1f4337ae90604c26c2aad8765a/config/config.go#L76) was called and returned.
