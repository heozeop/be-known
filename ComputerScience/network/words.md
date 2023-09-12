### throughput
- amount of data which were handled in unit of time.
- bps(bit per seconds)
- related [latency](#latency)

### latency
- amount of time to travel around to target.
- amount of time to take to resolve the request.
- related [through put](#throughput)

### Network Topology
- structure of network
- ex
    - star
    - mesh
    - bus
    - tree
    - ring

### Private Network
- computer network that uses a private address space of IP addresses.
- ref
    - [private network](https://en.wikipedia.org/wiki/Private_network)
    
### Carrier-grade NAT
- Type of network address translation([NAT](#NAT)) used by ISPs in IPv4 network
- connect private network with public network
- mitigate IPv4 exhaustion
- use IP block: 100.64.0.0/10 (netmask 255.192.0.0)
- ref
    - [carrier grade nat](https://en.wikipedia.org/wiki/Carrier-grade_NAT)

### NAT
- network address translation / or
- method of mapping an IP address space into another by modifying network address information in the IP header of packets while type are in transit across a traffic routing device.

- ref
    - [Network address translation](https://en.wikipedia.org/wiki/Network_address_translation)