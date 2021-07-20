# Autonomous Noise Unit ansible playbooks

Installs dependencies and configures services required for running your very own ANU.

See [more information](https://autonomousnoiseunit.co.uk) about ANU, read the [code](https://github.com/noiseorchestra/noise-audio-web) or visit [Noise Orchestra](https://noiseorchestra.org/).

**WARNING** *if you are installing on an existing RPi system, be aware that config files will be overwritten during the installation process. These include `etc/hosts`, `/boot/config.txt` and `/etc/modules`*

## Prerequisites

- only tested on RPi 4
- Raspberry Pi OS or similar with default `pi` user and ssh enabled
- hifiberry or pisound soundcards
- ANU custom HAT (contact noiseorchestramcr AT gmail . com if you want one)
- build the version of JackTrip you want to use and replace the existing build (v1.3.0) in `files/jacktrip` with your own. You could use [this](https://github.com/sandreae/jacktrip-builder).

## Config

- create a `default.yml` file in the `vars/` folder based on the `default-template.yml` and populate with your config values
- you also need to edit or create your ansible hosts file at `/etc/ansible/hosts` adding the address to your RPi and the host vars `audio_hat` ("hifiberry-dacplusadc" or "pisound") and `vpn_ip` (optional). An example would be:
```
[anu-local]
raspberrypi.local audio_hat=pisound vpn_ip=10.0.0.201
```

Once `anu-setup.yml` has been run the RPi hostname will be changed to `anu` so the ansible hosts file will need to be updated to reflect this.

## Install

The default target host is `anu-local`, this can be changed at runtime by passing in `"variable_host=new-target-host"` with the `--extra-vars` flag.

setup the RPi with required user and permissions copies ssh keys from default users home directory:
`$ ansible-playbook anu-setup.yml -u pi -k`

install dependencies and setup services for your ANU (hostname will have changed here):
`$ ansible-playbook anu-install.yml -u pi`

reboot your ANU:
`$ ansible-playbook anu-reboot.yml -u pi`

target 

#### optional

Install and configure vpncloud for remote ANU access:
`$ ansible-playbook anu-vpn.yml -u pi`

#### Runtime target host

`$ ansible-playbook anu-install.yml -u pi --extra-vars "variable_host=anu-fleet"`
