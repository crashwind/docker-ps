# about

scripts to show some helpful docker container info

fit output to terminal size

mac iTerm 1/2 (vertically splitted):
```
$ tput cols
118
```

# prerequisites
util `jq` is required to use these wrappers

# scripts

## docker-ps-command
show docker containers command with no truncation
```
$ docker-ps-command
NAMES               COMMAND
zabbix-server       "/sbin/tini -- /usr/bin/docker-entrypoint.sh /usr/sbin/zabbix_server --foreground -c /etc/zabbix/zabbix_server.conf"
zabbix-web          "docker-entrypoint.sh"
zabbix-db           "docker-entrypoint.sh --character-set-server=utf8 --collation-server=utf8_bin"
```

## docker-ps-image
```
$ docker-ps-image
NAMES               IMAGE                                                    STATUS
zabbix-server       my-docker-registry/infra/zabbix-server-mysql:latest      Up 18 hours
```

## docker-ps-network
```
$ docker-ps-network
Name           Config.MacAddress  Networks.IPAddress  Networks.MacAddress  Networks.Gateway
zabbix-server  00:01:02:03:04:05  192.168.123.234     00:01:02:03:04:05    192.168.123.234
```

## docker-ps-size
```
$ docker-ps-size
CONTAINER ID        NAMES               STATUS                 SIZE
aabbccddeeff        zabbix-server       Up 18 hours            22kB (virtual 98.3MB)
```

## docker-ps-cpu
```
$ docker-ps-cpu
Name           CpusetCpus  CpuCount  CpuQuota  CpuShares  CpuPercent
zabbix-server  26-27       0         0         0          0
```

## docker-show-config
show container `Config`
```
$ docker-show-config grafana
{
  "Hostname": "grafana.localdomain",
  ...
  "Env": [
  "GF_INSTALL_PLUGINS=alexanderzobnin-zabbix-app",
  ...
}
```

## docker-show-dirs
show container `GraphDriver`
```
$ docker-show-dirs grafana
{
  "Data": {
  ...
    "MergedDir": "/var/lib/docker/overlay2/d147cafcd133b8ecd69f6f2bd182969e956e373e6fd794cce536ef51496058d7/merged",
  ...
  }
}
```

## docker-show-log-config
show container `HostConfig.LogConfig` and `LogPath`
```
$ docker-show-log-config grafana
{
  "LogConfig": {
    "Type": "loki",
    "Config": {
      ...
      log-opts
    }
  }
}

{
  "LogConfig": {
    "Type": "json-file",
    ...
  }
  "LogPath": "/path/to/container-json.log"
}
```

## docker-show-network-config
show container `NetworkSettings`
```
$ docker-show-network-config grafana
{
  "Bridge": "",
  "Ports": {},
  ...
  "Networks": {
    "a_10_internal_network": {
      "IPAMConfig": {
        "IPv4Address": "192.168.123.234"
      },
      "MacAddress": "aa:bb:cc:dd:ee:ff",
    ...
    }
  }
}
```

