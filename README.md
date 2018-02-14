# RAWR Specification
An alternative to STUN and TURN ICE protocols for Web RTC which works with traversing symmetrical NAT.

WebRTC is a real time communication protocol for establishing a direct connection between nodes on a network ("peers"),
In order to connect these peers it uses a signalling server to exchange details and ICE servers to establish each connection.

In most cases WebRTC can use a STUN server to retrieve the public IP address and port of each peer to establish a direct connection or connect them directly if they are on the same subnet.

However when it comes to Symetrical NAT it's a different story; In this situation the port for each peer changes on each connection and only accepts an inbound connection from a destination and port of the outbound connection it was created for. This forces WebRTC to use a TURN server inorder to relay the data through a 3rd party to each peer, since they cannot connect to each other directly.

In this specification I propose a new protocol RAWR (Router assisting with relaying), for this protocol there are three guiding principles:

- It should be based on outbound connections
- It shouldn't require punching holes or insecure protcols (like uPnP)
- It should be flexible to deploy on legacy routers
- It should be able to fallback if it can't do a full traversal

# Overview

As a TURN server is also a STUN server, a RAWR server is also a TURN server. So how does it work? Well the idea of this protocol is to utilize the existing network.

The server will be ran as part of the router's services or on a device for each subnet of the network.

A peer will provide a root a configuration for a RAWR services as part of their list of ICE servers. The address for the RAWR server in this list will be for the Root RAWR server to fallback on (similar to how DNS servers work).

Both peers contact this server after exchanging ICE candidates and provide it with their MAC address.
The RAWR server then exchanges the MAC address between each peer.

Symetrical NAT traversal can now begin.

Each peer will have a RAWR gateway configured, this will be the server they should use for their subnet. Usually this is the router but this could be a server on the network the router is connected to for routers which don't support RAWR yet.

If the MAC address is already on the local network then they will connect to each otherwise they will use the gateway.

They will connect to this gateway and pass the MAC address they are trying to reach plus some details about the WebRTC session, if the mac address exists on that subnet then the router will establish a direct connection to it using the same rules as symetrical NAT.

If again the MAC address doesn't exist, it in turn will use it's own gateway to pass on the request (similar to how standard routing works.

Eventually if we reach a RAWR server without a gateway (this could be because its the last one in that subnet for example it's one ran by an ISP) then it will fallback onto the Root RAWR server specified by the peers.

If a RAWR server gets a request from a peer or another RAWR request which is for the same WebRTC session then it will act as a relay. Meaning whenever possible the closest RAWR server will try to become the relay to prevent long latency attrbiuted
to long round trips. (The Root RAWR server by default will only ever do this)

# Advantages

Each RAWR request is etablished by pairing up two outbound connections that want to talk to each other via their MAC address, therfore there is no outbound connection resulting in no need for hole punching.

Each node can configure a custom gateway meaning even networks with routers that don't support this yet can install a
server somewhere in the network to act as a hop. As more servers get added to more subnets the connections will get more
efficient as the RAWR server can figure out what is the optimal amount of hops.

And like DNS it supports a fallback to a specified Root server by the peers, so if you are on a network that doesn't yet
have it on every subnet or at all then we fallback to the old TURN based functionality.
