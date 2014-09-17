# node-wireless

A utility for handling interactions with wireless interfaces on \*nix distributions.

## Goals

This Node.js module will eventually provide all of the following features:

* Get a list of visible networks ✓
* Display info about connected network ✓
* Display different information about other networks, e.g. strength ✓
* Disconnect from network ✓
* Connect to open networks ✓
* Connect to secure networks, providing credentials or certificate
* Trigger an event when a new network appears ✓
* Trigger an event when a network changes ✓
* Trigger an event when a network disappears or lose connection ✓

Basically, this class should be able to do anything a user would be able to do using their OS's network configuration tools.

Currently there is a dependency on the tool `wpa_supplicant` being installed.
This module actually executes that utility many times to get results.
Eventually we'll move to a D-Bus based approach (#19) which will result in much quicker results and fewer dependencies.


## Installation

```bash
npm install wireless
```


## Current Status

Currently, enabling/disabling adapter works, finding new networks will trigger events,
able to read encryption method and other data, and disappearing networks trigger events,
able to enable and disable dhcp, able to connect to unsecure networks.

```
$ ./examples/scan-connect-disconnect.js wlan0
[PROGRESS] Enabling wireless card...
[PROGRESS] Wireless card enabled.
[PROGRESS] Starting wireless scan...
[PROGRESS] Wireless scanning has commenced.
[  APPEAR] Zen Buddhist Temple Public [00:27:22:14:DB:84] 64% -65 dBm NONE
[  APPEAR] ArborMesh-ch1 [0A:B3:85:5F:45:99] 62% -66 dBm NONE
[  APPEAR] AHOPS [00:23:A2:DE:4A:B0] 100% -14 dBm WPA&WPA2
[  APPEAR] ArborMesh [62:3D:28:71:4F:79] 100% -28 dBm NONE
[  APPEAR] dOpsInternal [00:0C:41:36:A3:F6] 100% -25 dBm WPA
[  APPEAR] Zen Buddhist Temple Public [F8:D1:11:47:EE:4A] 100% -17 dBm NONE
[  APPEAR] Zen Buddhist Temple Private [FA:D1:11:47:EE:4B] 100% -28 dBm WPA2
[  APPEAR] Zen Buddhist Temple Public [F8:D1:11:54:A9:DE] 100% -23 dBm NONE
[  APPEAR] Zen Buddhist Temple Private [FA:D1:11:54:A9:DF] 91% -46 dBm WPA2
[  APPEAR] ATT200 [CC:7D:37:81:0F:20] 68% -62 dBm WPA&WPA2
Yay, we connected! I will try to get an IP.
[    JOIN] Zen Buddhist Temple Public [00:27:22:14:DB:84] 
[    DHCP] Leased IP 10.88.0.58
Yay, I got an IP address (10.88.0.58)! I'm going to disconnect in 20 seconds.
[  LEVELS] Zen Buddhist Temple Public
[  LEVELS] ArborMesh-ch1
[  LEVELS] AHOPS
[  LEVELS] ArborMesh
[  LEVELS] dOpsInternal
[  LEVELS] Zen Buddhist Temple Public
[  LEVELS] Zen Buddhist Temple Private
[  LEVELS] Zen Buddhist Temple Public
[  LEVELS] ATT200
20 seconds are up! Attempting to turn off DHCP...
DHCP has been turned off. Leaving the network...
[   LEAVE] Left the network
[  LEVELS] Zen Buddhist Temple Public
[  LEVELS] ArborMesh-ch1
[  LEVELS] AHOPS
[  LEVELS] ArborMesh
[  LEVELS] dOpsInternal
[  LEVELS] Zen Buddhist Temple Public
[  LEVELS] Zen Buddhist Temple Public
[  APPEAR] Zen Buddhist Temple Private [02:27:22:14:DB:85] 100% -20 dBm WPA2
[  LEVELS] Zen Buddhist Temple Private
[  APPEAR] 2WIRE163 [00:1F:B3:6B:97:D9] 75% -57 dBm WEP
^C[PROGRESS] Gracefully shutting down from SIGINT (Ctrl+C)
[PROGRESS] Disabling Adapter...
[PROGRESS] Stopping Wireless App...
[PROGRESS] Exiting...
```


## Requirements

Needs `wpa_supplicant`, a wireless card which can see a list of available networks.


## Assumptions

* We assume that DHCP isn't enabled on the wireless device by default.
* I've only tried this on Arch  and Debian Linux.
* I've only tried this using a wireless card with the `RTL8187` and `rt2800usb` chipsets.


## License

Dual MIT/GPL
