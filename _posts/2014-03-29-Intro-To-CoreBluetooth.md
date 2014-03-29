---
layout: post
title: Intro To CoreBluetooth
---

CoreBluetooth is Apple's framework for interacting with Bluetooth Low Energy (BLE) wireless devices. BLE is an exciting new wireless technology that has been supported for less than a year on both iOS and Android. Unlike Classic Bluetooth, it requires no pairing between devices and uses significantly less power, at the cost of throughput. This makes it ideal for applications such as:

* Discovering sensors with your iPhone
* Receiving data from sensors with an iPad while walking around a building
* Sending short text messages between multiple iPhones line-of-sight without requiring an WiFi/3G/4G

## Terminology

While CoreBluetooth is straightforward to work with, the terminology can be confusing. Instead of using Client and Server to describe the role of a BLE device, we use Central and Peripheral. Peripherals have one or more Services, and each Service can have one or more Characteristics.

For example, If you were to think of the case where our Peripheral is a Heart Rate Monitor, and our Central our iPhone, then the Heart Rate Monitor's Services and Characteristics could look as follows:

Heart Rate Monitor:

- Heart Rate Service
  - Beats per Minute Characteristic
  - Signal Strength Characteristic
- Battery Life Service
  - Battery Percentage Characteristic
  - Battery Cycles Characteristic

Our iPhone will discover these Characteristics and interrogate them for data. Apple provides us with two types of characteristics- notification-based and read/write. For the former, a Central can subscribe to notifications from the Peripheral when the Characteristic value is updated. The latter provides more asynchronous behavior for both writing to the Peripheral, and reading from it.

Note that because of the client-server model of BLE, the Peripheral cannot initiate communication with the Central unless it has a notification Characteristic for the Central to subscribe to.

## Interacting with BLE Devices

There are 3 classes that we use to interact with other BLE devices. If our iPhone is a Central, we use CBCentralManager to handle discovery of Peripherals. Once Peripherals are discovered, we can use CBPeripheral in delegate methods to discover their Characteristics and Services, and finally access data their data. If our iPhone is a Peripheral, we use CBPeripheralManager to manage all incoming client connections. Because BLE uses a client-server model, the Peripheral does not do any discovery operations of its own.

## What about iBeacons?

iBeacons are a special protocol developed by Apple. You can think of them as Peripherals that broadcast certain information about themselves, and Centrals discover but do not connect.

-----

In future posts I will walk you through the creation a simple Central and Peripheral, and show you how to avoid common mistakes!

More Info:

* [CoreBluetooth Framework Reference](https://developer.apple.com/library/ios/documentation/CoreBluetooth/Reference/CoreBluetooth_Framework/_index.html)
* [My Github, with Central and Peripheral XCode projects](https://github.com/a34729t)

{% include twitter_plug.html %}