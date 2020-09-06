---
layout: post
title: Rtl-SDR GSM/IMSI Sniffer & Cell Triangulation
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

Now we need a gsm frequency on which to imsi and other informations. By using kalibrate we will get all the nearest gsm base stations frequencies.

```
kal -s GSM900

```

>kal: Scanning for GSM-900 base stations.\
        chan: 25 (940.0MHz - 492Hz)	power: 170562.29\
	chan: 29 (940.8MHz - 249Hz)	power: 32624.69\
	chan: 31 (941.2MHz - 168Hz)	power: 45288.13\
	chan: 95 (954.0MHz - 592Hz)	power: 43049.88\
	chan: 98 (954.6MHz -  26Hz)	power: 124469.19\
	chan: 107 (956.4MHz +  19Hz)	power: 34849.87\

This is the time to capture gsm traffic using gr-gsm on frequency of your any gsm base station which we get from previous(kalibrate).

```
grgsm livemon -f <your_frequency>M

Example :

grgsm livemon -f 940.0M

```

If the output comes gsm packets, means like the below screenshot(with continuous packet falling) then continue to next else change frequency and try.

![Grgsm livemon]({{site.baseurl}}/assets/img/grgzsm-livemon.png)

It's time to get the IMSI. The simplest and tricky way is to use wireshark.

![wireshark]({{site.baseurl}}/assets/img/wireshark_traffic-gsm.png)

But we will use an program to capture the IMSI and other information in a systematic manner. We will get the below information along with the IMSI from the program.

**MCC : Mobile country code.**\
**MNC : Mobile network code.**\
**CellID : Cell identifier, in decimal format.**\
**LAC : Location area code, in hexadecimal format.**

### IMSI-Catcher

Let's download the program and install it's dependancy.

```
git clone https://github.com/Oros42/IMSI-catcher.git
Or
wget https://github.com/Oros42/IMSI-catcher/archive/master.zip && unzip -q master.zip

sudo apt install python3-numpy python3-scipy python3-scapy
Or
pip3 install numpy...

```
Start the the program..Check the below Screenshot..

![ImsiCatcher]({{site.baseurl}}/assets/img/%20IMSI-%20sniff.png)

**Boom we got our stuffs**

### Cell Triangulation

Cell triangulation is a method by which the location of a radio transmitter can be determined by measuring either the radial distance, or the direction, of the received signal from two or three different cell towers for locating a mobile phone. It’s similar to GPS location tracking but less accurate. Some cases the method can mark the exact geographic position of a user. The mobile phone generally try to connect the nearest cell tower by emitting signal. The location of the  mobile device is adjudged through how strong the signal is sent to each of the cell tower.

[For more info about Cell Trangulation](https://4n6.com/cell-phone-triangulation/)

> To find out the geo location, there are lot of mathematical calculations behind the scene. So using the information, harvested from previous step the geographic location can be found without any extra job .. Visit [CellId](https://opencellid.org/#zoom=16&lat=37.77888&lon=-122.41943)



**The above is only for Educational**




