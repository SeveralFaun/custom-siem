# Setup Notes - Custom SIEM (ELK Stack)

This document outlines the technical setup, configuration changes, and log forwarding steps used to build a lightweight custom SIEM using the ELK stack in a local lab environment.

---

## Environment Overview

* **Host OS:** Windows 11 (with VMware Workstation)
* **Virtual Machines:**

  * `elk-siem` (Ubuntu, Docker ELK stack)
  * `kali-linux` (attacker/log source)
  * `metasploitable2` (vulnerable target)
* **Network Mode:** NAT + Host-only Adapter

---

## ELK Stack Setup (Docker)

* Cloned and customized [`docker-elk`](https://github.com/deviantony/docker-elk)
* Modified `logstash.conf` to receive logs from Filebeat on port `5044`
* Disabled `xpack.security` in Elasticsearch and Kibana configs to simplify access
* Launched the stack:

  ```bash
  cd docker-elk
  docker-compose up -d
  ```

---

## Kibana Configuration

* Accessed via `http://<ELK-IP>:5601`
* Created index pattern: `filebeat-*`
* Verified incoming logs from Filebeat (Kali Linux)
* Built visualizations for SSH login attempts and failed auth

---

## Filebeat Setup on Kali Linux

### Installation

```bash
sudo dpkg -i filebeat-7.17.29-amd64.deb
```

### Configuration

Edited `/etc/filebeat/filebeat.yml`:

```yaml
filebeat.inputs:
  - type: log
    paths:
      - /var/log/*.log

output.logstash:
  hosts: ["<ELK-IP>:5044"]
```

### Execution

```bash
sudo filebeat -e
```

Used `journalctl -u filebeat` to verify logs were being sent.

---

## Monitoring & Testing

* Used Kali to perform brute-force SSH logins against Metasploitable
* Monitored `/var/log/*.log` for log entries
* Verified those logs appeared in Kibana under `filebeat-*`
* Confirmed dashboards updated in real time

---

## Relevant File Paths

| File/Folder                                  | Purpose                         |
| -------------------------------------------- | ------------------------------- |
| `docker-elk/logstash/pipeline/logstash.conf` | Logstash input/output config    |
| `filebeat.yml` (on Kali)                     | Filebeat config to forward logs |
| `screenshots/`                               | Visuals of dashboards and setup |

---

## Status

SIEM successfully receives and visualizes logs from Kali Linux in real time using Filebeat + Logstash.

[Kali Log on Kibana](../screenshots/elk_logs.png)

Further improvements could include:

* Adding log sources from Metasploitable
* Creating custom dashboards for specific alerts
* Ingesting data from more complex attack chains
