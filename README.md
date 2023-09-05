# Kubernetes Deployments

This document outlines various Kubernetes (k8s) deployments used on my server.

### 🏗️ THIS DOCUMENT IS STILL UNDER CONSTRUCTION 🏗️

---

## Table of Contents
1. [Setup](#setup)
   - [Prerequisites](#prerequisites)
   - [Configuration](#configuration)
     - [MetalLB](#metallb)
2. [Architecture](#architecture)
3. [Security](#security)
4. [Monitoring & Logging](#monitoring--logging)
5. [Troubleshooting](#troubleshooting)
6. [Backups](#backups)
7. [Upgrades](#upgrades)
8. [API Endpoints](#api-endpoints)
9. [Contributing](#contributing)
10. [License](#license)
11. [Acknowledgments](#acknowledgments)

---

## Setup

### Prerequisites

- **Kubernetes Stack**: Either [Kubernetes](https://kubernetes.io/docs/setup/) or [microk8s](https://microk8s.io/docs/getting-started) should be installed. I utilize `microk8s` on an Ubuntu Server for my setup.
  - **IPv6 Note**: If you intend to use IPv6 with `microk8s`, consult [these instructions](https://microk8s.io/docs/explain-dual-stack) *prior* to installation.

- **Load Balancer**: Install [MetalLB](https://metallb.universe.tf/) if you wish to implement `LoadBalancer`. `NodePort` is an alternative.
  
- **Miscellaneous**: A cup of ☕

> **Note**: These instructions are geared towards a `microk8s` setup. For a general Kubernetes setup, please consult appropriate resources.

---

### Configuration

#### MetalLB

To enable MetalLB, execute the following command:

```bash
sudo microk8s enable metallb
```

Upon activation, MetalLB will prompt you for an IP address range for service allocation. Ensure that the selected range does not conflict with IP addresses already in use by other devices or services. Typically, for small local networks, the IP range begins with 192.168.xxx.xxx. For instance, you might specify the range as 192.168.0.50-192.168.0.59.

To confirm your current network configuration and available IP ranges, execute the following command:

```sh
ip -o addr
```

The command will return something similar to this:
```bash
1: lo    inet 127.0.0.1/8 scope host lo\       valid_lft forever preferred_lft forever
1: lo    inet6 ::1/128 scope host noprefixroute \       valid_lft forever preferred_lft forever
2: enp5s0    inet 192.168.0.11/24 brd 10.0.0.255 scope global noprefixroute enp5s0\       valid_lft forever preferred_lft forever
2: enp5s0    inet6 fe80::8a51:f645:4d98:8ed5/64 scope link noprefixroute \       valid_lft forever preferred_lft forever
```

---
