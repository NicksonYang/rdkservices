<!-- Generated automatically, DO NOT EDIT! -->
<a name="head.NetworkPlugin"></a>
# NetworkPlugin

**Version: 1.0**

**Status: :black_circle::black_circle::black_circle:**

A org.rdk.Network plugin for Thunder framework.

### Table of Contents

- [Introduction](#head.Introduction)
- [Description](#head.Description)
- [Configuration](#head.Configuration)
- [Interfaces](#head.Interfaces)
- [Methods](#head.Methods)
- [Notifications](#head.Notifications)

<a name="head.Introduction"></a>
# Introduction

<a name="head.Scope"></a>
## Scope

This document describes purpose and functionality of the org.rdk.Network plugin. It includes detailed specification about its configuration, methods provided and notifications sent.

<a name="head.Case_Sensitivity"></a>
## Case Sensitivity

All identifiers of the interfaces described in this document are case-sensitive. Thus, unless stated otherwise, all keywords, entities, properties, relations and actions should be treated as such.

<a name="head.Acronyms,_Abbreviations_and_Terms"></a>
## Acronyms, Abbreviations and Terms

The table below provides and overview of acronyms used in this document and their definitions.

| Acronym | Description |
| :-------- | :-------- |
| <a name="acronym.API">API</a> | Application Programming Interface |
| <a name="acronym.HTTP">HTTP</a> | Hypertext Transfer Protocol |
| <a name="acronym.JSON">JSON</a> | JavaScript Object Notation; a data interchange format |
| <a name="acronym.JSON-RPC">JSON-RPC</a> | A remote procedure call protocol encoded in JSON |

The table below provides and overview of terms and abbreviations used in this document and their definitions.

| Term | Description |
| :-------- | :-------- |
| <a name="term.callsign">callsign</a> | The name given to an instance of a plugin. One plugin can be instantiated multiple times, but each instance the instance name, callsign, must be unique. |

<a name="head.References"></a>
## References

| Ref ID | Description |
| :-------- | :-------- |
| <a name="ref.HTTP">[HTTP](http://www.w3.org/Protocols)</a> | HTTP specification |
| <a name="ref.JSON-RPC">[JSON-RPC](https://www.jsonrpc.org/specification)</a> | JSON-RPC 2.0 specification |
| <a name="ref.JSON">[JSON](http://www.json.org/)</a> | JSON specification |
| <a name="ref.Thunder">[Thunder](https://github.com/WebPlatformForEmbedded/Thunder/blob/master/doc/WPE%20-%20API%20-%20WPEFramework.docx)</a> | Thunder API Reference |

<a name="head.Description"></a>
# Description

The `Network` plugin allows you to manage network interfaces on a set-top box.

The plugin is designed to be loaded and executed within the Thunder framework. For more information about the framework refer to [[Thunder](#ref.Thunder)].

<a name="head.Configuration"></a>
# Configuration

The table below lists configuration options of the plugin.

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| callsign | string | Plugin instance name (default: *org.rdk.Network*) |
| classname | string | Class name: *org.rdk.Network* |
| locator | string | Library name: *libWPEFrameworkNetwork.so* |
| autostart | boolean | Determines if the plugin shall be started automatically along with the framework |

<a name="head.Interfaces"></a>
# Interfaces

This plugin implements the following interfaces:

- [Network.json](https://github.com/rdkcentral/ThunderInterfaces/tree/master/interfaces/Network.json)

<a name="head.Methods"></a>
# Methods

The following methods are provided by the org.rdk.Network plugin:

Network interface methods:

| Method | Description |
| :-------- | :-------- |
| [getDefaultInterface](#method.getDefaultInterface) | Gets the default network interface |
| [getInterfaces](#method.getInterfaces) | Returns a list of interfaces supported by this device including their state |
| [getIPSettings](#method.getIPSettings) | Gets the IP setting for the given interface |
| [getNamedEndpoints](#method.getNamedEndpoints) | Returns a list of endpoint names |
| [getQuirks](#method.getQuirks) | Get standard string `RDK-20093` |
| [getStbIp](#method.getStbIp) | Gets the IP address of the default interface |
| [getSTBIPFamily](#method.getSTBIPFamily) | Gets the IP address of the default interface by address family |
| [isConnectedToInternet](#method.isConnectedToInternet) | Whether the device has internet connectivity |
| [isInterfaceEnabled](#method.isInterfaceEnabled) | Whether the specified interface is enabled |
| [ping](#method.ping) | Pings the specified endpoint with the specified number of packets |
| [pingNamedEndpoint](#method.pingNamedEndpoint) | Pings the specified named endpoint with the specified number of packets |
| [setConnectivityTestEndpoints](#method.setConnectivityTestEndpoints) | Sets the default list of endpoints used for a connectivity test |
| [setDefaultInterface](#method.setDefaultInterface) | Sets the default interface |
| [setInterfaceEnabled](#method.setInterfaceEnabled) | Enables the specified interface |
| [setIPSettings](#method.setIPSettings) | Sets the IP settings |
| [trace](#method.trace) | Traces the specified endpoint with the specified number of packets using `traceroute` |
| [traceNamedEndpoint](#method.traceNamedEndpoint) | Traces the specified named endpoint with the specified number of packets using `traceroute` |


<a name="method.getDefaultInterface"></a>
## *getDefaultInterface [<sup>method</sup>](#head.Methods)*

Gets the default network interface. The active network interface is defined as the one that can make requests to the external network. Returns one of the supported interfaces as per `getInterfaces`, or an empty value which indicates that there is no default network interface.

### Parameters

This method takes no parameters.

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.interface | string | An interface, such as `ETHERNET` or `WIFI`, depending upon availability of the given interface in `getInterfaces` |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.getDefaultInterface"
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "interface": "WIFI",
        "success": true
    }
}
```

<a name="method.getInterfaces"></a>
## *getInterfaces [<sup>method</sup>](#head.Methods)*

Returns a list of interfaces supported by this device including their state.

### Parameters

This method takes no parameters.

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result?.Interfaces | array | <sup>*(optional)*</sup> An interface |
| result?.Interfaces[#] | object | <sup>*(optional)*</sup>  |
| result?.Interfaces[#].interface | string | An interface, such as `ETHERNET` or `WIFI`, depending upon availability of the given interface in `getInterfaces` |
| result?.Interfaces[#].macAddress | string | Interface MAC address |
| result?.Interfaces[#].enabled | boolean | Whether the interface is currently enabled |
| result?.Interfaces[#].connected | boolean | Whether the interface is currently connected |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.getInterfaces"
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "Interfaces": [
            {
                "interface": "WIFI",
                "macAddress": "AA:AA:AA:AA:AA:AA",
                "enabled": true,
                "connected": true
            }
        ],
        "success": true
    }
}
```

<a name="method.getIPSettings"></a>
## *getIPSettings [<sup>method</sup>](#head.Methods)*

Gets the IP setting for the given interface.

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.interface | string | An interface, such as `ETHERNET` or `WIFI`, depending upon availability of the given interface in `getInterfaces` |
| params?.ipversion | string | <sup>*(optional)*</sup> either IPv4 or IPv6 |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.interface | string | An interface, such as `ETHERNET` or `WIFI`, depending upon availability of the given interface in `getInterfaces` |
| result.ipversion | string | either IPv4 or IPv6 |
| result.autoconfig | boolean | `true` if DHCP is used, `false` if IP is configured manually |
| result.ipaddr | string | The IP address |
| result.netmask | string | The network mask address |
| result.gateway | string | The gateway address |
| result.primarydns | string | The primary DNS address |
| result.secondarydns | string | The secondary DNS address |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.getIPSettings",
    "params": {
        "interface": "WIFI",
        "ipversion": "IPv4"
    }
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "interface": "WIFI",
        "ipversion": "IPv4",
        "autoconfig": true,
        "ipaddr": "192.168.1.101",
        "netmask": "255.255.255.0",
        "gateway": "192.168.1.1",
        "primarydns": "192.168.1.1",
        "secondarydns": "192.168.1.2",
        "success": true
    }
}
```

<a name="method.getNamedEndpoints"></a>
## *getNamedEndpoints [<sup>method</sup>](#head.Methods)*

Returns a list of endpoint names. Currently supported endpoint names are: `CMTS`.

### Parameters

This method takes no parameters.

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.endpoints | array | A list of supported endpoint names |
| result.endpoints[#] | string |  |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.getNamedEndpoints"
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "endpoints": [
            "CMTS"
        ],
        "success": true
    }
}
```

<a name="method.getQuirks"></a>
## *getQuirks [<sup>method</sup>](#head.Methods)*

Get standard string `RDK-20093`.

### Parameters

This method takes no parameters.

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.quirks | string | Update `RDK-20093` string |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.getQuirks"
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "quirks": "RDK-20093",
        "success": true
    }
}
```

<a name="method.getStbIp"></a>
## *getStbIp [<sup>method</sup>](#head.Methods)*

Gets the IP address of the default interface.

### Parameters

This method takes no parameters.

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.ip | string | The IP address |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.getStbIp"
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "ip": "192.168.1.101",
        "success": true
    }
}
```

<a name="method.getSTBIPFamily"></a>
## *getSTBIPFamily [<sup>method</sup>](#head.Methods)*

Gets the IP address of the default interface by address family.

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.family | string | The address family to query |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.ip | string | The IP address |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.getSTBIPFamily",
    "params": {
        "family": "AF_INET"
    }
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "ip": "192.168.1.101",
        "success": true
    }
}
```

<a name="method.isConnectedToInternet"></a>
## *isConnectedToInternet [<sup>method</sup>](#head.Methods)*

Whether the device has internet connectivity. This API might take up to 2s to validate internet connectivity.

### Parameters

This method takes no parameters.

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.connectedToInternet | boolean | `true` if internet connectivity is detected, otherwise `false` |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.isConnectedToInternet"
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "connectedToInternet": true,
        "success": true
    }
}
```

<a name="method.isInterfaceEnabled"></a>
## *isInterfaceEnabled [<sup>method</sup>](#head.Methods)*

Whether the specified interface is enabled.

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.interface | string | An interface, such as `ETHERNET` or `WIFI`, depending upon availability of the given interface in `getInterfaces` |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.enabled | boolean | `true` if the interface is enabled, otherwise `false` |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.isInterfaceEnabled",
    "params": {
        "interface": "WIFI"
    }
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "enabled": true,
        "success": true
    }
}
```

<a name="method.ping"></a>
## *ping [<sup>method</sup>](#head.Methods)*

Pings the specified endpoint with the specified number of packets.

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.endpoint | string | The host name or IP address |
| params.packets | integer | The number of packets to send. Default is 15 |
| params?.guid | string | <sup>*(optional)*</sup> The globally unique identifier |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.target | string | The target IP address |
| result.success | boolean | Whether the request succeeded |
| result.packetsTransmitted | integer | The number of packets sent |
| result.packetsReceived | integer | The number of packets received |
| result.packetLoss | string | The number of packets lost |
| result.tripMin | string | The minimum amount of time to receive the packets |
| result.tripAvg | string | The average time to receive the packets |
| result.tripMax | string | The maximum amount of time to receive the packets |
| result.tripStdDev | string | The standard deviation for the trip |
| result.error | string | An error message |
| result.guid | string | The globally unique identifier |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.ping",
    "params": {
        "endpoint": "45.57.221.20",
        "packets": 10,
        "guid": "..."
    }
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "target": "45.57.221.20",
        "success": true,
        "packetsTransmitted": 10,
        "packetsReceived": 10,
        "packetLoss": "0.0",
        "tripMin": "61.264",
        "tripAvg": "130.397",
        "tripMax": "230.832",
        "tripStdDev": "80.919",
        "error": "...",
        "guid": "..."
    }
}
```

<a name="method.pingNamedEndpoint"></a>
## *pingNamedEndpoint [<sup>method</sup>](#head.Methods)*

Pings the specified named endpoint with the specified number of packets. Only names returned by `getNamedEndpoints` can be used. The named endpoint is resolved to a specific host or IP address on the device side based on the `endpointName`.

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.endpointName | string | An endpoint name returned by `getNamedEndpoints` |
| params.packets | integer | The number of packets to send. Default is 15 |
| params?.guid | string | <sup>*(optional)*</sup> The globally unique identifier |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.target | string | The target IP address |
| result.success | boolean | Whether the request succeeded |
| result.packetsTransmitted | integer | The number of packets sent |
| result.packetsReceived | integer | The number of packets received |
| result.packetLoss | string | The number of packets lost |
| result.tripMin | string | The minimum amount of time to receive the packets |
| result.tripAvg | string | The average time to receive the packets |
| result.tripMax | string | The maximum amount of time to receive the packets |
| result.tripStdDev | string | The standard deviation for the trip |
| result.error | string | An error message |
| result.guid | string | The globally unique identifier |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.pingNamedEndpoint",
    "params": {
        "endpointName": "CMTS",
        "packets": 10,
        "guid": "..."
    }
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "target": "45.57.221.20",
        "success": true,
        "packetsTransmitted": 10,
        "packetsReceived": 10,
        "packetLoss": "0.0",
        "tripMin": "61.264",
        "tripAvg": "130.397",
        "tripMax": "230.832",
        "tripStdDev": "80.919",
        "error": "...",
        "guid": "..."
    }
}
```

<a name="method.setConnectivityTestEndpoints"></a>
## *setConnectivityTestEndpoints [<sup>method</sup>](#head.Methods)*

Sets the default list of endpoints used for a connectivity test. Maximum number of endpoints is 5.

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.endpoints | array | A list of endpoints to test |
| params.endpoints[#] | string |  |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.setConnectivityTestEndpoints",
    "params": {
        "endpoints": [
            "xfinity.com:8080"
        ]
    }
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "success": true
    }
}
```

<a name="method.setDefaultInterface"></a>
## *setDefaultInterface [<sup>method</sup>](#head.Methods)*

Sets the default interface. The call fails if the interface is not enabled.

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.interface | string | An interface, such as `ETHERNET` or `WIFI`, depending upon availability of the given interface in `getInterfaces` |
| params.persist | boolean | Whether the default interface setting persists after reboot. When `true`, this interface is enabled as the default interface currently AND on the next reboot. When `false`, this interface is only the default during this session |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.setDefaultInterface",
    "params": {
        "interface": "WIFI",
        "persist": true
    }
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "success": true
    }
}
```

<a name="method.setInterfaceEnabled"></a>
## *setInterfaceEnabled [<sup>method</sup>](#head.Methods)*

Enables the specified interface.

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.interface | string | An interface, such as `ETHERNET` or `WIFI`, depending upon availability of the given interface in `getInterfaces` |
| params.enabled | boolean | Enables the interface when `true`. Disables the interface when `false` |
| params.persist | boolean | Whether the interface setting persists after reboot. When `true`, this interface is enabled currently AND on the next reboot. When `false`, this interface is only enabled during this session |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.setInterfaceEnabled",
    "params": {
        "interface": "WIFI",
        "enabled": true,
        "persist": true
    }
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "success": true
    }
}
```

<a name="method.setIPSettings"></a>
## *setIPSettings [<sup>method</sup>](#head.Methods)*

Sets the IP settings.

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.interface | string | An interface, such as `ETHERNET` or `WIFI`, depending upon availability of the given interface in `getInterfaces` |
| params.ipversion | string | IPv4 (IPv6 is not currently supported) |
| params.autoconfig | boolean | `true` if DHCP is used, `false` if IP is configured manually |
| params.ipaddr | string | The IP address |
| params.netmask | string | The network mask address |
| params.gateway | string | The gateway address |
| params.primarydns | string | The primary DNS address |
| params.secondarydns | string | The secondary DNS address |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.supported | boolean | `true` if setting the IP settings are supported, otherwise `false` if not supported |
| result.success | boolean | Whether the request succeeded |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.setIPSettings",
    "params": {
        "interface": "WIFI",
        "ipversion": "IPv4",
        "autoconfig": true,
        "ipaddr": "192.168.1.101",
        "netmask": "255.255.255.0",
        "gateway": "192.168.1.1",
        "primarydns": "192.168.1.1",
        "secondarydns": "192.168.1.2"
    }
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "supported": true,
        "success": true
    }
}
```

<a name="method.trace"></a>
## *trace [<sup>method</sup>](#head.Methods)*

Traces the specified endpoint with the specified number of packets using `traceroute`.

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.endpoint | string | The host name or IP address |
| params.packets | integer | The number of packets to send. Default is 15 |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.target | string | The target IP address |
| result.success | boolean | Whether the request succeeded |
| result.error | string | An error message |
| result.results | string | The results from `traceroute` |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.trace",
    "params": {
        "endpoint": "45.57.221.20",
        "packets": 10
    }
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "target": "45.57.221.20",
        "success": true,
        "error": "...",
        "results": "<<<traceroute command results>>>"
    }
}
```

<a name="method.traceNamedEndpoint"></a>
## *traceNamedEndpoint [<sup>method</sup>](#head.Methods)*

Traces the specified named endpoint with the specified number of packets using `traceroute`.

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.endpointName | string | An endpoint name returned by `getNamedEndpoints` |
| params.packets | integer | The number of packets to send. Default is 15 |

### Result

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| result | object |  |
| result.target | string | The target IP address |
| result.success | boolean | Whether the request succeeded |
| result.error | string | An error message |
| result.results | string | The results from `traceroute` |

### Example

#### Request

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "method": "org.rdk.Network.1.traceNamedEndpoint",
    "params": {
        "endpointName": "CMTS",
        "packets": 10
    }
}
```

#### Response

```json
{
    "jsonrpc": "2.0",
    "id": 42,
    "result": {
        "target": "45.57.221.20",
        "success": true,
        "error": "...",
        "results": "<<<traceroute command results>>>"
    }
}
```

<a name="head.Notifications"></a>
# Notifications

Notifications are autonomous events, triggered by the internals of the implementation, and broadcasted via JSON-RPC to all registered observers. Refer to [[Thunder](#ref.Thunder)] for information on how to register for a notification.

The following events are provided by the org.rdk.Network plugin:

Network interface events:

| Event | Description |
| :-------- | :-------- |
| [onInterfaceStatusChanged](#event.onInterfaceStatusChanged) | Triggered when an interface becomes enabled or disabled |
| [onConnectionStatusChanged](#event.onConnectionStatusChanged) | Triggered when a connection is made or lost |
| [onIPAddressStatusChanged](#event.onIPAddressStatusChanged) | Triggered when an IP Address is assigned or lost |
| [onDefaultInterfaceChanged](#event.onDefaultInterfaceChanged) | Triggered when the default interface changes, regardless if it's from a system operation or through the `setDefaultInterface` method |


<a name="event.onInterfaceStatusChanged"></a>
## *onInterfaceStatusChanged [<sup>event</sup>](#head.Notifications)*

Triggered when an interface becomes enabled or disabled.
 
### Methods
  
| Method | Description | 
| :----------- | :----------- |
| `setInterfaceEnabled` |Triggers event onInterfaceStatusChanged only if this method call caused the interface's enabled/disabled status to change.|
| `setDefaultInterface` |1.Triggers onInterfaceStatusChanged(WIFI,TRUE) event if the WIFI interface is enabled as a result of calling setDefaultInterface(WIFI) method.  2.Triggers onInterfaceStatusChanged(WIFI,FALSE) event if the WIFI interface is disabled as a result of calling setDefaultInterface(ETHERNET) method.|
 
Also see: [setDefaultInterface](#method.setDefaultInterface), [setInterfaceEnabled](#method.setInterfaceEnabled).

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.interface | string | An interface, such as `ETHERNET` or `WIFI`, depending upon availability of the given interface in `getInterfaces` |
| params.enabled | boolean | Whether the interface is enabled (`true`) or disabled (`false`) |

### Example

```json
{
    "jsonrpc": "2.0",
    "method": "client.events.1.onInterfaceStatusChanged",
    "params": {
        "interface": "WIFI",
        "enabled": true
    }
}
```

<a name="event.onConnectionStatusChanged"></a>
## *onConnectionStatusChanged [<sup>event</sup>](#head.Notifications)*

Triggered when a connection is made or lost.
 
### Methods
  
| Method | Description | 
| :----------- | :----------- |
| `setDefaultInterface` |Triggers onConnectionStatusChanged event if the device  connects to WIFI SSID  as a result of calling setDefaultInterface(WIFI) method.|
 
Also see: [setDefaultInterface](#method.setDefaultInterface).

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.interface | string | An interface, such as `ETHERNET` or `WIFI`, depending upon availability of the given interface in `getInterfaces` |
| params.status | string | Whether the interface is currently connected or disconnected (must be one of the following: *`CONNECTED`*, *`DISCONNECTED`*) |

### Example

```json
{
    "jsonrpc": "2.0",
    "method": "client.events.1.onConnectionStatusChanged",
    "params": {
        "interface": "WIFI",
        "status": "CONNECTED"
    }
}
```

<a name="event.onIPAddressStatusChanged"></a>
## *onIPAddressStatusChanged [<sup>event</sup>](#head.Notifications)*

Triggered when an IP Address is assigned or lost.
 
### Methods
  
| Method | Description | 
| :----------- | :----------- |
| `setIPSettings` |Triggers onIPAddressStatusChanged event for each IP address that is lost or acquired following a call to this method.|
| `setDefaultInterface` |Triggers onIPAddressStatusChanged event for each IP address that is lost or acquired following a call to this method.|
 
Also see: [setDefaultInterface](#method.setDefaultInterface), [setIPSettings](#method.setIPSettings).

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.interface | string | An interface, such as `ETHERNET` or `WIFI`, depending upon availability of the given interface in `getInterfaces` |
| params.ip6Address | string | The IPv6 address for the interface |
| params.ip4address | string | The IPv4 address for the interface |
| params.status | string | Whether IP address was acquired or lost (must be one of the following: *`ACQUIRED`*, *`LOST`*) |

### Example

```json
{
    "jsonrpc": "2.0",
    "method": "client.events.1.onIPAddressStatusChanged",
    "params": {
        "interface": "WIFI",
        "ip6Address": "2001:0xx8:85a3:0000:0000:8x2x:0370:7334",
        "ip4address": "192.168.1.2",
        "status": "ACQUIRED"
    }
}
```

<a name="event.onDefaultInterfaceChanged"></a>
## *onDefaultInterfaceChanged [<sup>event</sup>](#head.Notifications)*

Triggered when the default interface changes, regardless if it's from a system operation or through the `setDefaultInterface` method.
 
### Methods
  
| Method | Description | 
| :----------- | :----------- |
| `setDefaultInterface` |Triggers onDefaultInterfaceChanged event if a call to this method causes the device's default interface to change.|
 
Also see: [setDefaultInterface](#method.setDefaultInterface).

### Parameters

| Name | Type | Description |
| :-------- | :-------- | :-------- |
| params | object |  |
| params.oldInterfaceName | string | The previous interface that was changed |
| params.newInterfaceName | string | The current interface |

### Example

```json
{
    "jsonrpc": "2.0",
    "method": "client.events.1.onDefaultInterfaceChanged",
    "params": {
        "oldInterfaceName": "ETHERNET",
        "newInterfaceName": "WIFI"
    }
}
```

