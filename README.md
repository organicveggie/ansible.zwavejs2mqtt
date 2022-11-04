# Ansible Role: zwave-js-gui on Docker <!-- omit in toc -->

[![github](https://github.com/organicveggie/ansible.zwavejsgui/workflows/Molecule/badge.svg)](https://github.com/organicveggie/ansible.zwavejsgui/actions)
[![Issues](https://img.shields.io/github/issues/organicveggie/ansible.zwavejsgui.svg)](https://github.com/organicveggie/ansible.zwavejsgui/issues/)
[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/organicveggie/ansible.zwavejsgui.svg)](https://github.com/organicveggie/ansible.zwavejsgui/pulls/)
[![Last commit](https://img.shields.io/github/last-commit/organicveggie/ansible.zwavejsgui?logo=github)](https://github.com/organicveggie/ansible.zwavejsgui/commits/main)

An [Ansible](https://www.ansible.com/) role to setup and run the [zzwave-js-gui](https://github.com/zwave-js/zwave-js-ui/)
[Docker](http://www.docker.com) [container](https://hub.docker.com/r/zwavejs/zwave-js-ui).

## Contents <!-- omit in toc -->

- [Requirements](#requirements)
- [Role Variables](#role-variables)
  - [zwave-js-gui settings](#zwave-js-gui-settings)
  - [Container Settings](#container-settings)
  - [Docker volumes and folders](#docker-volumes-and-folders)
  - [Docker Networks](#docker-networks)
  - [Traefik Proxy](#traefik-proxy)
- [Dependencies](#dependencies)
- [Example Playbooks](#example-playbooks)
- [License](#license)
- [Author Information](#author-information)

## Requirements

Requires Docker. Reecommended role for Docker installation:
[geerlingguy.docker](https://galaxy.ansible.com/geerlingguy/docker).

## Role Variables

See [defaults/main.yml](defaults/main.yml) for a complete list.

### zwave-js-gui settings

```yaml
# Timezone code for the container. Timezone codes can be found at:
# https://en.wikipedia.org/wiki/List_of_tz_database_time_zones.
zwavejsgui_docker_timezone: "America/New_York"

# ZWave serial device to attach to the Docker container. Note: Do not use /dev/ttyUSBX serial
# devices, as those mappings can change over time. Instead, use the /dev/serial/by-id/X serial
# device for your Z-Wave stick.
#
# Example:
#
#   $ ls -al /dev/serial/by-id/
#   lrwxrwxrwx 1 root root 13 Sep  6 18:57 usb-1234_5678-ge11 -> ../../ttyACM0
#
zwavejsgui_docker_device: "/dev/serial/by-id/usb-1234_5678-ge11"
```

### Container Settings

```yaml
# Name of the Docker container.
zwavejsgui_docker_name: "zwave-js-ui"

# Base name of the Docker image to use for the container.
zwavejsgui_docker_image_name: "zwavejs/zwave-js-ui"

# Specific Docker image version to use for the container.
zwavejsgui_docker_image_version: "latest"

# TCP port number to expose to handle HTTP traffic.
zwavejsgui_docker_web_port: "8091"

# TCP port number to expose for MQTT traffic.
zwavejsgui_docker_ws_port: "3000"

# Number of vCPUs to allocate to the container.
zwavejsgui_docker_cpus: "1"

# Amount of memory to allocate to the container.
zwavejsgui_docker_memory: "512M"
```

### Docker volumes and folders

```yaml
# Create and use Docker volumes for storing data. True creates volumes and attaches them to the
# container. False creates folders and bind mounts them to the container.
zwavejsgui_docker_use_volumes: true

# Name of the Docker volume to create to store data files. Only used when
# [zwavejsgui_docker_use_volumes] is true.
zwavejsgui_docker_volume_name: "zwavejsqui"

# Directory on filesystem to use for storing data files. Only used when
# [zwavejsgui_docker_use_volumes] is false.
zwavejsgui_docker_data_dir: "/var/lib/zwavejsqui"
```

### Docker Networks

```yaml
# Name of the default Docker network for the container. The container will *always* attach to this
# network. If [zwavejsgui_docker_network_create] is true, this is also the name of the network which
# will be created.
zwavejsgui_docker_network: "zwave-js-ui"

# List of additional networks the container should attach to. Elements should be dictionaries like
# https://docs.ansible.com/ansible/latest/collections/community/docker/docker_container_module.html#parameter-networks.
zwavejsgui_docker_extra_networks: []

# List of aliases for this container in the default network. These names can be used in the default
# network to reach this container.
zwavejsgui_docker_network_aliases: []

# The container’s IPv4 address in the default network. Defaults to using DHCP.
zwavejsgui_docker_network_ipv4: null

# The container’s IPv6 address in the default network. Defaults to using DHCP. Only applies if
# IPv6 is enabled in the default network.
zwavejsgui_docker_network_ipv6: null

# Create the default Docker network. True creates network and attaches the container to it. False
# does not create the network.
zwavejsgui_docker_network_create: false
```

### Traefik Proxy

```yaml
# Enable use of Traefik as a proxy.
zwavejsgui_docker_available_externally: "true"

# Host name to use for the Traefik endpoint. Combined with [zwavejsgui_docker_host_domain] to form
# the FQDN for the endpoint.
zwavejsgui_docker_hostname: "zwavejgui"

# Domain name to use for the Traefik endpoint. Combined with [zwavejsgui_docker_hostname] to form
# the FQDN for the endpoint. Also used by Traefik to create the necessary Let's Encrypt certificate.
zwavejsgui_docker_host_domain: "example.com"
```

## Dependencies

None.

## Example Playbooks

TODO

## License

[GNU AFFERO GPL](LICENSE)

## Author Information

[Sean Laurent](http://github/organicveggie)
