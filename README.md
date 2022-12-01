# Grafana WRAP100 dashboard

Use prometheus [```snmp_exporter```](https://github.com/prometheus/snmp_exporter) to get metrics via snmp.

This dashboard represents the main metrics provided by a series of WRAP100 devices and more metrics from the common MIB.

## How to use
Install [```snmp_exporter```](https://github.com/prometheus/snmp_exporter) and configure it with the [```snmp.yml```](/snmp/snmp.yml). Then install and import [```dashboard```](/WRAP100.json). 

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

## Use Metrics
* ubntStaName
* ubntWlStatSsid
* ubntRadioMode
* ubntWlStatSecurity
* ifPhysAddress
* ubntRadioDistance
* ubntWlStatChanWidth
* ubntRadioFreq
* ubntStaCcq
* ubntRadioTxPower
* ubntWlStatSignal
* ubntRadioRssi
* ubntStaNoiseFloor
* ubntStaLastIp
* ifOperStatus
* ifInOctets
* ifOutOctets
* ifInErrors
* ubntWlStatRxRate
* ubntWlStatTxRate
* snmp_scrape_pdus_returned

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

## Useful endpoints
* More about snmp_exporter: https://github.com/prometheus/snmp_exporter
* MIB browser: http://oidref.com
* MIB WRAP100 browser: https://bestmonitoringtools.com/mibdb/mibdb_search.php?mib=UBNT-AirMAX-MIB

#### The project was completed by [SN](https://github.com/StanislavVN) working after [SPbEC-Mining Ltd](https://github.com/smtech-ru).
