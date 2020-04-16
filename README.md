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

However the reality is much more complicated as we will explain how the internet currently works
and how current peer-to-peer tecnologies create a connection between two computers.

### Basic