# SwiftNIO IRC

![Swift5](https://img.shields.io/badge/swift-5-blue.svg)
![iOS](https://img.shields.io/badge/os-iOS-green.svg?style=flat)
![macOS](https://img.shields.io/badge/os-macOS-green.svg?style=flat)
![tuxOS](https://img.shields.io/badge/os-tuxOS-green.svg?style=flat)
<a href="https://travis-ci.org/SwiftNIOExtras/swift-nio-irc"><img src="https://travis-ci.org/SwiftNIOExtras/swift-nio-irc.svg?branch=master" /></a>

SwiftNIO-IRC is a Internet Relay Chat 
[protocol implementation](Sources/NIOIRC) for
[SwiftNIO](https://github.com/apple/swift-nio).

This module contains just the protocol implementation. We also
provide:
- [swift-nio-irc-client](https://github.com/Under-the-Bed-Software/swift-nio-irc-client) - a simple IRC client lib
- [BrickBot](https://github.com/Under-the-Bed-Software/BrickBot)
    - A (basic) bot
  
To get started with this, pull 
[swift-nio-irc-server](https://github.com/NozeIO/swift-nio-irc-server) -
a module to rule them all and in the darkness bind them.

NIOIRC is a SwiftNIO port of the
[Noze.io miniirc](https://github.com/NozeIO/Noze.io/tree/master/Samples/miniirc)
example from 2016.


## Importing the module using Swift Package Manager

An example `Package.swift `importing the necessary modules:

```swift
// swift-tools-version:5.0

import PackageDescription

let package = Package(
    name: "IRCTests",
    dependencies: [
        .package(url: "https://github.com/SwiftNIOExtras/swift-nio-irc.git",
                 from: "0.6.0")
    ],
    targets: [
        .target(name: "MyProtocolTool",
                dependencies: [ "NIOIRC" ])
    ]
)
```


## Using the SwiftNIO IRC protocol handler

The IRC protocol is implemented as a regular
`ChannelHandler`, similar to `NIOHTTP1`.
It takes incoming `ByteBuffer` data, parses that, and emits `IRCMessage`
items.
Same the other way around, the user writes `IRCReply`
objects, and the handler renders such into `ByteBuffer`s.

To add the IRC handler to a NIO Channel pipeline:

```swift
import NIOIRC

bootstrap.channelInitializer { channel in
    channel.pipeline
        .add(handler: IRCChannelHandler())
        .then { ... }
}
```


### Who

This software is a fork of [swift-nio-irc](https://github.com/SwiftNIOExtras/swift-nio-irc). Please send all love to [ZeeZide](http://zeezide.de/) as this was their idea and I'm just hoping to continue working on it. 


