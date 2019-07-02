[![Build Status](https://dev.azure.com/home-assistant/Home%20Assistant/_apis/build/status/home-assistant.hassio-installer?branchName=master)](https://dev.azure.com/home-assistant/Home%20Assistant/_build/latest?definitionId=6&branchName=master)

# Install Hass.io

Beside the usage of the images it's also possible to run Hass.io on a generic system without flashing an image.

## Requirements

```
docker-ce
bash
jq
curl
avahi-daemon
dbus
```

## Optional

```
apparmor-utils
network-manager
```

## Run

Run as root (sudo su):

```bash
curl -sL https://raw.githubusercontent.com/home-assistant/hassio-installer/master/hassio_install.sh | bash -s
```

### Command line arguments
| argument           | default                                                                                                                                                                             | description                                            |
|--------------------|-------------------|--------------------------------------------------------|
| -m \| --machine    |                   | On a special platform they need set a machine type use |
| -d \| --data-share | /usr/share/hassio | data folder for hass.io installation                   |

you can set these parameters by appending ` -- <parameter> <value>` like:

```bash
curl -sL https://raw.githubusercontent.com/home-assistant/hassio-installer/master/hassio_install.sh | bash -s -- -m MY_MACHINE
```

## Supported Machine types

- intel-nuc
- odroid-c2
- odroid-xu
- orangepi-prime
- qemuarm
- qemuarm-64
- qemux86
- qemux86-64
- raspberrypi
- raspberrypi2
- raspberrypi3
- raspberrypi3-64
- tinker

## !!!WARNING!!! DO NOT DELETE CREATED CONTAINERS

This installer will create the base `homeassistant` container for you, but if you delete if (`docker rm` or `docker prune`) the supervisor will not be able to re-create it for you. Hass.io is a Eco System and Container Orchastrator they don't support manual adjustments.

If you wish to still safelly use `docker containers prune` you might want to add the `--filter` flag to your command.

Example:
```sh
$ docker container prune --filter label!=homeassistant
```
or, for a greater peace of mind, you can add the following config to your `~/.docker/config.json`:
```javascript
{
  "pruneFilters": ["label!=homeassistant", "label!=hassio_supervisor", "label!=addon*"]
}
```
