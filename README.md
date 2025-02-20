P2P Connect via UDP Hole Punching

UDP Hole Punching Overview

UDP hole punching is a technique used to establish direct peer-to-peer (P2P) connections between devices behind NAT (Network Address Translation). This method allows peers to communicate without requiring a direct public IP address.

Server Usage

Signaling: broker.emqx.io:1883

STUN Server: stun.l.google.com:19302

Workflow Description

Signaling via MQTT: Peers use MQTT as a signaling mechanism to exchange connection details.

Retrieving Public IP via STUN:

Each peer queries a STUN server to determine its public IP address and port.

The router temporarily keeps the public port open for a short duration after this request, allowing inbound packets from the same external endpoint.

Creating a UDP Socket:

Each peer initializes a UDP socket on a local port of its choice.

Publishing Candidate Information:

Peers connect to the MQTT broker and publish their connection details (IP, port) to a designated topic.

Gathering Candidates:

Each peer receives the connection details of the other peer.

The connection establishment process depends on the network configuration:

Case 1: Both peers are behind the same NAT and on the same machine.

Case 2: Both peers are behind the same NAT but on different machines within the local network.

Case 3: Peers are behind different NATs, requiring each peer to map its local port to the public port obtained from the STUN server.

UDP Hole Punching:

Once the peers exchange connection details and receive commands, they initiate communication through the mapped ports.

The hole punching process establishes a direct UDP connection between the peers.

How to Run

To run the implementation, simply execute:

make

References

Check the source code for detailed implementation steps.