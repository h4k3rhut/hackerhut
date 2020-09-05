---
layout: post
title: Rtl-SDR GSM/IMSI Sniffer
date: 2020-09-05 00:00:00 +0700
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: IMG_5866.jpg # Add image post (optional)
tags: [rtl-sdr, SDR, GSM] # add tag
---

GSM stands for Global System for Mobile communication. A recent repot shows That 46% of Global Mobile Users Use 2G and 3G. 
GSM(2G standard) is combination of FDMA (Frequency Division Multiple Access), TDMA (Time Division Multiple Access) spectrum sharing. At first, GSM use two frequency bands of 25 MHz width : 890 to 915 MHz frequency band for up-link and 935 to 960 MHz frequency for down-link. Later on, two 75 MHz band were added. 1710 to 1785 MHz for up-link and 1805 to 1880 MHz for down-link. up-link is the link from ground station to a satellite and down-link is the link from a satellite down to one or more ground stations or receivers. GSM divides the 25 MHz band into 124 channels each having 200 KHz width and remaining 200 KHz is left unused as a guard band to avoid interference.

We will not go deep with the Architecture of GSM, because I am adding a basic reference link....

## IMSI Sniffer

IMSI stands for International Mobile Subscriber Identity is a unique number, usually fifteen digits, associated with Global System for Mobile Communications (GSM) to identifying a GSM subscriber.

The IMSI number is securely stored in SIM card and only known to the service provider to identify the subscription. While the  Mobile Station International Subscriber Directory Number (MSISDN) / Internationally identified mobile phone number the public part of the mapping.

So Let’s start...

### Requirements 
* Any SDR  ( here the Rtl-sdr being used. HackRf One, BladRf & USRP can be used)
* Any Linux OS( Here the Parrot OS being used. Kali linux, Ubuntu, Raspbian Os...... can be used)

Before starting the necessary tool(software) installation, update and upgrade the OS.

```
apt-get update
apt-get upgrade Or apt upgrade

```

Let’s start Installing the Necessary environmental software..

* Install Kalibrate : ( For finding GSM frequencies )

```
apt-get install kalibrate-rtl

OR

sudo apt install build-essential libtool automake autoconf librtlsdr-dev libfftw3-dev
git clone https://github.com/steve-m/kalibrate-rtl
cd kalibrate-rtl
./bootstrap && CXXFLAGS='-W -Wall -O3'
./configure
make
sudo make install

```

* Install Gr GSM : ( For receiving GSM transmissions )

```
sudo add-apt-repository -y ppa:ptrkrysik/gr-gsm
sudo apt update
sudo apt install gr-gsm

```


![Arduino nano]({{site.baseurl}}/assets/img/Arduino-nano.png)
