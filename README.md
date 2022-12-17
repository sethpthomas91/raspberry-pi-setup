# raspberry-pi-setup
This repo will have various instructions for setting up a raspberry pi

## Basic Setup
1. Do not plug in your new raspberry pi. 
2. Flash a micro ssd card using the [raspberrypi imager](https://www.raspberrypi.com/software/)
3. Ensure that you select the gear icon before clicking write to setup the wifi password and local password.
4. Insert the micro ssd into your new raspberrypi.
5. Turn on the raspberrypi power.
6. SSH into the raspberry pi with your local settings.
```
ssh <designatedUsername>@raspberrypi.local
```

## Configuring a static IP Address
1. This step requires that you are ssh'd into the raspberrypi.
2. Record the raspberrypi's current IP address.
```
hostname -I
```
3. Record the router's gateway address (ROUTER_IP). It will be the first IP address given in the following command.
```
ip r | grep default
```
4. Record the current DNS_IP address.
```
cat /etc/resolv.conf
```
5. Configure the static IP settings by opening the config file.
```
nano /etc/dhcpcd.conf
```
6. Change the text at the bottom of the file to include the following:
```
interface NETWORK 
static ip_address=STATIC_IP/24
static routers=ROUTER_IP 
static domain_name_servers=DNS_IP
```

NETWORK will be either etho0 or wlan0 depending if you are using ethernet or wifi respectively.
STATIC_IP will be your choice of IP address. You can find rules about assigning your IP Address [here](https://www.lifewire.com/using-static-ip-address-on-private-computer-818404).
ROUTER_IP will be from step 33
DNS_IP will be from step 4.

7. Save your dhcpd.conf file.
8. Reboot your raspberrypi using:
```
sudo reboot
```
9. Ssh back into your raspeberry pi
```
ssh <designatedUsername>@raspberrypi.local
```
10. Ensure that the raspberrypi has changed its ip address.
```
hostname -I
```