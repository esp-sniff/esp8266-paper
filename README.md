# ESP8266 WiFi MAC Beacon sniffer

This project realizes a MAC sniffer using WiFi Beacons.

## License & References

The code inside this repository is heavily based on existing work of many people that have done something similar on this platform.
Any modification of the imported code and the code realized by us are provided under MIT License as specified in [`LICENSE` file](./LICENSE).

As thanks and references:

  - Ray Burnette (2016):
    [ESP8266 Mini Sniff](https://www.hackster.io/rayburne/esp8266-mini-sniff-f6b93a)
    
    - Code on [hackster.io](https://halckemy.s3.amazonaws.com/uploads/attachments/209627/ESP8266_Min-Sniff.zip)
    - 2016-10-13 compiled on Linux 16.3 using Arduino 1.6.12
    - License: [![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)
  
  - José Luis Garrido (2016):
    [ESP8266 WifiSniffer](https://github.com/kalanda/esp8266-sniffer/blob/master/README.md)
    
    - Code on [GitHub](https://github.com/kalanda/esp8266-sniffer)
    - License:  [![License: Unlicense](https://img.shields.io/badge/license-Unlicense-blue.svg)](http://unlicense.org/)
  
  - Andreas Spiess (2017):
    [Wi-Fi Sniffer as Sensor for Humans](https://youtu.be/fmhjtzmLrg8)
    
    - Code on [GitHub](https://github.com/SensorsIot/Wi-Fi-Sniffer-as-a-Human-detector)
    - License: [![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)
  
  - Lars Juhl Jensen (2017):
    [WiFi sniffing with Pi Zero (W) and ESP8266 pHAT](https://forums.pimoroni.com/t/wifi-sniffing-with-pi-zero-w-and-esp8266-phat/4476)

    - Code on [GitHub](https://github.com/larsjuhljensen/phatsniffer/tree/master/esp8266)
    - License: [![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)
  
  - Question on StackOverflow:
    [ESP8266 Sniffing and sending Mac address](https://stackoverflow.com/questions/45089986/esp8266-sniffing-and-sending-mac-address)
  
  - Ángel Suárez-Bárcena Martín (2018):
    [Writing a Simple ESP8266-Based Sniffer](https://carvesystems.com/news/writing-a-simple-esp8266-based-sniffer/)

    - Code on [GitHub](https://github.com/n0w/esp8266-simple-sniffer)
    - License: Copyright 2018 Carve Systems LLC Angel Suarez-B Martin
  
  - Enrique Condes (2018):
    [ESP8266 Sniffer](https://www.hackster.io/kosme/esp8266-sniffer-9e4770)

    - Code on [hackster.io](https://halckemy.s3.amazonaws.com/uploads/attachments/611796/MACSniff.zip)
    - License: [![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)
  
  - Łukasz Podkalicki (2019):
    [ESP8266 – WiFi sniffer](https://blog.podkalicki.com/esp8266-wifi-sniffer/)

    - Code on [GitHub](https://github.com/lpodkalicki/blog/tree/master/esp8266/016_wifi_sniffer)
    - License: [![License](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)
  
Also:

  - Steven Haigh:
    [Tracking people via WiFi (even when not connected)](https://www.crc.id.au/tracking-people-via-wifi-even-when-not-connected/)
  - Dana W. Jimenez (2017):
    [MAC randomization: A massive failure that leaves iPhones, Android mobes open to tracking](https://www.airsassociation.org/airs-articles/item/19456-mac-randomization-a-massive-failure-that-leaves-iphones-android-mobes-open-to-tracking)
  - Catalin Cimpanu (2017):
    [Researchers Break MAC Address Randomization and Track 100% of Test Devices](https://www.bleepingcomputer.com/news/security/researchers-break-mac-address-randomization-and-track-100-percent-of-test-devices/)
