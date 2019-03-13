# ESP-IDF lwIP library with NAT 

A version of the ESP-IDF lwIP library with NAT support.
To use it just replace the lwIP library from the lwIP component of the ESP-IDF with this one.

The NAPT functionality can be enabled with the IP_NAPT and IP_FORWARD options in "esp-lwip/src/include/lwip/opt.h".

In order for the NAT feature to work the option "Enable copy between Layer2 and Layer3 packets" must be enabled in the ESP-IDF project configuration.
An ESP-IDF project can be configured by calling `make menuconfig`. In the configuration go to *Component config -> LWIP*.

In the code of your firmware enable NAPT for the softAP interface by calling the *ip_napt_enable* function from "lwipt_napt.h" header file.
Additionally, you may want to change the DNS server ip address that is offered by the DHCP server of the softAP. By default, the DHCP server will use the ip address of the softAP as DNS server ip address.
To set a different ip address use the *dhcps_dns_setserver* function defined in the "esp-idf/components/lwip/include/apps/dhcpserver/dhcpserver.h" header file.

Tested with version v3.3 of the ESP-IDF: https://github.com/espressif/esp-idf/tree/release/v3.3

It is based on the NAT implementation from this ESP8266 lwIP library: https://github.com/martin-ger/esp-open-lwip
