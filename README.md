# 🚀 DPI Engine - Deep Packet Inspection System

> High-Performance Network Traffic Analysis & Application Classification Engine

Developed by **Ashutosh Sharma**

## 📖 Overview

DPI Engine is a C++17-based Deep Packet Inspection (DPI) system designed to analyze, classify, and control network traffic from PCAP captures. The engine inspects packet payloads, extracts application-level metadata such as TLS Server Name Indication (SNI), identifies applications like YouTube, Facebook, Google, and GitHub, and applies customizable blocking policies.

Unlike traditional firewalls that only inspect packet headers, this engine performs deep inspection of network traffic while maintaining high performance through a scalable multi-threaded architecture.

---

## ✨ Key Features

### 🔍 Deep Packet Inspection

* Parses Ethernet, IPv4, TCP, and UDP packets
* Extracts TLS SNI from HTTPS Client Hello packets
* Detects application traffic without decrypting encrypted payloads
* Supports HTTP Host Header inspection

### 🎯 Application Classification

Automatically identifies traffic belonging to:

* YouTube
* Facebook
* Google Services
* GitHub
* DNS
* HTTP/HTTPS
* Custom Applications

### 🚫 Intelligent Traffic Blocking

Supports rule-based filtering:

* IP-based blocking
* Application-based blocking
* Domain/SNI-based blocking
* Flow-level traffic enforcement

### ⚡ High-Performance Multi-Threading

* Reader Thread
* Load Balancer Threads
* Fast Path Processing Threads
* Output Writer Thread
* Thread-Safe Queues
* Consistent Hashing for flow affinity

---

## 🏗️ Architecture

```text
Input PCAP
    │
    ▼
┌──────────────┐
│ Packet Reader│
└──────┬───────┘
       ▼
┌──────────────┐
│ LoadBalancer │
└──────┬───────┘
       ▼
┌──────────────┐
│ Fast Path DPI│
│ Processing   │
└──────┬───────┘
       ▼
┌──────────────┐
│ Rule Engine  │
└──────┬───────┘
       ▼
┌──────────────┐
│ Output PCAP  │
└──────────────┘
```

---

## 🧠 Core Technologies

* **C++17**
* Multi-threaded Programming
* Network Packet Parsing
* TLS Handshake Analysis
* SNI Extraction
* Flow Tracking
* Producer-Consumer Architecture
* Thread-Safe Queues
* Hash-Based Load Balancing
* PCAP File Processing

---

## 🔬 How It Works

### Packet Processing Pipeline

1. Read packets from a PCAP capture.
2. Parse Ethernet, IP, TCP, and UDP headers.
3. Generate a Five-Tuple Flow Identifier.
4. Extract TLS SNI or HTTP Host information.
5. Classify traffic into applications.
6. Apply blocking rules.
7. Forward or drop packets.
8. Generate traffic analytics and reports.

---

## 📊 Supported Detection Techniques

### HTTPS Traffic Analysis

The engine extracts TLS Server Name Indication (SNI) during the Client Hello handshake:

```text
Client Hello
    └── SNI Extension
          └── www.youtube.com
```

This allows application identification without decrypting encrypted HTTPS traffic.

### Flow Tracking

Each connection is tracked using:

```cpp
Source IP
Destination IP
Source Port
Destination Port
Protocol
```

This ensures all packets belonging to the same connection are processed consistently.

---

## 📁 Project Structure

```text
packet_analyzer/
│
├── include/
│   ├── pcap_reader.h
│   ├── packet_parser.h
│   ├── sni_extractor.h
│   ├── connection_tracker.h
│   ├── rule_manager.h
│   └── dpi_engine.h
│
├── src/
│   ├── main_working.cpp
│   ├── dpi_mt.cpp
│   ├── pcap_reader.cpp
│   ├── packet_parser.cpp
│   ├── sni_extractor.cpp
│   └── types.cpp
│
├── generate_test_pcap.py
├── test_dpi.pcap
└── README.md
```

---

## 🚀 Performance-Oriented Design

The multi-threaded engine distributes workload using:

* Consistent Hashing
* Load Balancers
* Fast Path Workers
* Independent Flow Tables
* Concurrent Packet Processing

This design ensures:

✅ Scalable performance

✅ Flow consistency

✅ Low processing latency

✅ Efficient CPU utilization

---

## 🛠️ Build & Run

### Build

```bash
g++ -std=c++17 -pthread -O2 -I include -o dpi_engine \
src/dpi_mt.cpp \
src/pcap_reader.cpp \
src/packet_parser.cpp \
src/sni_extractor.cpp \
src/types.cpp
```

### Run

```bash
./dpi_engine input.pcap output.pcap
```

### Apply Blocking Rules

```bash
./dpi_engine input.pcap output.pcap \
--block-app YouTube \
--block-domain facebook \
--block-ip 192.168.1.50
```

---

## 📈 Example Use Cases

* Network Traffic Analysis
* Enterprise Security Monitoring
* Application Usage Tracking
* Educational Networking Labs
* Firewall Research
* Traffic Classification Systems
* Cybersecurity Projects

---

## 🎯 What I Learned

Through this project, I gained hands-on experience with:

* Network Protocol Internals
* TCP/IP Stack Analysis
* Deep Packet Inspection
* TLS Handshake Processing
* Concurrent Programming
* Thread Synchronization
* High-Performance System Design
* Packet Capture (PCAP) Processing
* Flow-Based Traffic Management

---

## 👨‍💻 Developer

### Ashutosh Sharma

**AI Engineer | Python Developer | FastAPI Expert | Systems Programmer**

Passionate about building scalable backend systems, AI-powered applications, networking tools, and high-performance software.

---

⭐ If you found this project interesting, consider giving it a star and exploring the codebase!
