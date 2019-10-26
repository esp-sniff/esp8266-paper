# Ray Brunette Sniffing v6

Requires ESP8266 Arduino SDK v1.3 (commit 1c5751460b7988041fdc80e0f28a31464cdf97a3).

Built with Arduino 1.6.12 on Linux Mint 17.3.

## Story

> I am constantly amazed at what the inexpensive ESP8266 can perform using only some creative software. In this article, I provide the Arduino sketch code to morph the WiFi device into a promiscuous WiFi scanner that will display both client and AP MAC addresses, broadcasts, signal strength and channel. It is a great project that listens silently to the WiFi 2.4G band looking for activity and then displaying it over the serial port. Since the signal strength is shown, you can even use this project to move your Access Point (WiFi router) around to find the best placement location in your home.
> 
> I have been working with the ESP8266 for over a year now; one project, the Tardis Time, has been running continuously since September 2015. Lately however, I have been using the NodeMCU (I am using the LoLin flavor from AliExpress) and I simply love the larger-sized breakout board but there is no reason you cannot use other sized and vendor breakouts: This project should run on any ESP8266 with 1M of flash storage.
> 
> As this is an all-software project, you should have it up and running in minutes. Just download the ZIP and put all of the files into your sketch folder. Please note that this is a multi-tab Arduino project, so there are more than one "program" file. Part of the difficulty in the software architecture of this project was to flatten the rather complex mess of code so that it "made sense" and allowed an interested programmer to follow what was going on. The use of function callback in the promiscuous functionality can easily obscure what is happening. By separating the code into "straight Arduino setup() and loop() and then putting all of the data structures into their own tab and putting all of the API functions into their own tabs, I hope that I have accomplished some simplification in what is going on in the sketch. However, I still consider this a complex project.
> 
> The critical set-up is in the line `wifi_set_promiscuous_rx_cb(promisc_cb)` and the real work-horse of this sketch is essentially managed in the function `promisc_cb()`.
> 
> This line `#include "./functions.h"` in the main sketch tells the Arduino IDE to includes all of the code in the tab `"functions.h"` and within the `function.h` code is `#include "./structures.h"` and therefore all three tabs are linked.

## Code details

### Beacon Template

```cpp
uint8_t template_beacon[128] = {
        0x80, 0x00, 0x00, 0x00,
/*4*/   0xff, 0xff, 0xff, 0xff, 0xff, 0xff,
/*10*/  0x01, 0x02, 0x03, 0x04, 0x05, 0x06,
/*16*/  0x01, 0x02, 0x03, 0x04, 0x05, 0x06,
/*22*/  0xc0, 0x6c,
/*24*/  0x83, 0x51, 0xf7, 0x8f, 0x0f, 0x00, 0x00, 0x00,
/*32*/  0x64, 0x00,
/*34*/  0x01, 0x04,
/* SSID */
/*36*/  0x00, 0x06, 0x72, 0x72, 0x72, 0x72, 0x72, 0x72,
        0x01, 0x08, 0x82, 0x84,
        0x8b, 0x96, 0x24, 0x30, 0x48, 0x6c, 0x03, 0x01,
/*56*/  0x04
};
```

### List hidden AP

Reference: http://www.esp8266.com/viewtopic.php?f=32&t=7025

In the ESP8266WiFi.h, there is the function getNetworkInfo() which I presume allows you to get info for hidden AP:

```cpp
/**
 * Loads all infos from a scanned wifi in to the ptr parameters
 *  @param networkItem uint8_t
 *  @param ssid  const char*
 *  @param encryptionType uint8_t
 *  @param RSSI int32_t
 *  @param BSSID uint8_t *
 *  @param channel int32_t
 *  @param isHidden bool
 *  @return (true if ok)
 */
bool getNetworkInfo(uint8_t networkItem, String &ssid, uint8_t &encryptionType, int32_t &RSSI, uint8_t* &BSSID, int32_t &channel, bool &isHidden);
```
### Serial Console Sample Output

