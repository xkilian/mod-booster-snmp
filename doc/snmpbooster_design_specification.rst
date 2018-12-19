.. _snmpbooster_design_specification:

====================
Design specification
====================

What is it
==========

The SnmpBooster module allows Shinken Pollers to directly manage SNMP data acquisition. This is an all Python cross-platform SNMP module. It is tightly integrated with the Shinken Poller, Scheduler and Arbiter daemons to provide the best possible user experience.

Design specification summary
============================

- STATUS - DESIGN SPEC PERFORMANCE

  * [Done] Functions as an integrated Shinken Poller module
  * [Done] Necessary integration code commited to Shinken official release (Integrated starting at v1.2)
  * [Done] Ability to collect thousands of SNMP metrics per second
  * [Done] Be compatible with distributed data acquisition
  * [Done] Collect data for a host/check_interval tuple via SNMP in a single pass
  * [Done] Use all builtin Shinken scheduler logic for retries, forced checks, timeouts, dependencies, parents
  * [Done] Store collected data for the duration of the check_interval in a Redis
  * [Done] On a restart, after the first collection, be able to pick up where the last check left and calculate derived values
  * [Done] Forced check are not allowed within 30 seconds of last SNMP query to the same host/check_interval, all other requests get data from the cache.
  * [Done] Only a single request to the host/check_interval via SNMP is allowed at a time, all other requests get data from the cache.

- STATUS - DESIGN SPEC USABILITY

  * [Done] Usage documentation
  * [xxxx] Provide sample configuration packs in Shinken
  * [Done] Provide sample config.ini with examples of all types of data

    * SNMP OIDS, DATASOURCES, DSTEMPLATES, TRIGGERS and TRIGGERGROUPS

  * [Done] Directly compatible for use with [[https://github.com/xkilian/genDevConfig|genDevConfig]] Shinken SNMP configuration generator
  * [Done] Provide meaningful feedback for users on errors
  * [Done] Capture all tracebacks and convert them to actual error or warning messages

- STATUS - DESIGN SPEC FEATURES

  * [Done] Return state and performance metrics
  * [Done] Performance metrics can be returned in a Weathermap compatible format
  * [Done] Configuration file format is ConfigObj INI
  * [Done] Load all valid INI configuration files from a directory and merge them
  * [Done] Load a single INI configuration file
  * [xxxx] Load a list of INI configuration files
  * [Done] Configuration file describes all generic acquisition parameters (OID, DATASOURCE, DSTEMPLATE, MAP, TRIGGER, TRIGGERGROUP)
  * [Done] Supports Triggers which are calculation rules to determine states
  * [Done] Triggers support an RPN (Reverse Polish Notation) calculation engine which includes mathematical and logical operators
  * [Done] Each TRIGGER is associated with a severity level, WARNING or CRITICAL
  * [Done] Multiple TRIGGERS can be associated with a TRIGGERGROUP
  * [Done] Use builtin Python Operators
  * [Done] Support DERIVE, TEXT, GAUGE and COUNTER data types
  * [xxxx] Support TIMETICKS data type
  * [Done] Support applying RPN based calculations to received metric for scaling or conversion purposes
  * [Done] Use a Python SNMP library which supports asynchronous acquisition PySNMP
  * [Done] Datasources can use rule based runtime instance mapping 
  * [Done] Set Snmp version as a check runtime option
  * [Done] Set Snmp DSTEMPLATE as a check runtime option
  * [Done] Set Snmp TRIGGERGROUP as a check runtime option
  * [Done] Set Snmp COMMUNITY as a check runtime option
  * [Done] Set SNmp DS Max as a check runtime option
  * [Done] Use Snmp version 2c GetBulk
  * [Done] Support Snmp version 2c GetNext if GetBulk is not supported
  * [Done] Support Snmp version 1 GetNext
  * [xxxx] Set Snmp Timeout as a check runtime option, instead of a hardcoded value at 5 seconds
  * [InProgress] Output contains which trigger is OK, WARNING or CRITICAL and more nicely formatted.

- STATUS - DESIGN SPEC MAINTAINABILITY

  * [xxxx] Functions documented in the source code
  * [Done] Critical functions documented in the source code
  * [Done] Locking sections identified in the code
  * [xxxx] Unit tests with at least 80% coverage
  * [xxxx] Unit tests integrated with Shinken test suite
  * [Done] Code hosted on github
  * [Done] configuration validity and integrity checking of all INI files
  * [xxxx] Pep8 compliant
  * [xxxx] Pylint pass


genDevConfig Plugins - Compatibility status with SnmpBooster
============================================================

- STATUS - genDevConfig maintained Plugins

  * [Done] Avaya ES switches
  * [Done] Avaya ERS routing switches
  * [Done] Accedian performance probes
  * [Done] Alcatel OS64xx
  * [Done] Alcatel OS68xx, OS69xx
  * [Done] Alcatel OXE
  * [Done] Cisco 29x0, 37K, 45K, 65K switches
  * [Done] Cisco PIX/ASA
  * [Done] Cisco IOS, IOS-XE routers
  * [Done] Geist RS-Mini and RS environmental sensors
  * [Done] IBM IMM and IMM2 modules
  * [Done] IP Forward
  * [Done] PaloAlto
  * [Done] JUNOS devices ** Validation required**
  * [Done] MIB-II Interfaces
  * [Done] Spectracom SecureSync NTP server
  * [Done] TrippLite NET and NET2 modules
  * [Done] APC PDU bars
  * [Done] NetSNMP unix hosts ** Validation required**
  * [Done] Packeteer devices ** Validation required**
  * [Done] Foundry devices ** Validation required**
  * [Done] Packeteer devices ** Validation required**
  * [Done] Cisco CSS ** Validation required**

- STATUS - 

.. tip::

   * [xxxx] Denotes a specification that is planned but not implemented
   * [InProgress] Denotes a specification that is under development
   * [Done] Denotes a specification that is implemented
