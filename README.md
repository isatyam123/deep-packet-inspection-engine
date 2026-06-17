# Deep Packet Inspection Engine

A high-performance Deep Packet Inspection (DPI) engine built in C++ for analyzing network traffic from PCAP files. The project parses network packets, tracks connections, extracts protocol information, and performs rule-based traffic inspection using a multithreaded architecture.

## Features

* Packet analysis from PCAP files
* Ethernet frame parsing
* IPv4 packet inspection
* TCP and UDP protocol parsing
* Connection tracking
* Deep Packet Inspection (DPI)
* HTTPS SNI extraction
* Rule-based traffic filtering
* Multithreaded packet processing
* Traffic classification

## Tech Stack

* C++
* STL
* Multithreading
* Networking Concepts
* PCAP Processing
* CMake

## Project Structure

```text
.
├── include/
├── src/
├── CMakeLists.txt
├── README.md
└── test files
```

## Build Instructions

```bash
mkdir build
cd build
cmake ..
make
```

## Applications

* Network traffic monitoring
* Protocol analysis
* Security research
* Traffic classification
* Deep Packet Inspection studies

## Future Improvements

* Real-time packet capture
* Intrusion Detection System (IDS) integration
* Machine Learning based traffic classification
* Web dashboard for traffic visualization

## Author

Satyam Kumar
