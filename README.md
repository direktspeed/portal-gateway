# portal-gateway Multi Point Architecture Lib written in JavaScript
A Portal lib for multible Gateways that can Translate between Multiple Protocols used by webtorrent, couchbase-node-gateway, couchbase-fs a multi Protocol Translation Layers

# Features
Supports the following High and Low Level Protocols including the TLS(succesor of SSL) Secure Counter Parts
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

