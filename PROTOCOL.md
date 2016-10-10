# Protocol

This is the technical protocol definiton of Gnamma, if you're interested in a more general overview go to the [`README.md`](README.md) file. Everything in this document is under rapid development: here be dragons.

## Server

The server is responsible for hosting a Gnamma experience. The rules of what player's are allowed to do or see are governed by the server, these rules are defined in config or scripting files. The main role of the server is to provide a link between all of the connected clients, and ensure that the clients are all obeying the logic of the server (that is, the rules defined in the aforementioned config and scripting files).

## Asset Server

The asset server is responsible for serving up assets to clients. It operates in a similar manner to a HTTP server, except working on a lower level and not concerning itself with the specifics of the served files. One of its more complex roles is to ensure the quickest possible loading of the 3D assets needed to make up a VR experience. This is done by caching as much as possible, and transfering files from the closest possibly server to minimise wait times.

You can read more about the asset server in the [`ASSET_SERVER.md`](ASSET_SERVER.MD) file.

## Client

The client is used to connect to a server in order to play a Gnamma experience. The main role of the client is to render the environment which it receives from the server, and relay the different inputs of the player. Upon connection, the client retrieves a copy of the logic of the server, which is a set of rules detailing what **can** happen in a given experience. This logic is then simulated, to allow the environment to react in real time to the player. At an interval set by the server the client has its own simulation overridden by that of the server. This ensures that all of the clients connected to a server are having the same experience.

### Lifecycle

1. Initiation
  - Located host
2. Establish environment
  - Download rules and scripts
  - Share asset list
  - Assess what needs to be downloaded
  - Download new assets
  - Load old and newly downloaded assets
3. Open stream
  - Keep environment in sync with server
  - *Loop until exit requested*
4. Disconnect

## Specification

Welcome to the actual specification section of the protocol. Again, note that this document is **not** finished.

### Contents

1. [Ping](#ping)
2. [Pong](#pong)
3. [Connect Request](#connect-request)
4. [Connect Verdict](#connect-verdict)
5. [Environment Request](#environment-request)
6. [Environment Package](#environment-package)

### Ping

Ping is used for verifying that the connection between a client and a server is working as intended.

#### Payload

```json
{
    "command": "ping",
    "sent_at": 0
}
```

The server will respond with a [pong](#pong).

### Pong

Pong is the response issued by the server when sent a [ping](#ping). If the client receives a pong, then it can be assumed that the connection is working time. The round trip latency can be found be measuring the delta between the `receieved_at` and `sent_at` fields.

#### Payload

```json
{
    "command": "pong",
    "sent_at": 1,
    "received_at": 0
}
```

### Connect Request

Connect Request is used when the client wants to initiate a connection with a server.

#### Payload

```json
{
    "command": "connect_request",
    "sent_at": 0,
    "username": "paked"
}
```

The server will respond with a [connect verdict](#connect-verdict)

### Connect Verdict

Connect Verdict informs the client of whether or not they are allowed to proceed into the server.

#### Payload

```json
{
    "command": "connect_verdict",
    "sent_at": 1,
    "can_proceed": true,
    "message": "Congrats! You've joined the server."
}
```

### Environment Request

Environment Request is sent by the client when it wants a copy of the [Gnamma World File (GWF)](GWF.md).

#### Payload

```json
{
    "command": "environment_request",
    "sent_at": 0
}
```

#### Notes

In the future, the client should probably have some sort of communication where it shares what it already has cached. This way unnecessary downloads can be prevented.

The server will respond with an [Environment Package](#environment-package).

### Environment Package

Environment Package contains information about the world which the experience is providing. It provides the unique identifier for each asset which needs to be downloaded, so they can be retrieved from an asset server.

#### Payload

```json
{
    "command": "environment_package",
    "sent_at": 1,
    "asset_keys": {
        "world": "some_hex_value",
        "glass": "another_hex_value"
    },
    "main": "world"
}
```
