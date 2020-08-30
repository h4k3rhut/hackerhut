---
layout: post
title: RKS/433MHZ Jammer
date: 2019-06-12 00:00:00 +0700
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: 433after-jamming.png # Add image post (optional)
tags: [Jammer, SDR] # add tag
---

Remote keyless Systems (RKS) is a very important element of automotive security of those days.These systems permits a user to lock and unlock the automotive instead of the mechanical key by clicking a button on the key fob close to the automotive. Though different automotive brands uses different frequencies, there area unit in the main 2 totally different frequencies adopted world- wide: 315MHz for North America for 433.92

As this attack is intended to jamming the RKS communication but here we are also focusing the 433mhz frequency. So let's proceed.....

## The Jammer(Prerequisite)

A jammer is a device that transmits a stronger interfering signals called noise and prevent a radio frequency or band of radio frequency from use by the valid user.

For this project, we are using Arduino nano and a FS1000A transmitter(other 433/315MHZ transmitter modules can be used).

As the replacement of Arduino Nano below can be used.
Arduino UNO, Arduino Mega, All adruino boards, Teensy boards, Raspberry pi computers. The best one is ATtiny85 USB board, which has by default USB interface, small in size makes it handy.

### Arduino Nano

The Arduino Nano is a small, complete, and breadboard-friendly board based on the ATmega328P (Arduino Nano 3.x). It has more or less the same functionality of the Arduino Duemilanove, but in a different package. It lacks only a DC power jack, and works with a Mini-B USB cable instead of a standard one.

![Arduino nano]({{site.baseurl}}/assets/img/Arduino-nano.png)

### FS1000A Transmitter

This is FS1000A 433mHz Tx RF Radio Module. This RF module comprises of an RF Transmitter. The transmitter operates at a frequency of 433.92 and 315 MHz. An RF transmitter receives serial data and transmits it wirelessly through RF through its antenna connected at pin4.
The transmission occurs at the rate of 1Kbps – 10Kbps. This low-cost RF transmitter can be used to transmit signal up to 100 meters (the antenna design, working environment, and supply voltage will seriously impact the effective distance). The operating voltage of the transmitter is 3-5v DC.

![FS1000A Transmitter]({{site.baseurl}}/assets/img/FS1000A-Transmitter.png)

## Let's Design The Jammer

First the arduino nano installed in a small bread board and then configured the FS100A transmitter with it. The VCC pin (positive) connected to 3.3v of Arduino NANO, GND pin (negative) connected with GND of Arduino NANO and finally the DATA pin connected to the digital pin 4 of Arduino NANO.

Let's code:

```
void setup(){
}
void loop(){
  tone(4, 15000); //digital pin 4
}
```

Explaining the code: Void set is used to declare the setup which are going to be used next in the code and in Void loop the provided code iterate. The // is used for commenting. The tone() function is used to generate square wave.

* Syntax
tone(pin, frequency)

* Parameters
Pin: the pin on which to generate the tone (Here Digital Pin 4 of Arduino nano) Frequency: the frequency of the tone in hertz. (Here it is 1500)

>Here Arduino ide used to compile and upload the code to arduino nano. The jammer is now ready.
![Arduino ide]({{site.baseurl}}/assets/img/arduino-program.png)


The real view of the jammer.
![433jammer]({{site.baseurl}}/assets/img/433MHZ-jammer.png)


