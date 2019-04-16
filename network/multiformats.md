# Multiformats notes & analysis

First, [multiformats](https://multiformats.io/) is designed to make project/frameworks future proof. Because technologies change so quick nowadays. The technology we rely on today may not fit our need tomorrow. Or simply just for flexibility. To illustrate, here is an example:
    I'm designing an API which accepts and emits JSON data. With the history of XML pushed out of fashion by JSON, I need to prepare for the next data-serialization scheme. With multicodec, all my data will be prefixed with the type of scheme codec it's being used, in my case it would be JSON. So my handling of data is not JSON but multicodec, I accept multicodec data and from the prefix, I can easily find out it's JSON data and handle it accordingly. In the future, I might want to switch to protobuf, which is no problem because all I need to do is to add a handler for protobuf.

There are sub projects for different areas: multiaddr, multihash, multistream ...

libp2p is a sister project of multiformats. Today I'm going to focus on multistream with Go. Key points for myself:

- multistream connection pretty much models Go's net.Conn with ReadWriteCloser interface.
- the multistream muxer adds a layer of self-description of protocol being used in this stream. The muxer can match the corresponding handler for each incoming stream.
- [example](https://github.com/multiformats/go-multistream#example)
- [this _Negotiate_ function](https://github.com/multiformats/go-multistream/blob/master/multistream.go#L270) is the middle layer that handle the negotiation of which codec to use. Overall, `Handle(rwc)` accepts the connection and let `Negotiate(rwc...) ...` take the lead to find out their shared codec(like a handshake). And then `Negotiate` will return the corresponding handler function so that the rwc(Conn) can be passed onto.