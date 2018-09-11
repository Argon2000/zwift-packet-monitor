# zwift-packet-monitor

This module monitors Zwift UDP traffic on port 3022 and TCP traffic on port 3023 (both contains protobuf payloads) and emits events for

- player state updates (incomingPlayerState and outgoingPlayerState)
- ride ons (incomingPlayerGaveRideOn)
- chat messages (incomingPlayerSentMessage)
- player entered world (incomingPlayerEnteredWorld)

## Install

### Prerequisites
On Windows this requires WinPcap, Win10PCap or Npcap. On other systems, libpcap should be installed.

### Installation

```
npm install zwift-packet-monitor
```

## Usage

```javascript
const ZwiftPacketMonitor = require('zwift-packet-monitor')

// interface is cap interface name (can be device name or IP address)
const monitor = new ZwiftPacketMonitor(interface)

monitor.on('outgoingPlayerState', (playerState, serverWorldTime) => {
  console.log(playerState)
})

monitor.on('incomingPlayerState', (playerState, serverWorldTime) => {
  console.log(playerState)
})

// The Zwift server sends states in batches. This event is emitted at the end of each incoming batch
monitor.on('endOfBatch', () => {
  console.log('end of batch')
})

monitor.start()
```


# Relevant links

Npcap https://nmap.org/npcap/
Win10Pcap http://www.win10pcap.org/
WinPcap https://www.winpcap.org/

