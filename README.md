Role Name
=========

Uses firewalld on CentOS/Redhat 7 or Fedora 21/22 to configure the firewall, featuring support for configuring zones

Requirements
------------

The ansible module firewalld is used for the configuration.

Role Variables
--------------

There are three sets of variables:
 - firewalld_zones
 - firewalld_allow_services
 - firewalld_allow_ports


Values for firewalld_zones:

    firewalld_zones:
      zone: [zone]
      source: <source IP/network>
      interface: [interface]
      permanent: [True|False] (default: True)
      state: [enabled|disabled] (default: enabled)
      immediate: [True|False] (default: True)


Values for firewalld_allow_services:

    firewalld_allow_services:
      service: <service name>
      zone: [zone]			(default: public)
      permanent: [True|False]	(default: True)
      state: [enabled|disabled]	(default: enabled)
      immediate: [True|False] (default: True)

Only service is required!

Values for firewalld_allow_ports:

    firewalld_allow_ports:
      port: <port/protocol>
      zone: [zone]			(default: public)
      permanent: [True|False]	(default: True)
      state: [enabled|disabled]	(default: enabled)
      immediate: [True|False] (default: True)


Example Playbook
----------------

    - hosts: servers
      vars:
        firewalld_zones:
            - { zone: "trusted", source: "192.168.1.1/24", interface: "eth0", state: "enabled", permanent: true, immediate: true }
        firewalld_allow_services:
          - { service: "http" }
          - { service: "telnet", zone: "dmz", permanent: True, state: "disabled" }
      roles:
        - mvarian.firewalld

Disable firewalld service example
---------------------------------

    - hosts: servers
      vars:
        firewalld_allow_services:
          - { firewalld_disable: true }
      roles:
        - mvarian.firewalld



License
-------

BSD

Author Information
------------------

Michael Varian (mike@northskytech.com).  Forked from original role written by Marcel Nijenhof (marceln@pion.xs4all.nl).
