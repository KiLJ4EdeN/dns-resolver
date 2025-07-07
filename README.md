# dns-resolver
simple dns using unbound


### Install unbound

```bash
sudo apt update
sudo apt install unbound -y
```

### Edit unbound config

```bash
sudo nano /etc/unbound/unbound.conf.d/public.conf
```

put these in:

```bash
server:
    interface: 0.0.0.0
    port: 53
    access-control: 0.0.0.0/0 allow
    do-ip4: yes
    do-udp: yes
    do-tcp: yes
    hide-identity: yes
    hide-version: yes
    use-caps-for-id: yes
    prefetch: yes
    qname-minimisation: yes
    verbosity: 1
```

### open firewall port

```bash
sudo ufw allow 53/udp
sudo ufw allow 53/tcp
sudo ufw reload
```

### edit `/etc/systemd/resolved.conf`

find DNSStubListener=yes, and set it to no

```bash
DNSStubListener=no
```

### restart unbound

```bash
sudo systemctl restart unbound
sudo systemctl enable unbound
```

### restart systemd-resolved

```bash
sudo systemctl restart systemd-resolved
```
