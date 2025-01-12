# KASM Hashcat Workspace
[![Docker Pulls](https://img.shields.io/docker/pulls/williamsct1/kasm-hashcat)](https://hub.docker.com/r/williamsct1/kasm-hashcat)
[![Docker Image Size](https://img.shields.io/docker/image-size/williamsct1/kasm-hashcat/latest)](https://hub.docker.com/r/williamsct1/kasm-hashcat)
[![Docker Image Version](https://img.shields.io/docker/v/williamsct1/kasm-hashcat/latest)](https://hub.docker.com/r/williamsct1/kasm-hashcat/tags)

## Container Registry
The pre-built container image is available on Docker Hub:
- [williamsct1/kasm-hashcat](https://hub.docker.com/r/williamsct1/kasm-hashcat)
- Latest version: `docker pull williamsct1/kasm-hashcat:latest`

## Description
This project provides a custom KASM workspace for running Hashcat with NVIDIA CUDA support in a containerized environment. It includes additional tools like the Adj-Noun Wordlist Generator and common wordlists for password cracking and penetration testing.

## Why Use KASM for Hashcat?
### GPU-Accelerated Password Cracking
- Leverage NVIDIA CUDA support for high-performance password cracking
- Access powerful GPU resources remotely through a web browser
- Run complex password cracking tasks from any device

### Integrated Tools & Wordlists
- Pre-installed Adj-Noun Wordlist Generator
- Included rockyou.txt wordlist
- Custom wordlist generation capabilities

### Convenient Web Access
- Access your password cracking environment from any browser
- No local installation required
- Consistent environment across different machines

## Features
- Hashcat with full NVIDIA CUDA support
- Pre-installed Adj-Noun Wordlist Generator
- Included rockyou.txt wordlist at `/usr/local/wordlists/rockyou.txt`
- Custom background image
- Persistent storage for wordlists and hash files
- Web-based access through KASM

## Quick Start: Using Pre-built Image
### Prerequisites
- A running KASM Workspaces installation
- Admin access to your KASM Workspaces instance
- NVIDIA GPU support on the host system

### Installation Steps
1. Log into your KASM Workspaces admin interface
2. Navigate to Workspaces
   - Click on "Workspaces" in the left sidebar
   - Click the "Add Workspace" button
3. Configure the New Workspace Details
   - **Workspace Type**: Container
   - **Friendly Name**: Hashcat
   - **Description**: GPU-accelerated password cracking environment
   - **Docker Image**: williamsct1/kasm-hashcat:latest
   - **Docker Registry**: https://index.docker.io/v1/
   - **Persistent Profile Path**: `/mnt/kasm_profiles/{image_id}/{user_id}`
   - Click "Save"

## Using the Adj-Noun Generator
The Adj-Noun Generator is pre-installed and available as the `adj` command. It generates wordlists by combining adjectives and nouns with optional digits.

### Basic Usage
```bash
# Basic usage (outputs adjective+noun+1digit and adjective+noun+3digits)
adj

# Pipe to hashcat
adj | hashcat -m 22000 hash.hc22000

# Different digit combinations
adj -0  # No digits
adj -1  # 1 digit
adj -2  # 2 digits
adj -3  # 3 digits

# Use expanded wordlist
adj -full
```

## Hashcat Usage Examples
```bash
# WPA/WPA2 Password Cracking
hashcat -m 22000 hash.hc22000 /usr/local/wordlists/rockyou.txt

# Generate Custom Wordlist and Crack
adj -full | hashcat -m 22000 hash.hc22000
```

## Building Your Own Image
### Prerequisites
- Docker installed on your system
- Git for cloning the repository
- NVIDIA Container Toolkit

### Building Steps
1. Clone the repository:
```bash
git clone https://github.com/williamsct1/kasm-hashcat.git
cd kasm-hashcat
```

2. Build the Docker image:
```bash
docker build -t williamsct1/kasm-hashcat:latest .
```

## Troubleshooting
### Common Issues
- If CUDA is not detected:
  1. Verify NVIDIA drivers are installed on the host
  2. Ensure NVIDIA Container Toolkit is properly configured
  3. Check GPU passthrough settings in KASM

- If wordlists are not persisting:
  1. Verify persistent storage is properly configured
  2. Check permissions on the storage directory

## Notes
- The workspace uses persistent storage for wordlists and hash files
- GPU passthrough must be properly configured in KASM
- Custom wordlists can be stored in `/usr/local/wordlists/`

## License
This project is licensed under the [MIT License](LICENSE) - see the LICENSE file for details.

## Acknowledgments
- [Hashcat](https://hashcat.net/hashcat/) - Advanced Password Recovery
- [KASM Workspaces](https://www.kasmweb.com/) - Base container images
- [NVIDIA](https://developer.nvidia.com/cuda-toolkit) - CUDA Toolkit
- [wpatookit](https://github.com/wpatoolkit/Adj-Noun-Wordlist-Generator) = WPA Toolkit
