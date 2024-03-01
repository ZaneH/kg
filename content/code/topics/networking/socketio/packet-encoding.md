---
title: Socket.IO Packet Encoding
tags: socketio, networking, packet, encoding
---

## Format
```
<packet type>[<# of binary attachments>-][<namespace>,][<acknowledgment id>][JSON-stringified payload without binary]

+ binary attachments extracted
```

Note: the namespace is only included if it is different from the main namespace (/)

## Examples

### Connection to a namespace

- with the main namespace

*Packet*

```
{ type: CONNECT, namespace: "/" }
```

*Encoded*

```
0
```

- with a custom namespace

*Packet*

```
{ type: CONNECT, namespace: "/admin", data: { sid: "oSO0OpakMV_3jnilAAAA" } }
```

*Encoded*

```
0/admin,{"sid":"oSO0OpakMV_3jnilAAAA"}
```

- in case the connection is refused

*Packet*

```
{ type: CONNECT_ERROR, namespace: "/", data: { message: "Not authorized" } }
```

*Encoded*

```
4{"message":"Not authorized"}
```

### Sending and receiving data

- with the main namespace

*Packet*

```
{ type: EVENT, namespace: "/", data: ["foo"] }
```

*Encoded*

```
2["foo"]
```

- with a custom namespace

*Packet*

```
{ type: EVENT, namespace: "/admin", data: ["bar"] }
```

*Encoded*

```
2/admin,["bar"]
```

- with binary data

*Packet*

```
{ type: BINARY_EVENT, namespace: "/", data: ["baz", <Buffer <01 02 03 04>> ] }
```


*Encoded*

```
51-["baz",{"_placeholder":true,"num":0}]

+ <Buffer <01 02 03 04>>
```

- with multiple attachments

*Packet*

```
{ type: BINARY_EVENT, namespace: "/admin", data: ["baz", <Buffer <01 02>>, <Buffer <03 04>> ] }
```

*Encoded*

```
52-/admin,["baz",{"_placeholder":true,"num":0},{"_placeholder":true,"num":1}]

+ <Buffer <01 02>>
+ <Buffer <03 04>>
```

Please remember that each Socket.IO packet is wrapped in a Engine.IO message packet, so they will be prefixed by the character "4" when sent over the wire.

Example:

```
{ type: EVENT, namespace: "/", data: ["foo"] } will be sent as 42["foo"]
```

### Acknowledgement

- with the main namespace

*Packet*

```
{ type: EVENT, namespace: "/", data: ["foo"], id: 12 }
```

*Encoded*

```
212["foo"]
```

- with a custom namespace

*Packet*

```
{ type: ACK, namespace: "/admin", data: ["bar"], id: 13 }
```

*Encoded*

```
3/admin,13["bar"]`
```

- with binary data

*Packet*

```
{ type: BINARY_ACK, namespace: "/", data: ["bar", <Buffer <01 02 03 04>>], id: 15 }
```

*Encoded*

```
61-15["bar",{"_placeholder":true,"num":0}]

+ <Buffer <01 02 03 04>>
```

### Disconnection from a namespace

- with the main namespace

*Packet*

```
{ type: DISCONNECT, namespace: "/" }
```

*Encoded*

```
1
```

- with a custom namespace

```
{ type: DISCONNECT, namespace: "/admin" }
```

*Encoded*

```
1/admin,
```