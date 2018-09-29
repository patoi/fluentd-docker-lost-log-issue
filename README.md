# Some log records are missing after restarting fluentd

```
docker -v
Docker version 18.06.1-ce, build e68fc7a

docker-compose -v
docker-compose version 1.22.0, build f46880f

MacOS 10.14.0 (Mojave)
```

# Reproducing

- Clone this repo
- Check your docker and docker-compose versions
- Open "A" terminal, start app: ```docker-compose up -d --build```
- Open "B" terminal, watch log: ```docker-compose logs -f```
- Stop fluent on "A": ```docker stop fluentd```
- Check your logs on "B": fluent gracefully stoped
- Wait 6 seconds
- Start fluent on "A": ```docker start fluentd```
- Check your logs on "B": check "msg": _number,_ **the numbering is not continuous.**

It is reproducible without docker-compose (docker run).

```
docker info
Containers: 0
 Running: 0
 Paused: 0
 Stopped: 0
Images: 232
Server Version: 18.06.1-ce
Storage Driver: overlay2
 Backing Filesystem: extfs
 Supports d_type: true
 Native Overlay Diff: true
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins:
 Volume: local
 Network: bridge host ipvlan macvlan null overlay
 Log: awslogs fluentd gcplogs gelf journald json-file logentries splunk syslog
Swarm: inactive
Runtimes: runc
Default Runtime: runc
Init Binary: docker-init
containerd version: 468a545b9edcd5932818eb9de8e72413e616e86e
runc version: 69663f0bd4b60df09991c08812a60108003fa340
init version: fec3683
Security Options:
 seccomp
  Profile: default
Kernel Version: 4.9.93-linuxkit-aufs
Operating System: Docker for Mac
OSType: linux
Architecture: x86_64
CPUs: 4
Total Memory: 7.786GiB
Name: linuxkit-025000000001
ID: COKY:2GBZ:DNBD:QARH:Z7GI:GDLK:PNBO:7P64:GMPE:VGHR:3MQB:D73M
Docker Root Dir: /var/lib/docker
Debug Mode (client): false
Debug Mode (server): true
 File Descriptors: 26
 Goroutines: 58
 System Time: 2018-09-29T17:55:29.363968437Z
 EventsListeners: 2
HTTP Proxy: gateway.docker.internal:3128
HTTPS Proxy: gateway.docker.internal:3129
Registry: https://index.docker.io/v1/
Labels:
Experimental: true
Insecure Registries:
 127.0.0.0/8
Live Restore Enabled: false
```
