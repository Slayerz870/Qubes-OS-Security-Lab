# Qubes OS Security Architecture

**Project:** Qubes OS Security Lab  
**Focus:** Xen Virtualization, Security Compartmentalization, Network Isolation, and Cryptographic Separation

## 1. Architecture Overview

Qubes OS is a security-focused operating system built on the Xen hypervisor. Its architecture isolates applications and workloads into separate virtual machines called *qubes*.

Rather than relying exclusively on application-level security, Qubes OS uses virtualization to establish boundaries between different computing activities.

This lab explores these isolation mechanisms through practical Linux administration, compartmentalized workflows, Whonix networking, and Split-GPG.

## 2. Logical Architecture

```text
                  QUBES OS HOST
                 Xen Hypervisor
                        |
         +--------------+--------------+
         |              |              |
       dom0         TemplateVMs      AppVMs
         |              |              |
   Qube Management   Fedora/Debian  +-- personal
         |                         +-- work
         |                         +-- vault
         |                         +-- media-cleaner
         |
         +---------- Qube Lifecycle Management
                                    |
                              DisposableVMs
                                    |
                         Temporary Isolated Tasks

                  NETWORK ISOLATION
                         |
                    sys-net
                         |
                    sys-firewall
                         |
                    sys-whonix
                         |
                    Whonix/Tor
                         |
                 Tor-Connected Qubes
```

*Conceptual diagram illustrating Qubes OS components and possible trust boundaries. It is not a verified inventory of the current host.*

## 3. Core Security Components

### dom0 — Administrative Domain

dom0 is the privileged administrative domain responsible for managing the Qubes environment.

Responsibilities include:

- Managing qube lifecycle operations.
- Controlling administrative interfaces.
- Managing VM configurations and assignments.
- Coordinating access to virtualized resources.

**Security principle:** Avoid running untrusted applications or routine internet-facing workloads in dom0.

### TemplateVMs

TemplateVMs provide shared operating system software environments for template-based qubes.

Common templates include Fedora and Debian.

Their primary benefits include centralized software maintenance, standardized configurations, and reduced duplication.

### AppVMs

AppVMs provide isolated environments for applications and persistent user data.

Separate AppVMs can be assigned to different activities according to their security requirements.

Example security domains include personal computing, work-related tasks, and offline file processing.

### DisposableVMs

DisposableVMs provide temporary environments for tasks that benefit from short-lived isolation.

They are useful for opening untrusted documents, processing files, and performing activities that should not persist in an ordinary AppVM.

Disposable environments reduce persistence but do not guarantee that malicious activity cannot affect external systems or accessible resources.

## 4. Network Architecture

Qubes OS can separate networking responsibilities into dedicated service qubes.

### sys-net

Provides access to physical networking hardware.

### sys-firewall

Provides an additional network policy enforcement layer between application qubes and network access.

### sys-whonix

Provides Tor-based networking for qubes configured to use the Whonix gateway.

Whonix separates Tor gateway functionality from applications that access the network.

**Important:** Tor routing does not guarantee anonymity. Application behavior, identity disclosure, configuration, and operational practices still matter.

## 5. Cryptographic Isolation — Split-GPG

Split-GPG separates cryptographic key operations from applications requesting them.

The architecture consists of:

- A trusted qube containing protected GnuPG key material.
- A separate application qube that requests cryptographic operations.
- Controlled inter-qube communication between the application and key-handling environments.

This approach reduces direct exposure of private key material to application environments.

It does not eliminate risks associated with compromised trusted qubes, malicious requests, or user authorization mistakes.

## 6. Isolated File Sanitization Workflow

A practical workflow explored in this lab uses an offline qube for image metadata sanitization.

```text
       Personal Qube
             |
             | Controlled File Transfer
             v
     Offline media-cleaner
             |
        MAT2 / ExifTool
             |
      Metadata Inspection
             |
             v
      Disposable Environment
             |
        Whonix / Tor
             |
             v
       External Upload
```

### Workflow

1. Transfer an image into an offline processing qube.
2. Use MAT2 to sanitize supported metadata.
3. Inspect the output using ExifTool.
4. Transfer the processed image into an isolated environment for subsequent handling.
5. Use a Tor-connected environment when appropriate for the intended workflow.

### Security Considerations

- Metadata removal does not guarantee complete anonymization.
- File contents may still reveal identifying information.
- Sanitization effectiveness depends on file format and tool behavior.
- Cross-qube transfers should be deliberate and limited to required files.
- Network access should be restricted according to workload requirements.

## 7. Security Design Principles

| Principle | Implementation |
|---|---|
| Compartmentalization | Separate activities into isolated qubes |
| Least Privilege | Restrict access to resources and administrative capabilities |
| Defense in Depth | Combine virtualization, network controls, and application security |
| Cryptographic Isolation | Separate private key operations from requesting applications |
| Network Separation | Use dedicated networking service qubes |
| Ephemeral Execution | Use DisposableVMs for suitable temporary workloads |
| Data Minimization | Inspect and sanitize files before external sharing |

## 8. Validation Roadmap

The following checks will be documented as the repository develops:

- [ ] Record the actual qube inventory using sanitized command output.
- [ ] Document template assignments and update procedures.
- [ ] Verify network assignments for selected qubes.
- [ ] Validate offline qube network isolation.
- [ ] Document Split-GPG configuration and controlled testing.
- [ ] Document metadata sanitization with before-and-after verification.
- [ ] Capture sanitized screenshots demonstrating the configured architecture.

## 9. Documentation Scope

This document describes Qubes OS architectural concepts and security workflows relevant to the lab.

The diagrams are conceptual. Actual configuration details will be added after verification on the Qubes host.

No private keys, authentication secrets, personal metadata, or sensitive configuration values should be committed to this repository.

---

**Repository:** [Qubes OS Security Lab](https://github.com/Slayerz870/Qubes-OS-Security-Lab)

**Related Project:** [Enterprise Active Directory Lab](https://github.com/Slayerz870/enterprise-active-directory-lab)
