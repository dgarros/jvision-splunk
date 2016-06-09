# open-nti-json-output

Standalone container running fluentd, fluent-plugin-splunk-ex and the Juniper Telemetry plugin.  

This container has been based on the  OpenNTI project and has been tested with SPLUNK as the upstream collector.   
Multiple type of output are supported and can be defined at launch time:

- JSON Output (Default)
- Influxdb 
- Kafka
- Stdout

## Environment variables

So parameters can be overwritten using environment variables define at launch time.   
Here is the list of variables available with their default value.

```yaml
OUTPUT_KAFKA: false
OUTPUT_INFLUXDB: true
OUTPUT_STDOUT: false

## Ports Numbers for Juniper Telemetry Input Plugins
PORT_JTI: 50000
PORT_ANALYTICSD: 50020

## Information for Influxdb Output plugin
INFLUXDB_ADDR: localhost
INFLUXDB_PORT: 8086
INFLUXDB_DB: juniper
INFLUXDB_USER: juniper
INFLUXDB_PWD: juniper

## Information for Kafka
KAFKA_ADDR: localhost
KAFKA_PORT: 9092

## Information for JSON Output plugin. 
JSON_Host: 192.168.0.100
JSON_Port: 9997
```

Here is an example to define an environment variable. Typically the JVISION input is expected to be listening on port 50000 which is the default, however this could be changed, especially for testing using external PCAP Files. 

```
docker run -e JSON_Host='10.4.5.6' -e PORT_JTI='40000' -it  juniper/open-nti-json-output
```

## Splunk Configuration

Splunk needs to be configured to accept JSON Packets for TCP on the Port defined as the environment variable JSON_Port. To make the required change configure Settings --> Data Inputs --> (Type) TCP. 

![alt tag](https://raw.githubusercontent.com/farsonic/jvision-splunk/master/Splunk1.png)

