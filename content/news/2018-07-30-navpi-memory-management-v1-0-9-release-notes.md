---
layout: news
generated_by_cms: true
title: NavPi Memory Management & v1.0.9 Release Notes
author: zanuka
date: '2018-07-30T10:39:01+12:00'
feature_image: /images/uploads/navpi3.jpg
categories:
  - Nav News
  - NavPi
---
## NavPi Memory Management

As most veteran NavPi users know, there has been a significant issue with the memory resources being completely maxed out while running the NavCoin daemon. It’s been a frustrating issue and the core team has been focused on solving the problem by engineering both short and long term solutions.

### The problem; memory is maxed

When the NavCoin daemon starts, it loads the chainstate database — containing information on the entire blockchain — in memory. This causes the NavPi's RAM usage to peak until that operation is complete, resulting in sluggish performance and occasional crashes. Advanced users of the NavPi have made various tweaks to their systems for optimised performance, but for new users the initial setup and configuration mods are most certainly daunting tasks.

### The short term solution; add swap space

Creating dedicated swap space was the key to resolving the memory issue, and three approaches; ZRAM swap, USB swap, and SD card swap.

### What is the function of swap space?

The swap space is an area on the Raspberry Pi’s SD card (or additional USB drive) intended as a place the operating system can store data temporarily.  

### How does NavPi use swap space?

NavPi uses the swap space to increase the amount of information it can process “in memory” while syncing the blockchain and performing other essential operations.

### ZRAM swap

The initial approach to the problem was to enable ZRAM on the NavPi as a temporary fix. For many users it seemed to help, but during the core team’s testing cycles there were still resource issues on the initial load of the chain state in memory. 

* [How to enable ZRAM swap on NavPi](https://info.navcoin.org/knowledge-base/enable-zram-navpi/) (NavCoin Knowledge Base)

### SD swap

As another temporary solution, we created an article on the Knowledge Base demonstrating how to enable the swap space on the SD card of the NavPi. The steps in the article were based on an article written by Justin Ellingwood of Digital Ocean and tested successfully on NavPi v1.0.8. While this approach did result in added stability for both the NavCoin daemon and the Chromium WebUI, it is not our recommended approach long-term.

* [How to enable SD swap space on NavPi](https://info.navcoin.org/knowledge-base/navpi-sd-swap/) (NavCoin Knowledge Base)

### USB swap

For best results, it’s recommended to utilize a USB drive as your swap space, due to the fact that repeated reads/writes to the SD card can potentially wear it out. There are multiple articles, posts and resources from the linux and Raspbian community demonstrating how to setup a swap space on a USB. We tested many approaches and created our own version intended for the NavPi, which is now documented Knowledge Base.

* [How to enable USB swap space on NavPi](https://info.navcoin.org/knowledge-base/navpi-usb-swap/) (NavCoin Knowledge Base)

### Long-term solutions

There are plans to enhance the NavPi to remedy the memory issue long term, including: 

* optimise NavCoin core (levelDB)
* optimise NavPi OS (system configs)
* optimise NavPi application (headless)
* upgrade to new Rasbpian OS (Stretch) for new Pi 3b +

### NavPi v1.0.9 "Default"

This new version includes the following:

* updated to run NavCoin v4.2.1 by default
* fully-synced blockchain
* ZRAM swap space enabled and prioritised
* default swap space increased to 500MB

### NavPi v1.0.9 "Optimised"

We have created an optimised version of the NavPi v1.0.9 image, which has had most of the non-essential Raspbian applications removed. This pruned version contains the same updates noted above but without the additional data consumed by the default Raspbian (jessie) applications. Everything should function exactly the same, and users can still add back applications as needed.

### Available Downloads

The new images are available for download:

* [NavPi v1.0.9 "Default"](https://nav.nyc3.digitaloceanspaces.com/navpi/navpi_1.0.9.img) - 11.1 GB
* [NavPi v1.0.9 "Optimised"](https://nav.nyc3.digitaloceanspaces.com/navpi/navpi_1.0.9_lite.img) - 6 GB

### Installation notes

After downloading v1.0.9, you'll need to use a program like [Etcher](https://etcher.io/) to flash the new image onto your SD card. After booting up the NavPi with the updated card installed, the NavCoin daemon should start automatically. If you have a keyboard and mouse connected, you should be able to now use the Chromium WebUI to view your wallet. The memory usage will initially spike as the chainstate database is loaded, but it should stabilise within about 10 minutes. 

For the best long-term performance, we recommend following the [guide to setup a USB swap drive](https://info.navcoin.org/knowledge-base/navpi-usb-swap/) instead of relying primarily on the preconfigured ZRAM and default SD swap space.