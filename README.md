# Autonomous Noise Unit ansible playbooks

[https://autonomousnoiseunit.co.uk](https://autonomousnoiseunit.co.uk)
[git](https://github.com/noiseorchestra/noise-audio-web)
[noise orchestra](https://noiseorchestra.org/)

Installs dependencies and configures services required for running your very own ANU.

**WARNING** *if you are installing on an existing RPi system, be aware that config files will be overwritten during the installation process. These include `etc/hosts`, `/boot/config.txt` and `/etc/modules`

## Prerequisites

- only tested on RPi 4
- Raspberry Pi OS or similar with default `pi` user and ssh enabled
- hifiberry or pisound soundcards
- ANU custom HAT (contact noiseorchestramcr AT gmail . com if you want one)

## Config

- create a `default.yml` file in the `vars/` folder based on the `default-template.yml` and populate with your config values
- you also need to edit or create your ansible hosts file at `/etc/ansible/hosts` adding the address of your RPi, for example:
```
[anu]
raspberrypi.local
```

## Install

setup the RPi with required user and permissions copies ssh keys from default users home directory:
`$ ansible-playbook anu-setup.yml -u root`

install dependencies and setup services for your ANU:
`$ ansible-playbook anu-install.yml`

#### optional

Install and configure vpncloud for remote ANU access:
`$ ansible-playbook anu-vpn.yml`