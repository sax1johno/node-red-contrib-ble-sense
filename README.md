# node-red-contrib-ble-sense
Node-RED central module for Bluetooth Low Energy (BLE) devices. Speficially designed for environmental sensing peripherals such as Arduino Nano 33 BLE Sense.

Example Arduino code is provided in the following path `examples/bleSense/bleSense.ino`.

# Installation

```
npm install node-red-contrib-ble-sense
```

# Prerequisite

Requires [@abandonware/noble: 1.9.2-14.](https://www.npmjs.com/package/@abandonware/noble)

# Quick Start

The package contains two nodes: BLE Scanner, BLE Connect.

**BLE Scanner** node allows you to scan BLE devices. A message with **start** as a topic starts scanning. The node can output the following:
- Whole peripheral as an object.
- The MAC address of the peripheral.
- The advertisement data as a buffer array.

Hence **BLE Scanner** node can be used as an observer. This node also allows you to configure and search for a specific peripheral via given name.
To stop scanning a message with **stop** topic should be given.

**BLE Connect** node provides direct connection to the peripheral. This node must not be used alone. The scanning should be in progress to establish a connection.
It takes JSON Object as an input. The service and characteristics UUIDs should be provided. If not, it will try to subscribe all advertised characteristics.

The example input is shown below: 
```
{
    "services": [
        "181a"
    ],
    "characteristics": [
        "2a6e",
        "2a6f",
        "2a6d"
    ]
}
```

More details are provided in Node-RED node information panel.

# Examples

An example flow that provides subscription to the all characteristics is given below.

<img src="images/exampleFlow2.png"></img>

# License

Licensed under the MIT [License](LICENSE).

# Cite

Please cite the following work if you are making use of this package academically.

@article{KAYAN2021100437,
title = {AnoML-IoT: An end to end re-configurable multi-protocol anomaly detection pipeline for Internet of Things},
journal = {Internet of Things},
pages = {100437},
year = {2021},
issn = {2542-6605},
doi = {https://doi.org/10.1016/j.iot.2021.100437},
url = {https://www.sciencedirect.com/science/article/pii/S2542660521000810},
author = {Hakan Kayan and Yasar Majib and Wael Alsafery and Mahmoud Barhamgi and Charith Perera}
}

# Known Bugs

- BLE Scanner status is not changing properly after establishing the first connection.
- To reconnect, we need to wait around 10 secs after disconnnecting. Otherwise the connection drops.


