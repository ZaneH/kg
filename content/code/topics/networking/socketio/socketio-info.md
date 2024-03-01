---
title: Socket.IO
tags: networking, socketio
---

Socket.IO is a layer on top of the WebSocket protocol that makes it easy to send and receive messages between a client and a server. It has a few extra features that make it ideal for real-time communication. Examples of these features include:

- Automatic reconnection
- Multiplexing
- Binary support
- Acknowledgements
- Broadcasts

The [Engine.IO](https://socket.io/docs/v4/engine-io-protocol/) library is also worth looking at. It is the underlying library that Socket.IO uses to handle the WebSocket protocol. It is a standalone library that can be used without Socket.IO.

## Socket.IO Breakdown

The entire Socket.IO protocol is documented in the [Socket.IO Protocol](https://socket.io/docs/v4/socket-io-protocol) page.

1. [[code/topics/networking/socketio/socketio-packet|Socket.IO Packet]]
2. [[code/topics/networking/socketio/packet-encoding|Packet Encoding]]
3. [[code/topics/networking/socketio/session-lifecycle|Session Lifecycle]]
4. [[code/topics/networking/socketio/sample-session|Sample Session]]
