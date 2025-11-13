
2025-11-12 21:59

Tags: #Network #Backend

# What is HTTP

hyper text transfer protocol is a protocol used over TCP/IP in internets on layer 7 of the OSI model.

the main feature of HTTP is being **stateless**. it means you don't need to constantly save states of users and everything is contained inside the packet.


## HTTP 1.0

in this earlier version of HTTP everything needed to have its own TCP connection. for example if your website contained multiple html and css files each of them needs a separate TCP connection for themselves. this increased the overhead a lot and was inefficent.

## HTTP 1.1

this version introduced persistent connections. so now you don't need a TCP connection for each static file. you open one single tcp connection and it do all your transfers and will be closed after being explicitly closed or its time to lived gets finished.

also there can only be 6 TCP connections at most.

- **Advantage:** This feature reduces latency and improves performance by minimizing the number of connections that need to be opened and closed.
- **Drawback:** The server needs to maintain the TCP connection until it is explicitly closed or until its Time to Live (TTL) expires, which consumes memory.

### Pipelining
Pipelining allows the client to send multiple http requests without waiting for response. but responses must come back in the same order.
so its still sequential but without waiting.


## HTTP 2.0

this version introduced significant improvements on performance and efficiency.

### Binary Protocol
this version use Binary format for sending data instead of the normal text format. this makes the protocol faster and less error prune since binary data is easier and faster for computers to process.

### Multiplexing 
Multiplexing allows multiple requests and responses to be sent simultaneously over a single TCP connection. This eliminates the Head of Line Blocking problem present in НТТP/1.x, where requests had to be processed sequentially.
so now requests and can be send in any order and we can get their responses in any order as well.

### Header Compression
HTTP/2 uses HPACK compression to reduce the size of headers, which can be quite large.
Unlike HTTP/1.x, where headers are sent as plain text for each request, HTTP/2 compresses them, reducing overhead and speeding up communication.

### Server push
Server push allows the server to send statics to client before the client has requested for them. this can significantly improve page load times by preemptively sending resources the client will need.


