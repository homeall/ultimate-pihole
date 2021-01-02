## PiHole with cloudflared - DoH - caddy reverse proxy and dhcphelper

The [docker-compose.yml](https://raw.githubusercontent.com/homeall/pihole-docker/main/docker-compose.yml) contains simple way to deploy to any enviroment.

You will have [PiHole](https://pi-hole.net) plus [cloudflared](https://github.com/homeall/cloudflared) docker with DoH enabled and only **security upstreams**.

Also it will have [Caddy](https://caddyserver.com) reverse proxy with https enabled and cert from [Let's Encrypt](https://letsencrypt.org).

If you will need to get DHCP in docker container, you can use [dhcphelper](https://github.com/homeall/dhcphelper), a tool for DHCP Relay Broadcast message.

### Optional config

At the moment you can not pass DHCP settings when you lunch a new docker container. See this ticket [link](https://github.com/pi-hole/docker-pi-hole/issues/598).

But you can add already prepared in advance on your `etc-pihole` mounting volume `setupVars.conf`:

```
WEBPASSWORD=XXXXXXXXZZZZZZZZYYYYYYYYYY
WEBTHEME=default-dark
BLOCKING_ENABLED=true
PIHOLE_DOMAIN=lan
DHCP_LEASETIME=24
DHCP_ACTIVE=true
DHCP_START=10.X.X.X
DHCP_END=10.X.X.X
DHCP_ROUTER=10.X.X.X
DHCP_LEASETIME=48
PIHOLE_DOMAIN=lan
DHCP_IPv6=true
DHCP_rapid_commit=true
DNSSEC=true
QUERY_LOGGING=true
INSTALL_WEB_SERVER=true
INSTALL_WEB_INTERFACE=true
IPV4_ADDRESS=172.31.0.100
PIHOLE_DNS_1=172.31.0.53#54
PIHOLE_INTERFACE=eth0
```

Also you will need to mount `etc-dnsmask` volume in order to set the right DNS server address such as `02-dhcp-options.conf` and add:

```dhcp-option=option:dns-server,10.X.X.X```
