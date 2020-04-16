## Introduction

When people think of how computers communicate with eachother via the internet they will often
give an analogy of computers being like telephones and IP Addresses are the phone numbers.

However the reality is much more complicated than thats - as we will soon found out as we explain 
how networking currently works and how current peer-to-peer tecnologies create a connection 
between two computers.

### Basic Communication

At a low-level computers do indeed have a unique address which other computers on that same network
can use to communicate with them. It is in-fact a very primitave system than what you may be used to.

Inside every computer there is dedicated hardware built to handle networking; This could be a
ethernet card, a wireless chip or even both. Each piece of hardware is assigned a unique MAC address
at the time of manufacturingg.

When two computers are directly connected to each other they can communicate by simply using the MAC
address for the computer they which to speak to So if Computer A wants to speak to Computer B, 
assuing they are connected to each other by ethernet, then it will send the message to the MAC
address for Computer B's ethernet card.

### IP Addresses

As computer networks expanded there grew a need to allow computers from different networks to 
communicate with each other. MAC addresses were great for identifying unique devices but they 
had one major pitfall, routing. 

If one computer on one network wanted to communicate to another computer on an other network
then the MAC address system no-longer scaled. Because MAC addresses were effectivley randomly
generated then there was no way to figure out where in the network a computer was connected
or how to reach it.

So if Computer A was connected to Computer B and Computer B to Computer C - Computer A wouldn't
know how to speak to Computer C since it would be on a different network. MAC addresses don't
provide any information on how to reach that device so Computer B would have to forward it to
Computer C.

Which as the network gets more complicated and web-like this potentially would maen every computer
on every network would have to be forwaded this request until the computer with that MAC address
was found.

IP addresses solved this by assigning a logical number to the hardware of each computer - like a
telephone number it was possible to know if this number was for a computer on the same
network, another network or even publically accessible.

So if all of the computers on the local netweork are assigned an IP address between 192.168.0.1 and 
192.168.0.255 - Then if Computer A knows that Computer C has an IP address of 10.5.4.2 then
because it's not between those two number then it knows it's not on the same network.

With this system on each network there is a designated "gateway" to forward requests for computers
not on the same network. In this case Computer B would be assigned as the gateway and it would check
if the IP address for Computer C is on the local network. Each time it wasn't found then the request
would be forwarded to the next gateway until there are no more gateways to forward to.

### The Internet

When the internet came along there need to be a way to allow certain computers to be accesible for
all computers in the world. To achieve this a certain range of IP addresses were designated as being
"public". Tbese would be assigned to web servers which powered websites such as Google and connected
to a special global network.

When your computer connected to the internet it would sned requests via a computer with a public
IP address and connected to the same global network as the websites of the world. The website
would then send the data back to your computer via the same computer using it's public IP address.

### Routers and NATs

The explanation given so far is a slight over-simplification so far. To get a full-picture we
need to explain the router and NAT.

As the internwt grew popular it became important to not only improve security but also ensure the
limited pool of IP addresses didn't run out. This is where routers and NAT became useful.

Most computers are used by people who don't want other computers accessing their content and so
additional security was need to make sure you couldn't just send a request to someone's computer
by guessing thier IP address.

NAT solved this by preventing direct access to the computers on a network - when you connect your
devices to your router there are each assigned a private IP address which is only known to the
devices on that network.

When your computer made a request your router forwards it and makes it look like it came from it's
IP address, this is wat is known as NAT. The router will send it via a special destination or port
that the responnse to it's request can be sent to and it will know to send it to the original 
computer making the request.

By doing this your devices are secure as nobody can communicate to it directly and IP addresses can
be re-used across many of these private networks as private IP addresses would only ever be used for
local communication.

### Peer-to-Peer today

However this presented an issue - direct communication between a computer on one network and another
on another network became more difficult when both of those computers wern't configured to be public.

The first wave of solutions involved using a protocol to request your router allows requests from
a specific port get forwarded to your device. However this came with security risks as any
application could then reconfigure your network settings.

And so when WebRTC came along two more protocols STUN and TURN were created. There are in-fact
many ways NAT can be configured - STUN detects which specific configuration your router has.

If your router always uses the same port for your device then STUN will detect that and then
when another computer will use this port to speak to your device. However not all routers
are configured like this and not every user has the ability to re-configute their network.

In addition if two devices are on the same network but connected to a different gateway or
subnet then the STUN protcol doesn't always work.

In these situations mos services fallback to TURN - essentailly using a publically accesible servers
both computers connect to and then that server acts as a middle man passing the data between them.

Obviously this has it's downside in terms of cost for the company running the TURN server and
creates a security risk as all communication is now passing though one centeral cerver which
elimiates the decentralized benefits of peer-to-peer.

To solve this strategies were developed to workaround the security policies so that more connections
could be directly established via STUN. But they are just that a workaround.

With this in mind  - Project Layla was started to address these issues.