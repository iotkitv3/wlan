## WLAN (WiFi)
***

> [⇧ **Home**](https://github.com/iotkitv4/intro)

![](https://raw.githubusercontent.com/iotkitv4/intro/main/images/ESP8266.png) 

Handelsübliches ESP8266-Modul. Im oberen Bildbereich die gedruckte WLAN-Antenne

- - -

[Wireless Local Area Network](https://de.wikipedia.org/wiki/Wireless_Local_Area_Network) (Wireless LAN bzw. W-LAN, meist WLAN; deutsch drahtloses lokales Netzwerk) bezeichnet ein lokales Funknetz, wobei meist ein Standard der IEEE-802.11-Familie gemeint ist. Für diese engere Bedeutung ist in manchen Ländern (z. B. USA, Großbritannien, Kanada, Niederlande, Spanien, Frankreich, Italien) weitläufig beziehungsweise auch synonym der Begriff Wi-Fi gebräuchlich. 

Das IoTKit K64F Board wird mittels dem [ESP8266 WLAN Modem](https://de.wikipedia.org/wiki/ESP8266) ans Internet angeschlossen. Die Verbindung erfolgt mittels Serieller Schnittstelle ([UART](https://github.com/iotkitv4/uart.git)).

Das DISCO_L475VG_IOT01A Boards wird mittels dem [Wi-Fi® module Inventek ISM43362-M3G-L44](https://www.inventeksys.com/wifi/wifi-modules/ism4336-m3g-l44-e-embedded-serial-to-wifi-module/) ans Internet angeschlossen. Die Verbindung erfolgt mittels [SPI-Bus](https://github.com/iotkitv4/spi).

Die benötigten Libraries befinden sich, im [mbed-os](https://github.com/ARMmbed/mbed-os/). 

Die Konfiguration, in WLAN SSID und Password, erfolgt in `mbed_app.conf`.

**Beispiel: mbed_app.json**

```js
    {
        "config": {
            "wifi-ssid": {
                "help": "WiFi SSID",
                "value": "\"LERNKUBE\""
            },
            "wifi-password": {
                "help": "WiFi Password",
                "value": "\"l3rnk4b3\""
            }
        },
        "target_overrides": {
            "*": {
                "platform.stdio-convert-newlines": true
            },
            "DISCO_L475VG_IOT01A": {
                "target.components_add": ["wifi_ism43362"],
                "ism43362.provide-default": true
            },
            "K64F": {
                "esp8266.provide-default" : true,
                "esp8266.rx": "PTC14",
                "esp8266.tx": "PTC15",
                "esp8266.rst": "D9"
            },
            "NUCLEO_F303RE": {
                "esp8266.provide-default" : true,
                "esp8266.rx": "D2",
                "esp8266.tx": "D10"
            }               
        }
    }
```        

## Network Time Protocol (NTP)
***

![](https://raw.githubusercontent.com/iotkitv4/intro/main/images/NTPArchitecture.png) 

NTP Hierarchie, Quelle: [Wikipedia](http://de.wikipedia.org/wiki/Network_Time_Protocol)

- - -

Das Network Time Protocol (NTP) ist ein Standard zur Synchronisierung von Uhren in Computersystemen über paketbasierte Kommunikationsnetze. NTP verwendet das verbindungslose Transportprotokoll UDP. NTP wurde speziell entwickelt, um eine zuverlässige Zeitangabe über Netzwerke mit variabler Paketlaufzeit zu ermöglichen.

Im allgemeinen Sprachgebrauch bezeichnet NTP sowohl das Protokoll als auch die Software-Referenzimplementierung.

NTP nutzt ein hierarchisches System verschiedener Strata (Plural von Stratum). Als Stratum 0 bezeichnet man das Zeitnormal, beispielsweise eine Atomuhr oder eine Funkuhr (genauer: Zeitzeichenempfänger) (GNSS, DCF77). Die unmittelbar mit ihm gekoppelten NTP-Server heißen Stratum 1. Jede weitere abhängige Einheit erhält bei der Bezeichnung eine höhere Nummer (Stratum 2, Stratum 3 …).

Das Network Time Protocol ist in der [NTP Library](https://github.com/ARMmbed/ntp-client/) abgebildet.

### Anwendungen 

*   Alle Arten von Zeit basierenden Anwendungen, wie Zeitschaltuhren etc.

### Beispiel(e)

Das Beispiel NTPV2 holt die Zeit vom Internet und setzt die interne Uhr des Boards.

<details><summary>main.cpp</summary>  

</p></details>


### Links

* [Konfiguration ESP8266](https://github.com/iotkitv4/uart#konfiguration-esp8266)
* [Gegenüberstellung HTTP, MQTT, CoAP](https://os.mbed.com/blog/entry/Using-HTTP-HTTPS-MQTT-and-CoAP-from-mbed/)
