# Protocol

This is the technical protocol definiton of Gnamma, if you're interested in a more general overview go to the [`README.md`](README.md) file.

## Lifecycle

1. Initiation
  - Located host
2. Establish environment
  - Share asset list
  - Assess what needs to be downloaded
  - Download new assets
  - Load old and newly downloaded assets
3. Open stream
  - Keep environment in sync with server
  - *Loop until exit requested*
4. Disconnect
