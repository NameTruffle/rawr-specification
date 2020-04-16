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

# Documentation

- [Background](docs/background.md) - A background on why Project Laya was developed and the state of peer-to-peer communication today
- [Design](docs/design.md) - The design and overview of how Project Laya works
- Specification - TBC

# Roadmap

- Break this into seperate markdown files