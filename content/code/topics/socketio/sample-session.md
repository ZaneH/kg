---
title: Socket.IO Sample Session
tags: socketio, network
---

A further breakdown of the topics covered here can be found in the [[code/topics/socketio/session-lifecycle|Socket.IO Session Lifecycle]] and [[code/topics/socketio/packet-encoding|Socket.IO Packet Encoding]] pages.

## Sample session

Here is an example of what is sent over the wire when combining both the Engine.IO and the Socket.IO protocols.

- Request n°1 (open packet)

```
GET /socket.io/?EIO=4&transport=polling&t=N8hyd6w
< HTTP/1.1 200 OK
< Content-Type: text/plain; charset=UTF-8
0{"sid":"lv_VI97HAXpY6yYWAAAC","upgrades":["websocket"],"pingInterval":25000,"pingTimeout":5000,"maxPayload":1000000}
```

Details:

```
0           => Engine.IO "open" packet type
{"sid":...  => the Engine.IO handshake data
```

Note: the `t` query param is used to ensure that the request is not cached by the browser.

- Request n°2 (namespace connection request):

```
POST /socket.io/?EIO=4&transport=polling&t=N8hyd7H&sid=lv_VI97HAXpY6yYWAAAC
< HTTP/1.1 200 OK
< Content-Type: text/plain; charset=UTF-8
40
```

Details:

```
4           => Engine.IO "message" packet type
0           => Socket.IO "CONNECT" packet type
```

- Request n°3 (namespace connection approval)

```
GET /socket.io/?EIO=4&transport=polling&t=N8hyd7H&sid=lv_VI97HAXpY6yYWAAAC
< HTTP/1.1 200 OK
< Content-Type: text/plain; charset=UTF-8
40{"sid":"wZX3oN0bSVIhsaknAAAI"}
```

- Request n°4

`socket.emit('hey', 'Jude')` is executed on the server:

```
GET /socket.io/?EIO=4&transport=polling&t=N8hyd7H&sid=lv_VI97HAXpY6yYWAAAC
< HTTP/1.1 200 OK
< Content-Type: text/plain; charset=UTF-8
42["hey","Jude"]
```

Details:

```
4           => Engine.IO "message" packet type
2           => Socket.IO "EVENT" packet type
[...]       => content
```

- Request n°5 (message out)

`socket.emit('hello'); socket.emit('world');` is executed on the client:

```
POST /socket.io/?EIO=4&transport=polling&t=N8hzxke&sid=lv_VI97HAXpY6yYWAAAC
> Content-Type: text/plain; charset=UTF-8
42["hello"]\x1e42["world"]
< HTTP/1.1 200 OK
< Content-Type: text/plain; charset=UTF-8
ok
```

Details:

```
4           => Engine.IO "message" packet type
2           => Socket.IO "EVENT" packet type
["hello"]   => the 1st content
\x1e        => separator
4           => Engine.IO "message" packet type
2           => Socket.IO "EVENT" packet type
["world"]   => the 2nd content
```

- Request n°6 (WebSocket upgrade)

```
GET /socket.io/?EIO=4&transport=websocket&sid=lv_VI97HAXpY6yYWAAAC
< HTTP/1.1 101 Switching Protocols
```

WebSocket frames:

```
< 2probe                                        => Engine.IO probe request
> 3probe                                        => Engine.IO probe response
> 5                                             => Engine.IO "upgrade" packet type
> 42["hello"]
> 42["world"]
> 40/admin,                                     => request access to the admin namespace (Socket.IO "CONNECT" packet)
< 40/admin,{"sid":"-G5j-67EZFp-q59rADQM"}       => grant access to the admin namespace
> 42/admin,1["tellme"]                          => Socket.IO "EVENT" packet with acknowledgement
< 461-/admin,1[{"_placeholder":true,"num":0}]   => Socket.IO "BINARY_ACK" packet with a placeholder
< <binary>                                      => the binary attachment (sent in the following frame)
... after a while without message
> 2                                             => Engine.IO "ping" packet type
< 3                                             => Engine.IO "pong" packet type
> 1                                             => Engine.IO "close" packet type
```