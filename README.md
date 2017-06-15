# Tentsensord

## Description

tentsensord is the service component used to interact with multiple electronic sensors and actuators.  
Communication between the host and the microcontroller (Arduino) relies on MySensors library and there's also an embedded http server that
exposes a simple REST api to read sensor data as well as toggling actuators.

## Requirements

* Arduino Nano (328p)
* MySensors 2.1.1
* Python >= 3.5
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

### Install

#### influxdb (optional)
  > curl -i -XPOST http://localhost:8086/query --data-urlencode "q=CREATE DATABASE tentsensord"
  > curl -i -XPOST http://localhost:8086/query --data-urlencode 'q=CREATE RETENTION POLICY "default" ON "tentsensord" DURATION 30d REPLICATION 1 DEFAULT'

#### service
  python setup.py install
