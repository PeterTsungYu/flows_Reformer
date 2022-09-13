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
![gif](https://i.imgur.com/UHQ0Eqj.gif)
