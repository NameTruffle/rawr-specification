# Project Laya

Project Laya is a concept for a modern peer-to-peer protocol for designed to work under all network
conditions including traversing symetrical NATs and other unique conditions not currently handled
by STUN or TURN.

For this protocol we have the following five principles:

- It should be primarily based on outbound connections to simplify firewall configuration
- It shouldn't require punching holes or insecure protcols (like uPnP)
- It should be flexible to deploy on networks with gateways which do not support this protocol
- It should use existing elements of the network stack when possible for ease of implementation
- It should be able to fallback if it can't do a full traversal

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

However this presented an issue

# Roadmap

- Break this into seperate markdown files