# ESP-IDF lwIP library with NAT 

\*Obsolete - NAPT ist now included in Espressif's esp-lwip\*

A version of the ESP-IDF lwIP library with NAT support.

The NAPT functionality can be enabled with the IP_NAPT and IP_FORWARD options in `esp-lwip/src/include/lwip/opt.h`.

Tested with version v3.3 of the ESP-IDF: https://github.com/espressif/esp-idf/tree/release/v3.3

It is based on the NAT implementation from this ESP8266 lwIP library: https://github.com/martin-ger/esp-open-lwip

**Update:** There is now a newer lwIP 2.1.2 library with NAT that can be found here: https://github.com/martin-ger/esp-lwip

## Get Started
To use it just replace the lwIP library from the lwIP component of the ESP-IDF with this one.
This can be done by following these steps:
1. Get the lwIP library with NAT

`git clone https://github.com/jonask1337/esp-lwip.git`

2. Rename or delete original lwIP library folder (*/esp-idf/component/lwip/lwip*)
3. Copy the lwIP library with NAT repository folder from step 1 to */esp-idf/component/lwip* and rename it to lwip.

Now if you build a project with the ESP-IDF it will use the lwIP library with NAT. 

In order for the NAT feature to work the option "Enable copy between Layer2 and Layer3 packets" must be enabled in the ESP-IDF project configuration.
An ESP-IDF project can be configured by calling `make menuconfig` (or `idf.py menuconfig` for CMake setups). In the configuration go to *Component config -> LWIP*.

In the code of your firmware enable NAPT for the softAP interface by calling the *ip_napt_enable* function from `lwipt_napt.h` header file.

Additionally, you may want to change the DNS server ip address that is offered by the DHCP server of the softAP. By default, the DHCP server will use the ip address of the softAP as DNS server ip address.
To set a different ip address use the *dhcps_dns_setserver* function defined in the `esp-idf/components/lwip/include/apps/dhcpserver/dhcpserver.h` header file.

Example esp-idf project where NAT is enabled and a custom DNS server ip is set: https://github.com/jonask1337/esp-idf-nat-example
