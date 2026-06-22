# Deep Packet Inspection (DPI) Engine

A high-performance **multithreaded Deep Packet Inspection (DPI) Engine** built in **C++17** for analyzing network traffic from PCAP captures, extracting application-level metadata, classifying traffic, and applying rule-based filtering.

The engine processes raw packets through a scalable pipeline of load balancer and worker threads, enabling efficient traffic inspection while preserving flow consistency.

---

## Highlights

- Multithreaded DPI pipeline with Reader → Load Balancer → Fast Path architecture
- Flow-aware packet processing using 5-tuple hashing
- TLS SNI extraction for encrypted HTTPS traffic classification
- Supports 15+ application signatures including YouTube, Netflix, GitHub, Discord, Spotify and Zoom
- Rule-based filtering using IP, domain and application policies
- Generates analytics reports and filtered PCAP outputs

---

## Overview

Modern networks carry encrypted traffic where traditional port-based classification is often insufficient.

This project performs:

* Packet parsing across multiple protocol layers
* Five-tuple flow tracking
* TLS Server Name Indication (SNI) extraction
* Application identification
* Rule-based traffic filtering
* Real-time traffic analytics generation

The system is inspired by core concepts used in enterprise firewalls, intrusion detection systems, and traffic management platforms.

---

## Key Features

### Network Protocol Support

* Ethernet
* IPv4
* TCP
* UDP
* TLS Client Hello parsing
* HTTP Host extraction
* DNS traffic detection

### Application Identification

Classifies traffic into applications such as:

* YouTube
* Netflix
* GitHub
* Google
* Facebook
* Instagram
* Discord
* Telegram
* Spotify
* TikTok
* Zoom
* Apple
* Microsoft
* Amazon
* Cloudflare

### Traffic Inspection

* Five-tuple flow tracking
* TLS SNI extraction
* Host header analysis
* Flow-level state management

### Rule Engine

Supports:

* IP blocking
* Domain blocking
* Application blocking

### Reporting

Generates:

* Traffic statistics
* Application distribution
* Flow analytics
* Classified domain reports
* Filtered PCAP output

---

## System Architecture

```text
                    +------------------+
                    |   PCAP Reader    |
                    +---------+--------+
                              |
                              v
                    +------------------+
                    | Load Balancers   |
                    +---------+--------+
                              |
          +-------------------+-------------------+
          |                   |                   |
          v                   v                   v
    +-----------+      +-----------+      +-----------+
    | Fast Path |      | Fast Path |      | Fast Path |
    | Worker 1  |      | Worker 2  |      | Worker N  |
    +-----+-----+      +-----+-----+      +-----+-----+
          |                  |                  |
          +------------------+------------------+
                              |
                              v
                    +------------------+
                    | Output Writer    |
                    +---------+--------+
                              |
                              v
                     Filtered PCAP File
```

---

## Packet Processing Pipeline

```text
Packet Capture
      │
      ▼
Ethernet Parsing
      │
      ▼
IPv4 Parsing
      │
      ▼
TCP / UDP Parsing
      │
      ▼
Flow Tracking (5-Tuple)
      │
      ▼
TLS SNI / HTTP Host Extraction
      │
      ▼
Application Classification
      │
      ▼
Rule Evaluation
      │
      ▼
Forward / Drop Decision
      │
      ▼
Analytics & Reporting
```

---

## Five-Tuple Flow Tracking

Each flow is uniquely identified using:

```text
(Source IP,
 Destination IP,
 Source Port,
 Destination Port,
 Protocol)
```

This guarantees packets belonging to the same connection are processed consistently by the same worker thread.

---

## Multithreading Design

The engine follows a producer-consumer architecture:

### Reader Thread

Reads packets from PCAP files.

### Load Balancer Threads

Distribute packets based on flow hashing.

### Fast Path Workers

Perform:

* Protocol parsing
* Flow tracking
* TLS inspection
* Application classification
* Rule evaluation

### Output Thread

Writes approved packets into a filtered PCAP.

This design improves throughput while preserving packet ordering within flows.

---

## TLS SNI Extraction

Even when HTTPS payloads are encrypted, the TLS Client Hello contains the Server Name Indication (SNI) field.

Example:

```text
www.youtube.com
github.com
open.spotify.com
```

The engine extracts SNI values and maps them to applications before encryption begins.

---

## Build Instructions

### Windows (GCC)

```bash
g++ -std=c++17 -pthread -O2 -I include ^
    -o dpi_engine.exe ^
    src/dpi_mt.cpp ^
    src/pcap_reader.cpp ^
    src/packet_parser.cpp ^
    src/sni_extractor.cpp ^
    src/types.cpp
```

### Run

```bash
dpi_engine.exe test_dpi.pcap output.pcap
```

Block specific applications:

```bash
dpi_engine.exe input.pcap output.pcap --block-app YouTube
```

Block specific domains:

```bash
dpi_engine.exe input.pcap output.pcap --block-domain youtube.com
```

---

## Technologies Used

* C++17
* Multithreading
* TCP/IP Networking
* Packet Processing
* TLS Inspection
* Concurrent Programming
* System Design
* PCAP Analysis
* STL Containers & Algorithms

---

## Future Enhancements

* IPv6 support
* QUIC protocol inspection
* Real-time packet capture
* Machine-learning based traffic classification
* REST API integration
* Web dashboard for analytics
* Performance benchmarking suite

---

## Author

Satyam Kumar

