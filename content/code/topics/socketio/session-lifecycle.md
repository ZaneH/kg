---
title: Socket.IO Session Lifecycle
tags: socketio, network
---

A full sample session can be found in the [[code/topics/socketio/sample-session|Socket.IO Sample Session]] page.

## Initial Connection

Clients can be connected to multiple namespaces in the same WebSocket connection.

```
CLIENT                                                      SERVER

  │  ───────────────────────────────────────────────────────►  │
  │             { type: CONNECT, namespace: "/" }              │
  │  ◄───────────────────────────────────────────────────────  │
  │   { type: CONNECT, namespace: "/", data: { sid: "..." } }  │
```

## Connecting to a namespace

- with the main namespace (named `"/"`)

```
Client > { type: CONNECT, namespace: "/" }
Server > { type: CONNECT, namespace: "/", data: { sid: "wZX3oN0bSVIhsaknAAAI" } }
```

- with a custom namespace

```
Client > { type: CONNECT, namespace: "/admin" }
Server > { type: CONNECT, namespace: "/admin", data: { sid: "oSO0OpakMV_3jnilAAAA" } }
```

- with an additional payload

```
Client > { type: CONNECT, namespace: "/admin", data: { "token": "123" } }
Server > { type: CONNECT, namespace: "/admin", data: { sid: "iLnRaVGHY4B75TeVAAAB" } }
```

- in case the connection is refused

```
Client > { type: CONNECT, namespace: "/" }
Server > { type: CONNECT_ERROR, namespace: "/", data: { message: "Not authorized" } }
```

## Sending and receiving data

Once the [connection to a namespace](https://socket.io/docs/v4/socket-io-protocol/#connection-to-a-namespace) is established, the client and the server can begin exchanging data:

```
CLIENT                                                      SERVER

  │  ───────────────────────────────────────────────────────►  │
  │        { type: EVENT, namespace: "/", data: ["foo"] }      │
  │                                                            │
  │  ◄───────────────────────────────────────────────────────  │
  │        { type: EVENT, namespace: "/", data: ["bar"] }      │
```

The payload is mandatory and MUST be a non-empty array. If that's not the case, then the receiver MUST close the connection.

Examples:

- with the main namespace

```
Client > { type: EVENT, namespace: "/", data: ["foo"] }
```

- with a custom namespace

```
Server > { type: EVENT, namespace: "/admin", data: ["bar"] }
```

- with binary data

```
Client > { type: BINARY_EVENT, namespace: "/", data: ["baz", <Buffer <01 02 03 04>> ] }
```

### Acknowledgement

The sender MAY include an event ID in order to request an acknowledgement from the receiver:

```
CLIENT                                                      SERVER

  │  ───────────────────────────────────────────────────────►  │
  │   { type: EVENT, namespace: "/", data: ["foo"], id: 12 }   │
  │  ◄───────────────────────────────────────────────────────  │
  │    { type: ACK, namespace: "/", data: ["bar"], id: 12 }    │
```

The receiver MUST respond with an `ACK` packet with the same event ID.

The payload is mandatory and MUST be an array (possibly empty).

Examples:

- with the main namespace

```
Client > { type: EVENT, namespace: "/", data: ["foo"], id: 12 }
Server > { type: ACK, namespace: "/", data: [], id: 12 }
```

- with a custom namespace

```
Server > { type: EVENT, namespace: "/admin", data: ["foo"], id: 13 }
Client > { type: ACK, namespace: "/admin", data: ["bar"], id: 13 }
```

- with binary data

```
Client > { type: BINARY_EVENT, namespace: "/", data: ["foo", <buffer <01 02 03 04> ], id: 14 }
Server > { type: ACK, namespace: "/", data: ["bar"], id: 14 }

or

Server > { type: EVENT, namespace: "/", data: ["foo" ], id: 15 }
Client > { type: BINARY_ACK, namespace: "/", data: ["bar", <buffer <01 02 03 04>], id: 15 }
```

## Disconnection from a namespace

At any time, one side can end the connection to a namespace by sending a `DISCONNECT` packet:

```
CLIENT                                                      SERVER

  │  ───────────────────────────────────────────────────────►  │
  │           { type: DISCONNECT, namespace: "/" }             │
```

No response is expected from the other side. The low-level connection MAY be kept alive if the client is connected to another namespace.