# Protocol

This is the technical protocol definiton of Gnamma, if you're interested in a more general overview go to the [`README.md`](README.md) file.

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
