# Supernode Approach

There are two types of participants in the XU network.

- "Supernodes" that maintain orderbooks, and may or may not trade themselves.
- "Nodes" that make and take orders using a supernode as an intermediary.

## Supernodes

Supernodes must burn a certain amount of XUC via an ethereum smart contract to "register" themselves as supernodes and committing their public key (and possibly IP address and/or supported chains) to the blockchain. This registration is independently verifiable by every other XU participant and can be an anti-spam/anti-DOS measure. Supernodes that misbehave or are otherwise unreliable can be banned or ignored. A dishonest supernode attempting to DOS or sybil attack the XU network must continue burning funds registering new public keys. This is also a use case for the XUC token.

Supernodes listen for incoming peers and payment channels. By default they establish XUC payment channels with incoming nodes. They can set and advertise their own fee rates - in XUC - for accepting orders into their orderbook as well as for sharing their orderbook. These fees can be very tiny and charged very granularly by taking advantage of the nature of payment channels. For example, it may cost a fraction of a penny worth of XUC to place an order or to get the current orderbook for a particular trading pair. Supernodes looking to build liquidity may offer near zero fees for placing orders. This again is a use case for XUC. Supernodes profit by collecting these fees, and also by collecting in the traded currencies when they act as a hop in the lightning payment swap. Supernodes wouldn't necessarily need to be involved in the payment swap itself, for example it would be possible for two nodes to have payment channels directly with each other and merely use the supernode for arranging orders.

Supernodes are expected to have near 100% uptime, support for all popular chains, and the resources to support low latency and robust orderbooks. Other nodes should be able to ping supernodes and get basic information like currencies supported and fee rates.

Although supernodes carry some privileges, there would be low barrier to entry in becoming a supernode which helps the network remain decentralized in nature. It also allows for competition - supernodes that are expensive or unreliable can be ignored and replaced by supernodes offering more attractive orderbook sservices.

XU could itself bootstrap the network by operating a supernode. Other early candidates for running supernodes may be relatively larger exchanges.

## Nodes

Regular nodes act like "leaves" in the XU network topography. Anyone can run a node and likely candidates are smaller exchanges or individual users. Nodes do not need to maintain internal orderbooks, they do not need to be constantly online, and they only need to run blockchain nodes for the currencies they themselves are interested in trading.

Regular nodes can "register" their public key with one or more supernodes. Registering enables them to place and query for orders with that particular supernode. The supernode will specify a one-time fee for registration - this too is an anti-spam and anti-DOS measure. Misbehaving nodes can be banned by supernodes, and must reregister and repay every time after being banned if they want to continue their attack.

Nodes can discover supernodes via the Ethereum blockchain and validate that they are properly registered. Nodes can keep internal blacklists of misbehaving or unreliable supernodes. As described above, nodes pay fees to a supernode when they want to place or query orders.

## Advantages

This approach treats each supernode as a meta-exchange (or perhaps "super exchange" is a better term). Internally, they are the source of truth and can independently handle adding, matching, and removing orders from their books. For this service they get paid XUC. Currency swaps still happen trustlessly and near-instantaneously. 
