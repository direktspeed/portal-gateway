# portal-gateway Multi Point Architecture Lib written in JavaScript
A Portal lib for multible Gateways that can Translate between Multiple Protocols used by webtorrent, couchbase-node-gateway, couchbase-fs a multi Protocol Translation Layers


https://www.w3.org/TR/webrtc/#call-flow-browser-to-browser
  
A Public IP Address is an IP address that is globally unique across the Internet. Only one device may be in possession of a public IP address.

A Private IP Address is an IP address that is not globally unique and may exist simultaneously on many different devices. A private IP address is never directly connected to the Internet. Devices that possesses a private IP address will be in their own unique IP space (e.g. different companies or domains, networks). 

Network Address Translation (NAT) gives private IP addresses access to the Internet. NAT allows a single devices, such as a router, to act as an agent between the Internet (populated with public IP addresses) and a private network (populated with private IP addresses). A NAT device can use a single public IP address to represent many private IP addresses.

A Symmetric NAT not only translates the IP address from private to public (and vice versa), it also translates ports. There are various rules as to how that translation and mapping occurs, but it’s safe to say that with symmetric NAT, you should never expect that the IP address/port of the source is what the destination will see.


## ICE Interactive Connectivity Establishment

It’s ICE’s job to find the best path to connect peers. It may be able to do that with a direct connection between the clients, but it also works for clients where a direct connection is not possible (i.e. behind NATs).

In the case of asymmetric NAT, ICE will use a STUN (Session Traversal Utilities for NAT) server. A STUN server allows clients to discover their public IP address and the type of NAT they are behind. This information is used to establish the connection. The STUN protocol is defined in RFC 3489.

In most cases, a STUN server is only used during the connection setup and once that session has been established, media will flow directly between clients.

If a STUN server cannot establish the connection, ICE can turn to TURN (pardon the pun). Traversal Using Relay NAT (TURN) is an extension to STUN that allows media traversal over a NAT that does not do the “consistent hole punch” required by STUN traffic. TURN servers are often used in the case of a symmetric NAT.

Unlike STUN, a TURN server remains in the media path after the connection has been established. That is why the term “relay” is used to define TURN. A TURN server literally relays the media between the peers.


# Features
Supports the following High and Low Level Protocols including the TLS(succesor of SSL) Secure Counter Parts

- rawRTC
- WebRTC [W3C WebRTC API][w3c-webrtc] and [[draft-ietf-rtcweb-jsep-24]][jsep]
- Session Description Protocol (SDP) [[RFC_4566]][sdp] and [[draft-ietf-rtcweb-sdp-04]][webrtc-sdp]
- [Object] RealTime Communication ([O]RTC), [w3c-ortc]
- Interactive Connectivity Establishment (ICE) [[draft-ietf-ice-rfc-5245bis-08]][ice]
  - Trickle ICE [[draft-ietf-ice-trickle-07]][trickle-ice]
- STUN [[RFC 5389]][stun]
  - DTLS over UDP [[RFC 7350]][stun-turn-dtls]
- TURN [[RFC 5766]][turn]
- IP Address Handling [[draft-ietf-rtcweb-ip-handling-03]][ip-handling]
- DNS-based STUN/TURN server discovery
- Data Channel
  - DCEP [[draft-ietf-rtcweb-data-protocol-09]][dcep]
  - SCTP-based [[draft-ietf-rtcweb-data-channel-13]][sctp-dc]
  - WebSockets
- Session Border Controller (SBC).
  - Security
  - NAT traversal
  - Interoperability
  - Policy enforcement  
- WebTorrent (WebRTC)
- WS(S) WebSockets (TCP)
- Torrent (TCP)
- UDP
- TCP
- HTTP(S)
- MQTT
- DNS(S)

It enables Multi Protocol Routing for distributed Applications. The Most amazing feature of couchbase-fs Called Torrent Stream Transport is enabled via this. It Allows File Downloads as distributed torrent even via direct links.

