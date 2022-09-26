# Zabbix Template for Monitoring Meinberg Lantime-NG devices

# What are Meinberg Lantime-NG devices
[Lantime-NG](https://www.meinbergglobal.com/english/products/ntp-time-server.htm) are a family of hardware based NTP appliances for providing propper time to computer, telco and other networks.

# What is Zabbix Template for Monitoring Meinberg Lantime-NG devices
This is a template for collecting key indicators for the performance of Lantime-NG devices. It Discovers, Collects and Graphs important information about the device itself and its performance.

Additionally besides operational data some additional informational data is collected and used to autofill Inventory fields.

# How is this template Designed
The template is designed with Zabbix [SNMP Agent](https://www.Zabbix.com/documentation/current/en/manual/config/items/itemtypes/snmp) items. This choice is dictated by the fact that Meinberg provides and maintains propper MIB's for their products.

## What is monitored
Currently only key indicators are monitored

| Item | Key | Description |
| ---- | --- | ----------- |
| Current GPS receiver position | `mbgLtNgRefclockGpsPos` | Position of the device itself (as reported). Currently not used for much but can be used to populate inventory fields. NOTE: this is the location of the antena itself and depending on cable length might be quite different than the actual device location itself |
| Client tracking enabled | `mbgLtNgCfgNtpEnableClientCounter` | Indicator if client tracking is enabled. See notes for usage and reason |
| Daily NTP Clients | `mbgLtNgNtpCCTodaysClients` | Number of unique NTP clients that have contacted the device. Needs Client tracking, resets daily |
| Firmware version | `mbgLtNgFirmwareVersion` | Version of the installed firmware |
| Internal Temperature | `mbgLtNgSysTempCelsius` | Temperature of the device itself. Most are passively cooled |
| NTP Clock Stratum | `mbgLtNgNtpStratum` | Clock Stratum |
| NTP Requests Per second | `mbgLtNgNtpCCTotalRequests` | Number of requests per second (via preprocessing) |
| Number of RefClocks | `mbgLtNgNumberOfRefclocks` | Number of hardware reference clocks |
| Offset in ms from NTP | `mbgLtNgNtpRefclockOffset` | Offset from the true NTP |
| Refclock Mode | `mbgLtRefClockMode` | State of the refclock (is it synced or not) |
| Serial Number | `mbgLtNgSerialNumber` | Serial number of the device |
| State of GPS FIX | `mbgLtRefGpsStateVal` | The status of the GPS refclock |

## What items are autodiscovered
Currently there are LLD's configured for:

 * Fan (if installed) - Just the status (not available, error, ok)
 * Power supplies - Status of the power supply
 * Refclocks - Full status of the refclocks. This includes basic and extended status, type, use and others. The information differs based on refclock.

## Available Triggers
There are several triggers available to fire on different (mostly hardware related conditions). This is work in progress.

Some of the available triggers (also created via LLD):

 * Fan problems
 * Power Supply problems
 * Refclock sync status
 * Antena faults
 * Clock/Sync states

## Available Macros

| Macros | Default | Description |
| ------ | ------- | ----------- |

## How to Use

 * Install the required [MIB's](https://www.meinbergglobal.com/english/sw/#snmp-mib) as item names defined in them are used
 * Import Template into Zabbix (will go in `Templates/NTP` group)
 * Assign to a Lantime-NG device
 * Configure SNMP variables as needed
 * It is recommended to also attach `Template OS Linux SNMPv2` to get more information (like cpu/disk/etc)

# Questions / Issues / Others
Feel free to use the issues system for requests and others
