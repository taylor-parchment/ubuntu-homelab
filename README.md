# Ubuntu Homelab Server

## Overview

This is my first attempt at setting up a homelab for self-hosting simple features and applications that I want to use across several devices in my home. The server is running on an old Microsoft Surface laptop with Ubuntu. This project serves multiple purposes for me: a low-budget introduction into homelabbing, a way to gain some IT experience, and a genuinely useful system that I use every day in my home.

## Project Goals

My biggest current use-case for my homelab is hosting media that I own across all devices. I want to be able to easily share files across any device on the network, stream movies and TV shows that I own, and access photos from a centralized storage.

Throughout the process, I hope to develop my understanding of networks, troubleshooting and documentation skills.

## Hardware

- The modem and router are both what was provided to me by my ISP, with almost nothing altered from the default configuration. I would like to look into router settings and consider an open source solution in the future. 
- The server runs on a Microsoft Surface Pro 7 with Intel i5-1035G4 (8) @ 3.700GHz and 8GB RAM. This remains plugged into power with the keyboard detached.
- A 2TB Toshiba HDD attached via USB to the Surface laptop.
- All configuration is done on my personal laptop, a Lenovo ThinkPad E14 Gen 2 Intel i7-1165G7 (8) @ 2.80GHz with 16GB RAM.
- Hosted services are also accessed by two Roku streaming sticks (via Jellyfin application) and mobile phones (through the browser).

## Software and Services

The server OS is Ubuntu 24.04.4 LTS. This being my first attempt and a bit of a learning activity, I just decided to use exactly what I had available at the moment. However, I will likely consider the advantages to switching to Ubuntu Server instead.

Currently installed services:
- [Jellyfin](https://jellyfin.org/docs/). This is a free service for managing and streaming media. It can be hosted with Docker, allowing all devices on a network with a browser or Jellyfin application to stream stored media files. It also helps with automatically managing and retrieving metadata for many types of media.
- [LUTE](https://luteorg.github.io/lute-manual/intro.html). This is a language-learning application which stands for Learning Using Texts. This provides a convenient place to manage and read texts in a foreign langauge. You can easily search and save words using a specified dictionary, translate sentences, and mark words by how "learned" they are.
- [Samba](https://www.samba.org/samba/). Open source implementation of SMB. With this, I can easily move files from my storage on the server to any device that can access the Samba share, without worrying about the filesystem.
- [Netdata](https://www.netdata.cloud/). A dashboard to get an overview of the server.

## Future Plans (in rough order of priority)

- Set up system backups - sooner rather than later!
- Look into better storage solutions. My current HDD is serving its purpose, and is certainly better than my old laptop's 500 odd GB, but I would like an easily expandable system with automatic drive backups.
- Set up [Immich](https://docs.immich.app/overview/quick-start/) for hosting our own photos.
- Look into my network settings and consider the advantages to an open source router software like Opensense. Also, I would like to see about setting up network-wide adblocking, with something like [AdGuard](https://adguard-dns.io/kb/adguard-home/getting-started/).
- Set up a secure method of accessing network services from the Internet. There several ways to go about this, but from what I've read, I'm leaning towards [TailScale](https://tailscale.com/docs/concepts/what-is-tailscale) for simplicity.

## Skills

Skills / Domains | What I Did
-----------------|-----------
Operating Systems|**Ubuntu Linux**: Installed and administered an Ubuntu-based home server, configuring storage, services, user permissions, and system startup behavior through the Linux command line. Managed persistent storage using fstab and maintained the system through package updates and configuration changes.
Remote Administration|**SSH**: Performed nearly all server administration remotely from a Windows workstation using SSH. Configured, managed, and troubleshot services without requiring direct physical access to the server.
Containerization|**Docker**: Deployed self-hosted applications using Docker Compose, including Lute and Jellyfin. Configured persistent volumes, container networking, and service management while troubleshooting Docker permissions and deployment issues.
Networking|Configured LAN services to allow Windows client to securely access resources hosted on the Ubuntu server. Managed network shares, verified connectivity between devices, and configured applications to communicate across the local network.
System Monitoring|**Netdata**: Installed and configured Netdata to monitor server resource utilization, uptime, storage, and network activity. Used the monitoring dashboard to verify system health and observe the impact of hosted services.
Storage and File Sharing|**ext4 Drive**: Configured an external hard drive as permanent Linux storage using the ext4 filesystem and automatic mounting through /etc/fstab. <br> **Samba**: Shared storage across the local network with Samba for seamless access from Windows while supporting media libraries hosted by Jellyfin.
Troubleshooting|Diagnosed and resolved issues including Docker daemon permission errors, SSH host authentication warnings, Linux file permissions, Wi-Fi connectivity during lid-close behavior, and application configuration. Verified solutions through testing and documented configuration changes to improve repeatability.
Documentation|**Github**: Documented system architecture, installation procedures, configuration decisions, and troubleshooting steps in this GitHub repository to provide reproducible setup instructions and demonstrate technical communication skills.

## Troubleshooting

Troubleshooting logs can be found in [docs/troubleshoting.md](/docs/troubleshooting.md).
