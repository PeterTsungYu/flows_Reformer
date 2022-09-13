# NodeRed Dashboard
## Scope
This project aims to build a dashboard for IoT monitoring and controlling. 
- Display monitored data
- Remotely automatic control
- Remotely manual control 
- Wirelessly communicate via the MQTT protocol

## Dependencies
Everything is dragged, dropped, wired inside a [NodeRed platform](https://nodered.org/).
Hence, an installment of a nodered package in the running environment is required beforehand.
Other [add-on dependencies](https://github.com/PeterTsungYu/flows_Reformer/blob/f58e6b7e5ea29fcb2f91cfca4b48b40701c1f44f/package.json#L5) could be further installed via the NodeRed palette located inside your personal NodeRed platform (the one you start in your environment after the installment).
> To find where to manage palette, right click the upper right icon with three lines. From the drop-down, you may find it.

Data can be delivered to other platforms via [phao MQTT](https://pypi.org/project/paho-mqtt/). This is a wireless communication protocol between subscribers, publishers, and a server.
Data conveys either from the master as a publisher or to the master as a subscriber.
In NodeRed, there are nodes related to the MQTT. 
You will find the instructions about how to set up the MQTT nodes below.

With this IoT project folder, one could further pipe data for monitoring, controlling, and visualizing. 
Take a look at the [Pythonic IoT project](https://github.com/PeterTsungYu/dev_iot) and [visualization project](https://github.com/PeterTsungYu/dev_eda) that are created under the same scope of this project.   

| Features              | Links                   |
| -----------------     |:----------------------- |
| Pythonic IoT project  | [:link:][https://github.com/PeterTsungYu/dev_iot]    |
| Visualization project | [:link:][https://github.com/PeterTsungYu/dev_eda]    |

### Snaps
#### Overall view
![gif_0](https://i.imgur.com/UHQ0Eqj.gif)

#### Monitoring temperature conditions
<img src="https://i.imgur.com/hv6srNP.jpg" width="500" height="300">

#### Monitoring gas production
<img src="https://i.imgur.com/eSJr4U6.jpg" width="500" height="300">

## Quick Start
The below instructions are employed in the environment as...
- Linux-based or Linux system
- Raspberry Pi board (Rpi 3B+ is used in this project)
- Wifi or Intranet access

### Install MQTT Eclipse
```shell
sudo apt update
sudo apt install mosquitto mosquitto-clients

# to start the service
sudo systemctl start mosquitto

# to stop the service 
sudo systemctl stop mosquitto

# to enable the service on boot (/lib/systemd)
sudo systemctl enable mosquitto

# to disable the service on boot (/lib/systemd)
sudo systemctl disable mosquitto
```

### Install and start NodeRed  
```shell
# install 
bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)

# to restart(/start) the service
## restart, also start other dependent services
sudo systemctl restart nodered.service
sudo systemctl start nodered.service

# enable on boot
sudo systemctl enable nodered.service

# disable on boot
sudo systemctl disable nodered.service

# status 
systemctl status nodered.service
```
After starting the NodeRed as a service, you can access the editor in a browser by visiting localhost:1880.
The browser should be the one running on your machine (like RPi) or the one on your remote computer as you are accessing your machine by remote ssh or connections.
> The default port for NodeRed is 1880

### Import flows and install dependencies
1. After installing the NodeRed and opening the editor in a browser, you could download the [NodeRed flows](https://github.com/PeterTsungYu/flows_Reformer/blob/dev/flows_BW.json) and import the json file to your editor.
> To find where to import, right click the upper right icon with three lines. From the drop-down, you may find it.

2. There are some [add-on dependencies](https://github.com/PeterTsungYu/flows_Reformer/blob/f58e6b7e5ea29fcb2f91cfca4b48b40701c1f44f/package.json#L5) needed to be downloaded via the NodeRed pallete.
> To find where to manage palette, right click the upper right icon with three lines. From the drop-down, you may find it.




### Import flows