## Example usage
All examples assume that the client is connected to a portal-gateway enabled Server
- Webtorrent Client in Browser to Download Torrents that are only seeded via TCP at present.
- A UDP or TCP Client can get MQTT protocol Messages
- a HTTP client can get WebSocket Messages via HTTP Server sent Events.
- a HTTP client with WebRTC support can download Direct Links while seeding them as torrent.
- a Torrent client can Download HTTP Links

## Main Usage is to allow Distributed transfer of binary Data over many channels.

## MCU stands for Multipoint Conferencing Unit.
An MCU offers the ability to connect multiple participants in a single voice or video or any other binary(UP/DOWNLOAD) session.

MCUs generally implement the mixing architecture and are expensive due to their need for a lot of processing power per session.
with Portal Gateway you can implament multi client Multipoint connections via all 3 Types Mixing, Mesh, Routing.


#### Mixing
Mixing is an architecture for multipoint where every participant sends its media to a central server and receives the single media stream from that server that mixes all (or some) of the streams it receives.

The mixing server is called MCU.
Advantages of mixing architecture

    Requires little effort from the client to support this, as for the client this is a regular P2P session

Disadvantages of mixing architecture

    The most expensive of the options, since the MCU needs to decode, layout and re-encode the media it receives for all participants

Other multipoint architectures are mesh and routing.

#### Mesh
Mesh is an architecture for multipoint where every participant sends and receives its media to all other participants.

A mesh is a very common technique that is used in WebRTC to build multipoint conferences. It can usually scale to 4-6 participants for video sessions at most.
Advantages of mesh architecture

    Simple to implement in WebRTC
    Requires very little backend infrastructure, keeping the resulting service cheap to operate

Disadvantages of mesh architecture

    Can’t scale to a large number of participants
    Requires a lot of uplink bandwidth from the participants

#### Routing
Routing is an architecture for multipoint where every participant sends its media to a central server and receives the streams from all participants via that central server.

The routing mechanism enables the WebRTC clients to reduce the load necessary from them on the uplink by having a server “spread” their media to all other participants.

The routing mechanism also reduces the load from the server by not requiring it to decode, layout and re-encode the media sent to all the participants.

At times, routing will use Simulcast to provide the most suitable resolution and bitrate to each participant.

This makes the cost of a routing architecture feasible for many use cases.
Advantages of routing architecture

    Requires asymetric bandwidth (more downlink than uplink) from the participants, making it very suitable for ADSL
    Scales to 10 and more participants with ease for many use cases and screen layouts

Disadvantages of routing architecture

    Requires backend routing server, though less expensive than a mixing solution
    Can be tricky to implement
   
   
# Infrastructure
- https://github.com/rawrtc/rawrtc
-


[sdp]: https://tools.ietf.org/html/rfc4566
[ice]: https://tools.ietf.org/html/draft-ietf-ice-rfc5245bis-08
[trickle-ice]: https://tools.ietf.org/html/draft-ietf-ice-trickle-07
[stun]: https://tools.ietf.org/html/rfc5389
[turn]: https://tools.ietf.org/html/rfc5766
[stun-turn-dtls]: https://tools.ietf.org/html/rfc7350
[dcep]: https://tools.ietf.org/html/draft-ietf-rtcweb-data-protocol-09
[sctp-dc]: https://tools.ietf.org/html/draft-ietf-rtcweb-data-channel-13
[jsep]: https://tools.ietf.org/html/draft-ietf-rtcweb-jsep-19
[w3c-webrtc]: https://www.w3.org/TR/webrtc/
[w3c-ortc]: http://draft.ortc.org
[webrtc-sdp]: https://tools.ietf.org/html/draft-ietf-rtcweb-sdp-04
[ip-handling]: https://tools.ietf.org/html/draft-ietf-rtcweb-ip-handling-03
