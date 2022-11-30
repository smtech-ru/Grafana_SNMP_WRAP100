# Grafana WRAP100 dashboard

## Prometheus Configuration
Example config:
```
  - job_name: "asterisk_exporter"
    scrape_interval: 10s
    static_configs:
      - targets: ["localhost:8088"]        #IP-address Asterisk Server
        labels:
          id: "Asterisk"
```

## View Metrics
You can view the resulting metrics using the following command (example): 

`curl http://172.20.10.12:9115/snmp?module=ubiquiti_airmax&target=172.20.10.40`

## Metrics
* asterisk_channels_count
* asterisk_calls_sum
* asterisk_calls_count
* asterisk_channels_state
* asterisk_channels_duration_seconds
* asterisk_endpoints_count
* asterisk_endpoints_state
* asterisk_endpoints_channels_count
* asterisk_bridges_count
* asterisk_bridges_channels_count
* asterisk_core_properties
* asterisk_core_uptime_seconds
* asterisk_core_last_reload_seconds
* asterisk_core_scrape_time_ms

## General rows
General information for WRAP100

![image alt](/images/General.png)

## States rows
States:
* Destination states (WDS)
* CURRENT PORT SUMMARY
* Destination states (users)

![image alt](/images/States.png)

## TTX rows
TTX for WRAP100:
* TX power
* signal strenght
* RSSI signal
* Noise floor

![image alt](/images/TTX.png)

## Trafic rows
Trafic information

![image alt](/images/Trafic.png)

#### The project was completed by [SN](https://github.com/StanislavVN) working after [SPbEC-Mining Ltd](https://github.com/smtech-ru).
