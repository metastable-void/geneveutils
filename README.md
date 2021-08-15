# geneveutils
GENEVE networking simplified for GNU/Linux systems.

## Usage

```
./bin/geneveutils pre-up <geneve interface config>

./bin/geneveutils post-down <geneve interface config>

./bin/geneveutils restart <geneve interface config>
```

Clone this repository:

```
# cd /etc/network
# git clone https://github.com/metastable-void/geneveutils.git
```

/etc/network/interfaces.d/geneve-31:

```
auto geneve-31
iface geneve-31 inet static
    pre-up /etc/network/geneveutils/bin/geneveutils pre-up /etc/network/geneve/geneve-31.conf
    post-down /etc/network/geneveutils/bin/geneveutils post-down /etc/network/geneve/geneve-31.conf
    address 10.199.31.1/24
    broadcast 10.199.31.255
    mtu 1430
```

/etc/network/geneve/geneve-31.conf:

```
# This script is sourced with /bin/sh.

# The interface name of the GENEVE device.
GENEVE_IFNAME=geneve-31

# 4 for IPv4 and 6 for IPv6.
GENEVE_IP_VERSION=4

# The GENEVE ID of the device.
GENEVE_ID=31

# The link device to use.
GENEVE_LINKDEV=eth0

# Remote endpoint (IP address or hostname)
GENEVE_REMOTE=remotemachine.local
```

/etc/cron.d/geneve-31:

```
31 * * * * root /etc/network/geneveutils/bin/geneveutils restart /etc/network/geneve/geneve-31.conf
```

## License

GNU GPL version 3 or any later version.