```
ESP8266 mini-sniff by Ray Burnette http://www.hackster.io/rayburne/projects
  Type:   /-------MAC------/-----WiFi Access Point SSID-----/  /----MAC---/  Chnl  RSSI
  BEACON: <=============== [                      TardisTime]  1afe34a08bc9    8    -76
  BEACON: <=============== [                     xfinitywifi]  56571a0730c0   11    -90
  BEACON: <=============== [                                ]  52571a0730c0   11    -91
  BEACON: <=============== [                      ATTGH6Gs22]  1005b1d6ff90   11    -95
  BEACON: <=============== [                      ATT4P3G9f8]  1c1448777420   11    -92
  BEACON: <=============== [                       HOME-30C2]  5c571a0730c0   11    -91
  BEACON: <=============== [                      ATT8Q4z656]  b077acc4dfd0   11    -92
  BEACON: <=============== [                       HOME-B1C2]  94877c55b1c0   11    -94
  BEACON: <=============== [                        HUXU2012]  0c54a5d6e480    6    -94
  BEACON: <=============== [                     xfinitywifi]  0c54a5d6e482    6    -97
  BEACON: <=============== [                                ]  0c54a5d6e481    6    -96
  DEVICE: 18fe34fdc2b8 ==> [                      TardisTime]  1afe34a08bc9    8    -79
  DEVICE: 18fe34f977a0 ==> [                      TardisTime]  1afe34a08bc9    8    -94
  DEVICE: 6002b4484f2d ==> [                      ATTGH6Gs22]  0180c2000000   11    -98
  BEACON: <=============== [                   HOME-01FC-2.4]  84002da251d8    6   -100
  DEVICE: 503955d34834 ==> [                      ATT8Q4z656]  01005e7ffffa   11    -87
  BEACON: <=============== [                                ]  84002da251d9    6    -98
  BEACON: <=============== [                     xfinitywifi]  84002da251da    6    -95
  BEACON: <=============== [                                ]  fa8fca34e26c   11    -94
  DEVICE: cc0dec048363 ==> [                      ATT8Q4z656]  01005e7ffffa   11    -88
  BEACON: <=============== [                                ]  fa8fca95bad3   11    -92
  BEACON: <=============== [                       HOME-5475]  58238c3b5475    1    -96
  BEACON: <=============== [                     xfinitywifi]  5a238c3b5477    1    -94
  BEACON: <=============== [                                ]  5a238c3b5476    1    -96
  DEVICE: 1859330bf08e ==> [                      ATT8Q4z656]  01005e7ffffa   11    -92
  BEACON: <=============== [                                ]  92877c55b1c0   11    -92
  DEVICE: f45fd47bd5e0 ==> [                      ATTGH6Gs22]  ffffffffffff   11    -93
  BEACON: <=============== [                           Lynch]  744401480a27   11    -96
  BEACON: <=============== [                     xfinitywifi]  96877c55b1c0   11    -93
  DEVICE: f43e9d006c10 ==> [                     xfinitywifi]  8485066ff726    6    -96
  DEVICE: 285aeb4f16bf ==> [                      ATTGH6Gs22]  3333ffb3c678   11    -94
  DEVICE: 006b9e7fab90 ==> [                      ATTGH6Gs22]  01005e7ffffa   11    -91
  DEVICE: 78456155b9f0 ==> [                           Lynch]  01005e7ffffa   11    -95
  DEVICE: 6cadf84a419d ==> [                       HOME-30C2]  88cb8787697a   11    -89
  BEACON: <=============== [           Verizon-SM-G935V-6526]  a608ea306526   11    -92
```

> A little explanation to assist in understanding the printout:
> 
> An Access Point, AP, will occasionally "beacon" so that WiFi devices and other APs will know of its existence. It does this for the center frequency on which the AP is configured. The RSSI is a signal indicator of the received power: generally speaking, the higher the numeric number the weaker the signal (due to the minus sign.) A MAC address of all `"ffffffffffff"` is called a **broadcast** which has special network significance.
> 
> On the client (device) side, a MAC will be printed followed by `"==>"` to indicate communication (typically) with an AP. Again, the MAC of the receiving device is shown as well as the channel and the signal level.

## References
  - based on [RandDruid/esp8266-deauth](https://github.com/RandDruid/esp8266-deauth) (MIT)
  - inspired by [kripthor/WiFiBeaconJam](https://github.com/kripthor/WiFiBeaconJam) (no license)
  - also see [JimmieJammer](https://git.schneefux.xyz/schneefux/jimmiejammer/src/master/jimmiejammer.ino)