# Web Lab 4 – Secure server

## Overview

This practice is a direct continuation of **WebLab02**. The existing infrastructure (DNS, Apache HTTP VirtualHost, authentication, and document structure) is reused without modification. The objective of this lab is to extend the previous setup by adding **HTTPS support** using **SSL/TLS** with a **self-signed certificate**.

The environment is deployed using **Vagrant** and **VirtualBox**, following the same configuration and project layout established in the previous laboratory.


## Infrastructure Description

The environment consists of two virtual machines already configured in WebLab02:

- **dns.sistema.sol**  
  Provides authoritative DNS resolution for the domain `sistema.sol`.

- **tierra.sistema.sol**  
  Hosts the Apache web server and serves the website `discovery.sistema.sol`.

All DNS resolution, HTTP configuration, authentication mechanisms, and directory structures from the previous lab are preserved and reused.



## HTTPS Configuration

### SSL/TLS Support

HTTPS support is added by enabling the SSL module in Apache and configuring a new secure VirtualHost listening on port **443**.

A **self-signed SSL certificate** is generated using OpenSSL with the following characteristics:
- RSA 2048-bit key
- Validity period of 365 days
- Common Name (CN): `discovery.sistema.sol`

This certificate is used exclusively for academic and testing purposes.
---

## Apache Secure VirtualHost

A new Apache VirtualHost is created for HTTPS with the following properties:
- Protocol: HTTPS
- Port: 443
- ServerName: `discovery.sistema.sol`
- DocumentRoot: `/var/www/discovery.sistema.sol`

The same DocumentRoot used for HTTP is reused for HTTPS to ensure consistent content delivery across both protocols.


## Host System Considerations (macOS Apple Silicon)

The host system used for this practice is **macOS running on Apple Silicon (M2)**.

Due to compatibility limitations between **VirtualBox**, **Vagrant**, and Apple Silicon, the virtual machines are deployed using an **internal network with port forwarding**.

For HTTPS access, port **443** on the virtual machine is forwarded to port **8081** on the host system. To allow proper name-based virtual hosting from the host browser, the `/etc/hosts` file on the host machine was manually modified as follows:
```bash
127.0.0.1 discovery.sistema.sol
```
This allows access to the secure website using the following URL: **https://discovery.sistema.sol:8081**

A browser security warning is expected due to the use of a self-signed certificate and must be manually accepted.



## Evidence

All required configuration files and screenshots demonstrating the correct HTTPS configuration and operation of the secure web server are included in the **`evidences`** directory, as required by the lab instructions.



## Conclusion

This practice demonstrates how an existing web infrastructure can be extended with HTTPS support using SSL/TLS. By reusing the configuration from WebLab02 and adding a self-signed certificate, secure communication is achieved in a controlled academic environment, fulfilling all the requirements specified in WebLab04.