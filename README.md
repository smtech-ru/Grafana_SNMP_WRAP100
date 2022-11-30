# Grafana WRAP100 dashboard

## SNR-private-OIDs
Use prometheus [```snmp_exporter```](https://github.com/prometheus/snmp_exporter) to get SNR metrics via snmp.

This dashboard represents the main metrics provided by a series of SNR devices and more metrics from the common MIB, which in my opinion seemed useful.

## Prometheus Configuration
Example config:
```
  - job_name: "airmax"
    scrape_interval: 30s
    scrape_timeout: 29s
    static_configs:
      - targets: ["172.20.10.40"]  #target
        labels:
          id: "WRAP-1"
      - targets: ["172.20.10.45"] #target
        labels:
          id: "WRAP-2"

    metrics_path: /snmp
    params:
      module: [ubiquiti_airmax]
    relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - target_label: __address__
        replacement: 127.0.0.1:9115
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
