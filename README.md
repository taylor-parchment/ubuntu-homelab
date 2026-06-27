# Ubuntu Homelab Server

## Overview

This is my first attempt at setting up a homelab for self-hosting simple features and applications that I want to use across several devices in my home. The server is running on an old Microsoft Surface laptop with Ubuntu. This project serves multiple purposes for me: a low-budget introduction into homelabbing, a way to gain some IT experience, and a genuinely useful system that I use every day in my home.

## Project Goals

My biggest current use-case for my homelab is hosting media that I own across all devices. I want to be able to easily share files across any device on the network, stream movies and TV shows that I own, and access photos from a centralized storage.

Throughout the process, I hope to develop my understanding of networks, troubleshooting and documentation skills.

## Hardware

- The modem and router are both what was provided to me by my ISP, with almost nothing altered from the default configuration. I would like to look into router settings and consider an open source solution in the future.
- The server runs on a Microsoft Surface Pro 7 with Intel i5-1035G4 (8) @ 3.700GHz and 8GB RAM. This remains plugged into power with the keyboard detached.
- All configuration is done on my personal laptop, a Lenovo ThinkPad E14 Gen 2 Intel i7-1165G7 (8) @ 2.80GHz with 16GB RAM.
- Hosted services are also accessed by two Roku streaming sticks (via Jellyfin application) and mobile phones (through the browser).

## Software and Services

The server OS is Ubuntu 24.04.4 LTS. This being my first attempt and a bit of a learning activity, I just decided to use exactly what I had available at the moment. However, I will likely consider the advantages to switching to Ubuntu Server instead.

Currently installed services:
- Jellyfin for convenient media streaming across devices.
- Lute, a language-learning utility.
- Samba for file sharing.
- Netdata for a server network overview.

## Future Plans

- Figure out storage - currently, my server laptop's measly 500GB drive is holding all media, which will soon run out. I need to research the best way to set up storage for my system. I have a spare SSD, but I don't know whether it's viable to leave it mounted via USB.
- Set up system backups - sooner rather than later!
- Set up Immich for hosting our own photos.
- Look into my network settings and consider the advantages to an open source router software like Opensense.
