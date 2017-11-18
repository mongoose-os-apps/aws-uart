# Mongoose OS & AWS IoT - UART and Thing Shadow example (Javascript)

## Overview
This app does two things.
- Reading UART 0 of ESP8266 and sending it to AWS IoT
- Sending device metadata and two pins state to AWS IoT

## How to install this app

## Step 1: Import

##### Via MOS UI tool
- Install and start [mos tool](https://mongoose-os.com/software.html)
- Switch to the Project page, find and import this app(if available otherwise follow the steps below), build and flash it:

<p align="center">
  <img src="https://mongoose-os.com/images/app1.gif" width="75%">
</p>

##### Flash the app through command line

- Clone this repo ```git clone https://github.com/mongoose-os-apps/aws-uart```
- Go into the directory `aws-uart` and run `mos build --arch esp8266` ( Change the arch respectively )
- After that, you should see a **build** directory in the current directory which will have the `fw.zip` binary
- Run ```mos flash``` which flashes the current build
- Run ```mos console``` and check

## Step 2: Set up Wi-Fi

- You can do this via mos tool UI or use command `mos wifi WIFI_NAME WIFI_PASSWORD`

Note that `mos` talks to the device using RPC mechanism.
RPC can talk over serial (uart), http, mqtt. By default, `mos` talks via uart.
but aws-uart example takes over uart, therefore mos RPC does not work.
You need to use another RPC channel - for example websocket. Therefore,
update `mos.yml`, put your wifi credentials there, then build/flash,
see what IP address is assigned to your board, and start mos as
`mos --port ws://IP_ADDRESS/rpc`.

## Step 3: Set up and Provision AWS IoT thing, Policy

- You can do this via mos tool UI or use command `mos aws-iot-setup --aws-iot-policy mos-default`
- Create a thing in AWS IoT and you are done
- Test this by going into AWS IoT MQTT test Console by subscribing to `mos/#` with QoS 1

### Video
[![Mongoose OS + AWS IoT](https://s3.amazonaws.com/mongoose-os/video-shot.png)](https://www.youtube.com/watch?v=2zZWANSQKqg "Mongoose OS + AWS IoT")
