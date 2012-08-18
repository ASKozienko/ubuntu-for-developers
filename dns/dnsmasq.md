# Ubuntu Wildcard DNS for developers

### Ubuntu 12.04 users should disable hardcoded `dnsmasq`

```bash
$ sudo nano /etc/NetworkManager/NetworkManager.conf
```

```bash
[main]
plugins=ifupdown,keyfile
#dns=dnsmasq

[ifupdown]
managed=false
```

### Restart NetworkManager
```bash
$ sudo service network-manager restart
```

### Install standalone `dnsmasq` from repo
```bash
$ sudo apt-get install dnsmasq
```

### Save original `dnsmasq` conf
```bash
$ sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig
```

### Create new conf with next content
```bash
# Listen only on localhost
listen-address=127.0.0.1
bind-interfaces

# The default is 150 dns entries to be cached.
cache-size=1000

# Make sure that DNS requests going out contain a valid domain
domain-needed

# Read the IP addresses of the upstream nameservers from <file>, instead of /etc/resolv.conf.
# For the format of this file see resolv.conf(5)
# resolv-file=/etc/resolv.dnsmasq

# Wildcard DNS zone for devel VHOSTs
# i.e. any_name.dev will be resolved as 127.0.0.1
address=/dev/127.0.0.1
```

### Enable auto start `dnsmasq` service and start him

```bash
$ sudo update-rc.d dnsmasq default
$ sudo service dnsmasq start
```
