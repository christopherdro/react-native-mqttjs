# react-native-mqttjs

## Features

## Install

`npm i react-native-mqttjs --save`

## Basic usage

```
import { MqttClient } from 'react-native-mqttjs';

var mqtt = new MqttClient();
mqtt.connect('ws://test.mosquitto.org:8080');

mqtt.subscribe({'/topic1': 0}, () => {
  console.log('subscribe success topic1 with qos 0');
});
mqtt.subscribe([{'/topic2': 1}, {'/topic3': 2}], () => {
  console.log('subscribe success topic2 with qos 1, topic3 with qos 2');
});

mqtt.publish('/topic1', 'test', {qos: 0, retain: 0}, () => {
  console.log('publish success');
});

mqtt.addListener('message', (topic, data) => {
  console.log('data arrived, topic: ' + topic + ' - data: ' + data);
});

mqtt.addListener('connect', () => {
  console.log('mqtt connected');
});

```

## API

- Options:
  + keepalive: 120 seconds
  + reschedulePings: reschedule ping messages after sending packets (default true)
  + clientId: 'mqttjs_' + Math.random().toString(16).substr(2, 8)
  + protocolId: 'MQTT' or 'MQIsdp'
  + clean: true, set to false to receive QoS 1 and 2 messages while offline
  + reconnectPeriod: 1000 milliseconds, interval between two reconnections
  + connectTimeout: 30 * 1000 milliseconds, time to wait before a CONNACK is received
  + username: the username required by your broker, if any
  + password: the password required by your broker, if any
  + will: a message that will sent by the broker automatically when the client disconnect badly. The format is:
    - topic: the topic to publish
    - payload: the message to publish
    - qos: the QoS
    - retain: the retain flag

## License

MIT
