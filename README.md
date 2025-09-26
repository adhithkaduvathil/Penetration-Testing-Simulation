# Wireshark-Traffic-Analysis

## Overview
This small lab demonstrates basic network traffic analysis using **Wireshark** in a controlled environment. The goal is to capture packets, identify common protocols and suspicious patterns, and document findings. This repo is intended for educational use in an isolated lab only.

**Note:** Do not capture traffic from networks you do not own or have explicit permission to test.

---

## Tools Used
- **Wireshark** – packet capture and analysis
- **tcpdump** – optional command-line packet capture
- **Kali Linux / Ubuntu** – where captures were performed

---

## Files in this repo
- `README.md` — this document  
- `sample_capture_summary.txt` — short, sanitized text summary of a sample capture (included below)  
- `screenshots/` — place screenshots of Wireshark views here (optional)

---

## How to reproduce (lab steps)
1. Create an isolated network with at least two VMs (attacker and target).  
2. Start a packet capture in Wireshark on the lab network interface.  
3. Generate benign traffic (browsing, ping) and a small simulated suspicious event (e.g., repeated ICMP pings or a port scan from attacker VM).  
4. Stop capture and save the `.pcap` file.  
5. Open the capture in Wireshark and filter, for example:  
   - `ip.addr == 192.168.56.101` (filter by host)  
   - `tcp.flags.syn == 1 and tcp.flags.ack == 0` (show SYN scans)  
6. Export a screenshot of the packet list and add it to `screenshots/`.

---

## Sample findings (sanitized)
See `sample_capture_summary.txt` for a short extract showing common protocol lines and an example of suspicious activity (SYN scan). The sample includes lines like:

## Sample Finding: SYN Scan Detection

The following screenshot shows captured TCP SYN packets from host `10.28.70.131` to multiple destinations. Using the filter `tcp.flags.syn == 1 && tcp.flags.ack == 0`, we observed repeated SYNs with retransmissions and no completed handshakes. This indicates a **SYN scan**—a reconnaissance technique used to identify open ports and services.

![SYN Scan Screenshot](screenshots/syn_scan_filter.png)

