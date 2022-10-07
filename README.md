# MING (MQTT, InfluxDB, NodeRED and Grafana)

This is an educative project called *MING* based on MQTT, InfluxDB, [balena Node-RED block](https://github.com/balenablocks/balena-node-red), Grafana and WiFi Connect balena blocks. MING is an Open-Source LAMP-like stack for the Internet of Things.

Each of these applications is built and runs in its own container on an embedded Linux target supporting balena.io or Docker:

* Mosquitto MQTT broker listening on port 1883 for MQtt message publications.
* InfluxDB listening on port 8086 providing a time series database for sensor data storage.
* NodeRed listening on port 80 to provide an easy to use graphical environment for parsing, analysing, storing, and forwarding sensor data messages.
* Grafana listening on port 8080 providing a data visualisation environment for sensor data.
* WiFi Connect listening on the port 80 in case there is not WiFi connectivity available.


## Requirements

### Hardware

* Raspberry Pi 0/2/3/4 or [balenaFin](https://www.balena.io/fin/)
* SD card in case of the RPi 3/4
* Power supply and (optionally) ethernet cable

### Software

* A balenaCloud account ([sign up here](https://dashboard.balena-cloud.com/))
* [balenaEtcher](https://balena.io/etcher)


## Deploy

You have two options here:

### One-click deploy via [Balena Deploy](https://www.balena.io/docs/learn/deploy/deploy-with-balena-button/)

You can deploy this project to a new balenaCloud application in one click using the button below:

[![](https://balena.io/deploy.svg)](https://dashboard.balena-cloud.com/deploy?repoUrl=https://github.com/mpous/ming)

Or, you can create an application in your balenaCloud dashboard and balena push this code to it the traditional way.

### In-control deploy via [balena CLI](https://www.balena.io/docs/reference/balena-cli/)

If you are a balena CLI expert, feel free to use balena CLI. This option lets you configure in detail some options, like adding new services to your deploy or configure de DNS Server to use.

- Sign up on [balena.io](https://dashboard.balena.io/signup)
- Create a new application on balenaCloud.
- Add a new device and download the image of the BalenaOS it creates.
- Burn and SD card (if using a Pi), connect it to the device and boot it up.

While the device boots (it will eventually show up in the Balena dashboard) we will prepare de services:

```
cd ~/workspace
git clone https://github.com/mpous/ming
cd ming
```

- Using [Balena CLI](https://www.balena.io/docs/reference/cli/), push the code with `balena push <application-name>`
- See the magic happening, your device is getting updated 🌟Over-The-Air🌟!


## Variables

### Device Variables

Variable Name | Default | Description
------------ | ------------- | -------------
PORT | `80` | the port that exposes the Node-RED UI
USERNAME | `balena` | the Node-RED admin username
PASSWORD | `balena` | the Node-RED admin password
ENCRIPTION_KEY | `balena` | the encription key used to store your credentials files

You **must** set the `USERNAME` and `PASSWORD` environment variables to be able to save or run programs in Node-RED.  


## Node-RED

For running Node-RED, use the local IP address on port 80, if you are on the same network than your device. You also can use the `Publick Device URL` by balena to access to the Node-RED UI.

### Add new Node-RED nodes

Add new Node-RED nodes on the Dockerfile templates on the `node-red` folder in the project. Find more an example [here](https://github.com/mpous/ming/blob/3c2e5eac92d7be3b643ca4fe6d29d0aefd533832/node-red/Dockerfile.raspberrypi4-64#L11).

### Add new services

For adding new services, use the `docker-compose` [here](https://github.com/mpous/ming/blob/master/docker-compose.yml). Go to [balenaHub](https://hub.balena.io) and use the blocks available there to accelerate your development.

### Deploy your flow into your entire fleet

If you would like to deploy your flow into your entire fleet, you can introduce a file into the folder `node-red/app/flows` [here](https://github.com/mpous/ming/tree/master/node-red/app/flows) on your cloned github repository. Then using the `balena CLI` call `balena push <your Fleet name>` and you will find the flow deployed on all your fleet.

Go to the Node-RED UI and `Import` the flow and start using it.



## Attribution

- This is based on the [balena Node-RED block](https://github.com/balenablocks/balena-node-red) made by Carlo Curinga and others. And also inspired by the [Razikus Node-RED](https://github.com/Razikus/balena-nodered) project. It is also inspired by [Alex Lennon MING project](https://github.com/DynamicDevices/ming).
- This is in joint effort between Carlo Curinga and Marc Pous to present in the [Node-RED Con 2021](https://nodered.jp/noderedcon2021/index-en.html).

## Disclaimer

This project is for educational purposes only. Do not deploy it into your premises without understanding what you are doing. 
