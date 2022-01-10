Role Name
=========

Uses firewalld on CentOS/Redhat 7 or Fedora 21/22 to configure the firewall

Requirements
------------

The ansible module firewalld is used for the configuration.

Role Variables
--------------

There are four hashes:
 - firewalld_zone
 - firewalld_allow_sources
 - firewalld_allow_services
 - firewalld_allow_ports

Values for firewalld_zones:

    firewalld_zones:
      zone: [zone]
      permanent: [True|False] (default: True)
      state: [present|absent] (default: present)
      interface: [interface]

interface parameter is used in the handler.

Values for firewalld_allow_sources:

    firewalld_allow_services:
      source: <service name>
      zone: [zone]			(default: public)
      permanent: [True|False]	(default: True)
      state: [enabled|disabled]	(default: enabled)

Only source is required!

Values for firewalld_allow_services:

    firewalld_allow_services:
      service: <service name>
      zone: [zone]			(default: public)
      permanent: [True|False]	(default: True)
      state: [enabled|disabled]	(default: enabled)

Only service is required!

Values for firewalld_allow_ports:

    firewalld_allow_ports:
      port: <port/protocol>
      zone: [zone]			(default: public)
      permanent: [True|False]	(default: True)
      state: [enabled|disabled]	(default: enabled)

Only port is required!

Example Playbook
----------------

    - hosts: servers
      vars:
        firewalld_allow_sources:
          - { source: 192.168.2.0/23, zone: "internal", permanent: True, state: "enabled" }
        firewalld_allow_services:
          - { service: "http" }
          - { service: "telnet", zone: "dmz", permanent: True, state: "disabled" }
        firewalld_allow_ports:
          - { port: "161/udp", zone: "internal", permanent: True, state: "enabled" }
          - { port: "162/udp", zone: "internal", permanent: True, state: "enabled" }
        firewalld_zones:
          - { zone: "internal", interface: "ens256", state: "present", permanent: true }
          - { zone: "dmz", interface: "ens224", state: "present", permanent: true }
      roles:
        - marcelnijenhof.firewalld

Disable firewalld service example
---------------------------------

    - hosts: servers
      vars:
        firewalld_allow_services:
          - { firewalld_disable: true }
      roles:
        - marcelnijenhof.firewalld

License
-------

BSD

Author Information
------------------

Marcel Nijenhof <marceln@pion.xs4all.nl>
