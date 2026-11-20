# Qubes OS Security Lab

**Security Compartmentalization | Xen Virtualization | Linux Administration | Privacy Engineering**

## Executive Summary

A hands-on security engineering lab demonstrating practical experience with Qubes OS, a security-focused operating system built around the Xen hypervisor.

This project documents isolated computing environments, Linux administration, cryptographic workflows, network compartmentalization, and secure file handling.

The objective is to demonstrate practical security engineering skills through documented configurations, controlled workflows, and validation evidence.

## Technical Environment

| Component | Technology |
|---|---|
| Operating System | Qubes OS |
| Hypervisor | Xen |
| Linux Environments | Fedora, Debian |
| Network Privacy | Whonix, Tor |
| Virtualization | TemplateVMs, AppVMs, DisposableVMs |
| Cryptographic Tools | GnuPG, Split-GPG |
| File Sanitization | MAT2, ExifTool |
| Administration | Linux CLI, Bash |

## Security Architecture

Qubes OS implements security through compartmentalization, separating applications and activities into isolated virtual machines.

### Core Components

- **dom0:** Administrative domain responsible for managing the Qubes environment.
- **TemplateVMs:** Provide reusable operating system environments for dependent qubes.
- **AppVMs:** Separate applications and data into distinct security domains.
- **DisposableVMs:** Provide temporary environments for processing untrusted content.
- **Whonix:** Provides Tor-based network privacy through isolated gateway and workstation components.

## Documented Security Workflows

### 1. VM Isolation and Compartmentalization

Security domains are separated to reduce the impact of compromised applications and prevent unnecessary access between workloads.

**Technical focus:**
- Security-domain separation
- Controlled inter-VM communication
- Template-based administration
- Disposable computing environments

### 2. Whonix and Tor Integration

Whonix provides an isolated environment for applications requiring Tor-based network connectivity.

**Technical focus:**
- Network compartmentalization
- Gateway and workstation separation
- Tor-routed application workflows
- Isolation of network-sensitive activities

### 3. Split-GPG Cryptographic Isolation

Split-GPG separates cryptographic operations from applications that request them.

**Technical focus:**
- GnuPG key management
- Isolated cryptographic operations
- Inter-VM communication
- Reduced exposure of private key material

### 4. Secure File Sanitization

Implemented an isolated image-processing workflow using MAT2 and ExifTool.

**Documented workflow:**

1. Transfer an image from a personal qube to an offline processing qube.
2. Remove metadata using MAT2.
3. Inspect the sanitized file using ExifTool.
4. Transfer the cleaned file to a separate disposable environment.
5. Use an isolated Tor-connected environment for subsequent upload.

**Tools used:**
- MAT2 0.13.5
- ExifTool 13.25
- Whonix
- DisposableVMs

This workflow demonstrates separation of file preparation, metadata inspection, and network activity.

## Security Engineering Principles

- Least privilege
- Defense in depth
- Security compartmentalization
- Isolation of sensitive operations
- Reduced attack surface
- Controlled inter-VM communication
- Reproducible security workflows

## Project Roadmap

- [x] Establish Qubes OS working environment
- [x] Implement compartmentalized application workflows
- [x] Work with Whonix and Tor environments
- [x] Implement Split-GPG workflows
- [x] Perform isolated image metadata sanitization
- [ ] Document Qubes architecture with diagrams
- [ ] Add sanitized configuration screenshots
- [ ] Document security validation procedures
- [ ] Add reproducible technical walkthroughs

## Project Status

**Active — Documentation and Security Validation**

This repository is being developed as a technical portfolio demonstrating practical Qubes OS administration, Linux security, virtualization, and privacy-focused system design.

Documentation will be expanded with technical procedures, configuration examples, and validation evidence.

---

**Author:** [Slayerz870](https://github.com/Slayerz870)

**Related Project:** [Enterprise Active Directory Lab](https://github.com/Slayerz870/enterprise-active-directory-lab)
