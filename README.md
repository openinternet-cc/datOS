# About

DatOS is built for people who would like to use their mobile phone as a general purpose internet router. 

For many people, stable wired internet options are limited or unavailable - therefore cellular based internet options may be the only option. Unfortunately, there are some systemic barriers which generally cause problems for these types of users. The basic problems will be discussed below and also described how DatOS addresses these issues.

> DatOS was forked from LineageOS, an open source android derivative. 

# Prevent Hotspot Limitations

The main issue DatOS addresses are the arbitrary usage-based restrictions that cellular carriers put on their "unlimited data plans". 

Generally, carriers will detect, and limit/throttle hotspot, also known as "tethering", data usage; this essentially means your ability to share mobile data with other devices like your TV or computer. 

DatOS addresses this issue in 2 main ways:

- remove DUN/APN provisioning

- force TTL 64 for outgoing HTTP packets (no need to configure on each individual device)

In Progress:

- auto detect and reconnect when mobile data disconnected or throttled 

# Ease of Use

DatOS also seeks to make the phone to repurpose as a router, as such we make some basic changes for better user experience.

- default to 5GHZ wifi band

- default to use VPN for upstream (tethered) devices

- removes additional bloatware

- ships with F-droid, open source app store, for easy flexibility and customization options

In Progress:

- start/restart wifi tether on boot

# Devices

Currently, DatOS is supported on:

- LeEco Le S2 (available for purchase [here](https://openinternet.cc/#shop))

> NOTE: If you would like to help expand DatOS support to new devices, please reach out to me personally at glenn@openinternet.cc

# MIT License

Copyright 2021 Open Internet, Inc.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

# Notice

By installing and using DatOS, you are responsible for your Terms of Service with your mobile data carrier. We are not responsible if the carrier cancels or terminates your contract. 

