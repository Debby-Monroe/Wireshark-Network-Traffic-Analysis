# Network Traffic Analysis & Protocol Investigation Lab

## 📝 Project Overview

This project demonstrates core Security Operations Center (SOC) analyst workflows using **Wireshark** to investigate network traffic, validate protocol handshakes, and reconstruct application-layer objects from packet captures. Through hands-on analysis of `.pcap` files, I examined network communications, verified protocol behavior, and extracted application-layer metadata to distinguish normal activity from potential anomalies.

## 🛠️ Skills & Tools Demonstrated

* **Tooling:** Wireshark, macOS Terminal
* **Protocols Analyzed:** TCP (Three-Way Handshake), HTTP (POST Requests), PKIX-CMP
* **Core Competencies:** Network traffic analysis, protocol investigation, packet inspection, application-layer analysis, and security reporting

---

## 🔬 Investigation Breakdown

### Phase 1: TCP Session Establishment & Protocol Validation

Using a packet capture containing web application traffic over port `8080`, I analyzed the network session lifecycle from connection establishment through application-layer communication.

#### Verifying the TCP Three-Way Handshake

Before application data transmission occurred, the following TCP handshake was observed:

1. `59935 → 8080 [SYN]`
2. `8080 → 59935 [SYN, ACK]`
3. `59935 → 8080 [ACK]`

This sequence confirms successful session establishment between the client and server.

**Analyst Insight:** Port scanning activity often generates large volumes of SYN packets across multiple destination ports without completing full sessions. In this capture, the communication remained focused on a single destination port and completed a normal TCP handshake before transferring application data, indicating legitimate session establishment.

![TCP Handshake and HTTP Packet Headers](./handshake_and_headers.png)

---

### Phase 2: Application-Layer Analysis & Certificate Traffic Investigation

After the TCP session was established, the client initiated HTTP POST requests carrying certificate-management data.

```text
Protocol: Hypertext Transfer Protocol (HTTP)
Request Method: POST
Content-Type: application/pkixcmp
Payload Size: 578 bytes
```

The packet inspection revealed PKIX Certificate Management Protocol (PKIX-CMP) traffic encapsulated within HTTP POST requests. This protocol is commonly used for certificate enrollment, renewal, and management operations within Public Key Infrastructure (PKI) environments.

By examining the application-layer headers and payload metadata, I was able to identify the protocol purpose and validate the legitimacy of the transaction.

---

## 🔎 Investigation Summary

The packet capture revealed a normal TCP session lifecycle consisting of connection establishment, application-layer communication, and successful data transfer.

Analysis confirmed:

- Successful TCP three-way handshake
- HTTP POST activity over port 8080
- PKIX-CMP certificate management traffic
- No indicators of port scanning behavior
- No malformed packets or protocol violations observed

The traffic appeared consistent with legitimate application communication rather than suspicious or malicious activity.

---

## 📚 Key Takeaway

This project demonstrates how packet analysis can be used to validate network communications, investigate protocol behavior, and distinguish normal operational traffic from suspicious activity. Using Wireshark, I traced session establishment, inspected application-layer requests, and interpreted packet-level evidence to support investigative conclusions.
