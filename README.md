# EARB -- Encrypted Binary Release Artifacts

## Overview

`encrypted-binary-release-artifacts` is a centralized public distribution repository for encrypted binary release artifacts generated from private source repositories.

This repository is designed to provide a unified binary distribution platform for multiple software projects.

Source code, development resources, and CI/CD workflows are maintained in private repositories. Only encrypted, verified, and release-ready binary artifacts are published here.

This repository **does not contain source code**.

---

# Purpose

The purpose of this repository is to provide a secure and standardized distribution channel for software binary releases.

The general workflow:

```

Private Source Repository
|
|
GitHub Actions
|
|
Build Binary Artifacts
|
|
Encrypt & Package Artifacts
|
|
Generate Checksums & Signatures
|
|
Publish GitHub Release
|
|
Encrypted Binary Release Artifacts

```

---

# Repository Scope

This repository supports multiple independent software projects.

Each project maintains:

- Private source repository
- Independent CI/CD pipeline
- Independent release lifecycle
- Independent version management

This repository only stores final release artifacts.

---

# Repository Organization

Each project is managed through GitHub Releases.

Example:

```

encrypted-binary-release-artifacts

Releases:

project-a-v1.0.0

```
Assets:
├── project-a-v1.0.0-linux-amd64.7z
├── project-a-v1.0.0-linux-arm64.7z
├── project-a-v1.0.0-windows-amd64.7z
└── SHA256SUMS
```

project-b-v2.1.0

```
Assets:
├── project-b-v2.1.0-linux-amd64.7z
└── SHA256SUMS
```

```

---

# Release Naming Convention

All releases should follow:

```

<ProjectName>-v<Version>

```

Examples:

```

mytool-v1.0.0

server-agent-v2.3.0

backup-manager-v1.5.2

```

---

# Artifact Naming Convention

All release artifacts should follow:

```

<ProjectName>-<Version>-<OS>-<Architecture>.<Format>

```

Examples:

```

mytool-v1.0.0-linux-amd64.7z

mytool-v1.0.0-linux-arm64.7z

mytool-v1.0.0-windows-amd64.7z

mytool-v1.0.0-darwin-arm64.7z

```

---

# Supported Platforms

Default build targets:

| Operating System | Architecture |
|------------------|--------------|
| Linux            | amd64        |
| Linux            | arm64        |
| Windows          | amd64        |
| macOS            | arm64        |

Additional platforms may be added according to project requirements.

---

# Artifact Security

All artifacts published in this repository should follow secure software distribution practices.

Recommended security measures:

- AES-256 encrypted archives
- SHA256 checksum verification
- Digital signatures
- Automated CI/CD publishing
- Build provenance tracking
- Reproducible builds when possible

Example release assets:

```

mytool-v1.0.0-linux-amd64.7z

mytool-v1.0.0-linux-amd64.sha256

mytool-v1.0.0-linux-amd64.sig

```

---

# Encryption Policy

Binary artifacts may be encrypted before publication.

Example:

```

Original Binary

```
    |
    |
    v
```

Encrypted Archive

```
    |
    |
    v
```

GitHub Release Asset

````

Encrypted packages require valid credentials for extraction.

Without the correct decryption credentials, the contents of the release package cannot be accessed.

---

# Integrity Verification

Users should verify downloaded artifacts before use.

## Linux / macOS

```bash
sha256sum -c SHA256SUMS
````

## Windows PowerShell

```powershell
Get-FileHash .\filename -Algorithm SHA256
```

---

# CI/CD Release Pipeline

All projects publishing artifacts to this repository should follow a standardized release workflow.

Recommended pipeline:

```
Private Repository

        |
        v

Source Checkout

        |
        v

Build

        |
        v

Automated Tests

        |
        v

Binary Packaging

        |
        v

Encryption

        |
        v

Checksum Generation

        |
        v

Release Publishing

        |
        v

GitHub Release Assets
```

---

# Version Management

All projects should follow Semantic Versioning:

```
MAJOR.MINOR.PATCH
```

Examples:

```
v1.0.0

v1.2.5

v2.0.0
```

Version rules:

| Version Part | Description                       |
| ------------ | --------------------------------- |
| MAJOR        | Breaking changes                  |
| MINOR        | New features                      |
| PATCH        | Bug fixes and maintenance updates |

---

# Source Code Policy

This repository does not store source code.

Source code remains in private repositories.

The following items are published:

* Compiled binaries
* Encrypted release packages
* Checksums
* Digital signatures
* Release notes
* Build metadata (when applicable)

The following items must never be published:

* Source code
* Private keys
* Access tokens
* CI/CD credentials
* Internal configuration files

---

# Software Supply Chain Security

Projects using this repository should follow modern software supply chain security practices.

Recommended:

* Protected source repositories
* Automated CI/CD builds
* Secret management
* Artifact signing
* Integrity verification
* Dependency scanning
* SBOM generation

---

# Download Process

Typical user workflow:

```
1. Open GitHub Releases

2. Select required version

3. Download platform-specific artifact

4. Verify SHA256 checksum

5. Extract encrypted package

6. Run application
```

---

# License

Each project distributed through this repository maintains its own license and usage terms.

Artifacts are subject to the corresponding project's license agreement.

---

# Maintenance

This repository is maintained as a centralized binary distribution platform.

For project-specific documentation, installation instructions, and support information, please refer to the corresponding project repository.

---

# Maintainer

Maintained by the project owner.

This repository provides a secure and standardized delivery channel for encrypted binary software releases.

