# Tentsensord

[![Build Status](https://travis-ci.org/joaoubaldo/tentsensord.svg?branch=master)](https://travis-ci.org/joaoubaldo/tentsensord)

## Description

tentsensord is the service component used to interact with multiple electronic sensors and actuators.  
Communication between the host and the microcontroller (Arduino) relies on MySensors library and there's also an embedded http server that
exposes a simple REST api to read sensor data as well as toggling actuators.

## Requirements

* Python >= 3.5
* Arduino Nano (328p)
* MySensors 2.1.1
* DHT lib for Arduino
* platformio

## Arduino code

Inside **extra/arduino/tentsensors/** there's the Arduino code ready to be
compiled and uploaded with platformio.

### Building and uploading
    platformio init  
    platformio run  
    platformio run -t upload

### Monitor device
    platformio device monitor -b 115200

## Service

### Run tests
    nosetests  
    pylint tentsensord  
    pep8 tentsensord

### Test locally
    python setup.py develop

### Configuration and logic code
The service reads logic code from an external python script.  
See tentsensord.conf and logic.py example. Also look at tentsensord source code for documentation about the logic api.

### Installation

#### Service
    python setup.py install

#### Influxdb db setup (optional)
    curl -i -XPOST http://localhost:8086/query --data-urlencode "q=CREATE DATABASE tentsensord"  
    curl -i -XPOST http://localhost:8086/query --data-urlencode 'q=CREATE RETENTION POLICY "default" ON "tentsensord" DURATION 30d REPLICATION 1 DEFAULT'


### HTTP interface

#### Enable / Disable automatic control
    curl -XPOST http://127.0.0.1:8080/control/enable_control -H"Content-length:0"  
    curl -XPOST http://127.0.0.1:8080/control/disable_control -H"Content-length:0"


#### Turn on / off a specific device
    curl -XPUT -d'value=1' http://127.0.0.1:8080/device/Extractor  
    curl -XPUT -d'value=0' http://127.0.0.1:8080/device/Fan


#### Get status of all devices
    curl http://127.0.0.1:8080/device/ -o -


#### Get status of a specific device
> curl http://127.0.0.1:8080/device/Fan -o -
