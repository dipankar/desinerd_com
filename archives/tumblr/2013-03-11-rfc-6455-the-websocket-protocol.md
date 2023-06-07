---
layout: post
title: RFC 6455 - The WebSocket Protocol
date: '2013-03-11T17:24:42+05:30'
tags:
- bosh
- ietf
- rfc
- websockets
- xmpp
tumblr_url: http://www.desinerd.com/post/150535103518/rfc-6455-the-websocket-protocol
---

 The WebSocket Protocol enables two-way communication between a client
   running untrusted code in a controlled environment to a remote host
   that has opted-in to communications from that code.  The security
   model used for this is the origin-based security model commonly used
   by web browsers.  The protocol consists of an opening handshake
   followed by basic message framing, layered over TCP.  The goal of
   this technology is to provide a mechanism for browser-based
   applications that need two-way communication with servers that does
   not rely on opening multiple HTTP connections (e.g., using
   XMLHttpRequest or <iframe>s and long polling).
RFC 6455 - The WebSocket Protocol.
Very interesting RFC, say in comparison to BOSH. Should be a fun read for most engineers.
