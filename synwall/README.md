Role Name
=========
This role installs the SYNwall kernel module

Role Variables
--------------
- installation:
  - git: every target will download the source from a git repo and compile it
  - source: you should provide the source code (on local machine) to the target which will compile it
  - compiled: you should provide the compiled module (on local machine) to the target

- source:
  - if installation is git it should be the url to the repository
  - if installation is source it should be the path to the folder containing the source code (path must end with /)
  - if installation is compiled it should be the path to the compiled module (should be a .ko file)

- destination: absolute path to put source code or compiled (path must end with /)

- modprobe: decide to insert the module now

- load_at_boot:
  - modules: puts the ko file in /lib/modules/'uname -r'/misc and creates a configuration file under /etc/modules-load.d
  - cron: set the module to be loaded after boot time with cron
  - any other value: it does nothing

- sleep: optionally add a sleep before running modprobe at boot via cron, by default is 0

- module params, see module documentation for usage. the only mandatory value is the psk

      params:
        \# Pre-Shared Key used for the OneTimePassword
        psk: ""
        \# Time precision parameter
        precision: 1
        \# Disable the OTP for outgoing packets
        disable_out: 0
        \# Enable DoS protection
        enable_antidos: 0
        \# Enable IP Spoofing protection
        enable_antispoof: 0
        \# Delay in starting up the module functionalities (ms)
        load_delay: 10000
        \# List of ports for port knocking failsafe
        portk:
          - 0
          - 0
          - 0
          - 0
        portk_count: 0

Example Playbook
----------------

    - name: Installing Synwall module
      hosts: synwall
      roles:
        - synwall

License
-------
GPL-3.0

Author Information
------------------
Sorint.Lab
