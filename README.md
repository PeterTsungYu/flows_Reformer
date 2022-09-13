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

### Edit nodes
There are plenty of nodes inside the flows you just imported.
Some of them could be easily customized to meet your personal application interest.
The below instructions are starting points for your own project.

#### MQTT nodes
##### Subscription nodes, also known as mqtt_in nodes
Observed from the below image, this project uses the mqtt server and nodered serve both in a local host. (A RPi 3B+ hosts in this project.) 
The default port for the mqtt server is at 1883.
- Actions: Subscribe to a single topic, which is the "ADAM_*" down below.
> The subscription topic here should be a published variable, which is the opposite role in the MQTT protocol, in the other platform. 
[Pythonic IoT project](https://github.com/PeterTsungYu/dev_iot) is an example. Check the [rehttps://github.com/PeterTsungYu/dev_iot#define-your-topics-to-be-published--subscribedadme](https://github.com/PeterTsungYu/dev_iot#define-your-topics-to-be-published--subscribed) for more information on how to define subscription and publication topics inside a config.py file.
Carefully define on both sides; otherwise, the MQTT will not work as you would expect. 
<img src="https://i.imgur.com/ahZN0i4.png" width="250" height="300">

##### A subscription node in one of the flows
The below image is an example of showing how to read data from another platform via the MQTT protocol.
1. The flow stats from using a MQTT_in node to subscribe the topic called "ADAM_*".
2. It then communicates data, which have been processed by another program, from an 8-channel data collecter to here.  
3. The 8-channel data will be displayed in some charts on the dashboard.
4. Data are packed in a variable called "NodeRed.*" with a prefix called flow. The prefix allow you to access this flow_variable in some other flow wihin this project. See [more introduction](https://nodered.org/docs/user-guide/context#:~:text=in%20your%20browser.-,What%20is%20context%3F,This%20is%20called%20%27context%27.) on managing with different contexts in the official document.
5. The flow_variable is further connected to a mqtt_out node to be piped to a database.
<img src="https://i.imgur.com/RAtgTHf.png" width="750" height="200">

##### Publication nodes, also known as mqtt_out nodes
- Actions: Publish a single topic, which is the "NodeRed" down below, to the MQTT server
> The publication topic here should be a subscribed variable, which is the opposite role in the MQTT protocol, in the other platform. 
<img src="https://i.imgur.com/lXpLejH.png" width="250" height="300">

##### A publication node in one of the flows
The below image is an example of showing how to transfer data to another platform/program via the MQTT protocol.
1. The injection node continuously inserts a flow_variable (a variable accessed from another flow.) every 1 sec.
2. The end of this flow is the mqtt_out node, which is publishing a topic to the MQTT server.
3. In this project, it is the NodeRed topic carrying all the data processed by the flows that will be further piped to a remote database.   
<img src="https://i.imgur.com/HYQ0SP4.png" width="550" height="300">
