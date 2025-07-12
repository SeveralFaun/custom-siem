# 🛡️ Custom SIEM with Docker ELK

This repository contains a customized version of the [docker-elk](https://github.com/deviantony/docker-elk) stack, tailored for use in a local cybersecurity lab. It provides a lightweight SIEM (Security Information and Event Management) environment using:

- **Elasticsearch** for storing and indexing logs  
- **Logstash** for parsing and forwarding logs  
- **Kibana** for visualizing security events  

---

## ⚙️ Features

- Preconfigured for use with **Kali Linux** and **Metasploitable2**
- Accepts and parses logs like `/var/log/auth.log`
- Visualizes login attempts, brute force attacks, and other system events
- Forward logs using `Filebeat`, `scp`, or other mechanisms
- Built for **learning**, **practicing detection engineering**, and **resume projects**

---

## 🚀 Getting Started

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

---

### Quick Start

1. Clone the repository:
    ```bash
    git clone https://github.com/severalfaun/custom-siem.git
    cd custom-siem/docker-elk

2. Start the ELK stack
    ```bash
    docker-compose up -d

3. Access Kibana:
    `http://localhost:5601`

## 📌 Use Cases

- Learn how SIEMs process real log data
Build dashboards for security events
Practice blue team skills like log analysis
Prep for security engineering of SOC roles

## 🧾 Credits

This project is based on [docker-elk](https://github.com/deviantony/docker-elk) by [@deviantony](https://github.com/deviantony).