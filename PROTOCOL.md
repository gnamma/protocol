# Protocol

This is the technical protocol definiton of Gnamma, if you're interested in a more general overview go to the [`README.md`](README.md) file. Everything in this document is under rapid development: here be dragons.

## Server

The server is responsible for hosting a Gnamma experience. The rules of what player's are allowed to do or see are governed by the server, these rules are defined in config or scripting files. The main role of the server is to provide a link between all of the connected clients, and ensure that the clients are all obeying the logic of the server (that is, the rules defined in the aforementioned config and scripting files).

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

Welcome to the actual specification section of the document. Again, note that this document is **not** finished.

### Contents

1. Ping
2. Connect

### Ping

Ping is used for testing a connection between a client and a server. The information shared in a ping should be enough to establish a basic idea about:

- What the server is
- Multiplayer ability
- Connection quality

#### Request

```json
{
    "command": "ping",
    "sent_at": 0
}
```

#### Response

```json
{
    "server": "127.0.0.1",
    "name": "Courtyard",
    "description": "A place to meet and hang out with new friends",
    "receieved_at": 0,
    "rules": {
        "pvp": true,
        "multiplayer": true,
    }
}
```

### Connect

Connect is used when the client wants to initiate a connection with a server. The server will respond with a unique ID, which should be used by the client to create the long-term connection with the client.


#### Request

```json
{
    "command": "connect"
}
```

#### Response

```json
{
    "status": "approved",
    "uid": "0xFAB233"
}
```
