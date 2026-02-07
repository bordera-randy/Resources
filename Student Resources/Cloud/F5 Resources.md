<!--
---
title: "F5 BIG-IP Resources & Study Guide"
description: "Comprehensive collection of F5 BIG-IP resources including documentation, troubleshooting guides, certifications, and training materials."
tags: ["F5", "BIG-IP", "Load Balancing", "LTM", "Networking", "Certification"]
updated: "2026-02-01"
---
-->
# 🔀 F5 BIG-IP Resources & Study Guide

> **Master F5 BIG-IP load balancing, local traffic management, and F5 certification.**

This comprehensive guide provides resources, documentation, and study materials for F5 BIG-IP administration, certification preparation, and advanced topics.

**Key Topics:**
- BIG-IP Local Traffic Management (LTM)
- Virtual servers, pools, and health monitors
- Profiles, SSL/TLS, and performance optimization
- High availability and failover
- F5 certification exam preparation

---

## 📚 Table of Contents

1. [General Resources](#general-resources)
2. [Virtual Servers](#virtual-servers)
3. [Health Monitors](#health-monitors)
4. [Profiles](#profiles)
5. [Miscellaneous](#miscellaneous)
6. [Certification & Training](#certification--training)
7. [Useful Tools & References](#useful-tools--references)
8. [Back to Top](#-f5-big-ip-resources--study-guide)

---

## 🔧 General Resources

Virtual Lab edition:
https://www.cdw.com/product/big-ip-virtual-edition-lab-license-v.-18.x-license-10-mbps/5623506

Update RDP services on Mac. Remove the Round Icon version, and install the Square Icon version.,
https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12

Silverline Services
https://f5.com/products/deployment-methods/silverline

Lightboard videos on DevCentral
https://devcentral.f5.com/s/global-search/%40uri#q=lightboard%20lessons&sort=relevancy&f:@f5_url_filter=[Articles]
 
OSI and TCPIP Models
https://en.wikipedia.org/wiki/OSI_model
https://devcentral.f5.com/s/articles/lightboard-lessons-osi-and-tcp-ip-models-30201
 
BIG-IP: Life of a packet
https://www.youtube.com/watch?v=qCLEw5xIZ7s
 
Root and admin users must reset default passwords when logging in for the first time
https://support.f5.com/csp/article/K10612010

Enable Persistence Records using TMSH
tmsh modify sys db ui.statistics.modulestatistics.localtraffic.persistencerecords value true
 
BIG-IP 15.1.0 General Release Notes
https://techdocs.f5.com/kb/en-us/products/big-ip_ltm/releasenotes/product/relnote-bigip-15-1-0.html

BIG-IP APM 15.1.0 Knowledge Center
https://support.f5.com/csp/knowledge-center/software/BIG-IP?module=BIG-IP%20LTM&version=15.1.0
## 🎯 Virtual Servers

- [BIG-IP Local Traffic Management: Basics](https://techdocs.f5.com/kb/en-us/products/big-ip_ltm/manuals/product/big-ip-local-traffic-management-basics-14-1-0.html)
- [K8082: TCP connection setup for BIG-IP LTM virtual servers](https://support.f5.com/csp/article/K8082)

---
## 🏥 Health Monitors

- [K2167: Constructing HTTP requests for use with the HTTP or HTTPS application health monitor](https://support.f5.com/csp/article/K2167)
- [K12531: Troubleshooting health monitors](https://support.f5.com/csp/article/K12531)

---


## ⚙️ Profiles

### Protocol Profiles

- [Manual Chapter: Protocol Profiles](https://techdocs.f5.com/en-us/bigip-15-1-0/big-ip-local-traffic-management-profiles-reference.html)
- [K10711911: Overview of the TCP profile (13.x)](https://support.f5.com/csp/article/K10711911)
- [K09948701: Overview of the FastL4 profile](https://support.f5.com/csp/article/K09948701)

### Service Profiles

- [Manual Chapter: Services Profiles](https://techdocs.f5.com/en-us/bigip-15-1-0/big-ip-local-traffic-management-profiles-reference/services-profiles.html)
- [K40243113: Overview of the HTTP profile](https://support.f5.com/csp/article/K40243113)

---
### High Availability & Clustering

- [K94333370: Time sync troubleshooting for HA Failover](https://support.f5.com/csp/article/K94333370)

### SSL/TLS & Security

- [SSL Testing & SSL Labs](https://www.ssllabs.com/ssltest/index.html)

### Networking & Troubleshooting

- [TCP/IP Cheatsheet for TCPDUMP](https://www.sans.org/security-resources/tcpip.pdf)
- [K6546: Recommended methods and limitations for running tcpdump on a BIG-IP system](https://support.f5.com/csp/article/K6546)

### Performance Optimization

- [DevCentral: F5 Fast L4 Acceleration and the F5 Smart Coprocessor](https://devcentral.f5.com/s/articles/F5-Fast-L4-Acceleration-and-the-F5-Smart-Coprocessor-prioritized-Fast-L4-Acceleration)

---


## 🏆 Certification & Training

### F5 Certification

- [K29900360: F5 certification | Exams and study materials](https://support.f5.com/csp/article/K29900360#101)
- [F5 Certified Professionals - Certification Account Registration](https://www.certmetrics.com/f5certified)
- [Practice Exam Studio](https://portal-v5.examstudio.com/Default.aspx?id=20882)
- [F5 Certified Professionals Group on LinkedIn](https://www.linkedin.com/groups/85832)

### Non-F5 Resources

- [Veritable Networks Blog - F5 Exam Resources](https://veritablenetworks.blogspot.com/)

---

## 📖 Useful Tools & References

### Official F5 Training

- [LearnF5 - F5 Online Learning Platform](https://account.f5.com/learnf5)
- [F5 Community Training & Lab Content](https://clouddocs.f5.com/training/community/)
- [F5 Instructor Led Training](https://www.f5.com/services/training#instructorled)

### Remote Access Tools

- [Microsoft Remote Desktop for Mac](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12)
  - **Note:** Install the Square Icon version (newer) and remove the Round Icon version (legacy)

---

**Back to [Student Resources](../readme.md)**