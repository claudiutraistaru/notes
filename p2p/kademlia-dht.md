# Kademlia DHT

A DHT(Distributed hash table) is a simple concept. All values are hashed to certain digest and the digest is used as a key in the table. And keys are evently distributed as responsibility of each node. By looking up keys, values can be found.

DHT is vague. Kademlia is more concrete and pratical.

In Kademlia, routing table has _k_ buckets, where _k_ is the number of bits a node ID has(of course each network should have a fixed agreed-upon node ID size). The bucket index(0~_k_) represent the distance from the local host to the known nodes. Backtrack: the routing table is used to store known nodes for the local host. In another word, distance is the number of bits difference between two nodes. By definitation, the more different between two IDs, the further they are located.

The genius part of Kademlia is each bucket should have a fixed size. By nature, It's easier to fill out nodes with great distance than with short distance. So farther nodes matter less as they could be unstable and replacable. And nearby nodes are more stable and of course are of fewer number. More concisely, each node knows its neighbour better than other nodes know about them. So when you querying keys, each step will bring you closer!

Its implementation in [libp2p-go](https://github.com/libp2p/go-libp2p-kad-dht)

- Kad-dht depends on Host interface.
- BasicHost depends on Network interface. More precisely, Host interface wraps around Network.
- cpl(Common prefix length) is used to split a kbucket.