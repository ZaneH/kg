---
title: Socket.IO Packet
tags: socketio, network, packet
---

# Socket.IO Packet

Packets are [[code/topics/socketio/packet-encoding|encoded]] in the Socket.IO protocol. Read a breakdown of the [[code/topics/socketio/sample-session|sample session]] or read more about the [[code/topics/socketio/session-lifecycle|session lifecycle]].

## Packet Contents

| Description | Data type        | Optional |
| -------------- | ------------ | ------------- |
| A packet type | integer | |
| A namespace | string | |
| A payload | Object or Array | x |
| An acknowledgement ID | integer | x |

### Packet Types

| Type | ID | Usage |
|---|---|---|
|CONNECT|0|Used during the [connection to a namespace](https://socket.io/docs/v4/socket-io-protocol/#connection-to-a-namespace).|
|DISCONNECT|1|Used when [disconnecting from a namespace](https://socket.io/docs/v4/socket-io-protocol/#disconnection-from-a-namespace).|
|EVENT|2|Used to [send data](https://socket.io/docs/v4/socket-io-protocol/#sending-and-receiving-data) to the other side.|
|ACK|3|Used to [acknowledge](https://socket.io/docs/v4/socket-io-protocol/#acknowledgement) an event.|
|CONNECT_ERROR|4|Used during the [connection to a namespace](https://socket.io/docs/v4/socket-io-protocol/#connection-to-a-namespace).|
|BINARY_EVENT|5|Used to [send binary data](https://socket.io/docs/v4/socket-io-protocol/#sending-and-receiving-data) to the other side.|
|BINARY_ACK|6|Used to [acknowledge](https://socket.io/docs/v4/socket-io-protocol/#acknowledgement) an event (the response includes binary data).|
