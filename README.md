# stangri's OpenWrt Packages Documentation

This is documentation for packages I'm maintaining for OpenWrt routers. While some of these are packages are already available from official OpenWrt release/snapshots repositories/feeds, [my packages repo](https://repo.openwrt.melmac.net) usually contains newer versions. You can also browse/check-out the [source code](https://source.openwrt.melmac.net).

## How to use

### On your router

The repository is currently hosted at [GitHub](https://github.com). If you have problems accessing [my packages repo](https://repo.openwrt.melmac.net) or access to [GitHub](https://github.com) may be blocked at the location where your router is installed, skip to the [Add Repository (jsDelivr)](#add-repository-jsdelivr) section. Both repositories use HTTPS protocol and require one of the SSL support packages to be installed on your router.

#### Add Repository (GitHub)

```sh
opkg update
opkg install wget-ssl
echo -e -n 'untrusted comment: OpenWrt usign key of Stan Grishin\nRWR//HUXxMwMVnx7fESOKO7x8XoW4/dRidJPjt91hAAU2L59mYvHy0Fa\n' > /etc/opkg/keys/7ffc7517c4cc0c56
sed -i '/stangri_repo/d' /etc/opkg/customfeeds.conf
echo 'src/gz stangri_repo https://repo.openwrt.melmac.net' >> /etc/opkg/customfeeds.conf
opkg update
```

#### Add Repository (jsDelivr)

```sh
opkg update
opkg install wget-ssl
echo -e -n 'untrusted comment: OpenWrt usign key of Stan Grishin\\nRWR//HUXxMwMVnx7fESOKO7x8XoW4/dRidJPjt91hAAU2L59mYvHy0Fa\\n' > /etc/opkg/keys/7ffc7517c4cc0c56
sed -i '/stangri_repo/d' /etc/opkg/customfeeds.conf
echo 'src/gz stangri_repo https://cdn.jsdelivr.net/gh/stangri/repo.openwrt.melmac.net' >> /etc/opkg/customfeeds.conf
opkg update
```

Please note that there may be delay in [jsDelivr CDN](https://cdn.jsdelivr.net/gh/stangri/repo.openwrt.melmac.net) cache updates comparing to [my packages repo at GitHub](https://repo.openwrt.melmac.net) which may cause `opkg` to pull older files and/or complain about wrong signature.

### Image Builder (GitHub)

Add the following line:

```sh
src/gz stangri_repo https://repo.openwrt.melmac.net
```

to the `repositories.conf` file inside your Image Builder directory. You can use the following shell script code to achieve that:

```sh
sed -i '/stangri_repo/d' repositories.conf
! grep -q 'stangri_repo' repositories.conf && sed -i '4 i\src/gz stangri_repo https://repo.openwrt.melmac.net' repositories.conf
```

### Image Builder (jsDelivr)

Add the following line:

```sh
src/gz stangri_repo https://cdn.jsdelivr.net/gh/stangri/repo.openwrt.melmac.net
```

to the `repositories.conf` file inside your Image Builder directory. You can use the following shell script code to achieve that:

```sh
sed -i '/stangri_repo/d' repositories.conf
! grep -q 'stangri_repo' repositories.conf && sed -i '4 i\src/gz stangri_repo https://cdn.jsdelivr.net/gh/stangri/repo.openwrt.melmac.net' repositories.conf
```

### SDK

The packages source code is available in my packages source on [GitHub](https://source.openwrt.melmac.net)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/source.openwrt.melmac.net/). Check out the code for the individual packages you want into your SDK's `package` folder or for luci apps into the `package/luci/applications` folder.

## Description of packages

### adblock-fast & luci-app-adblock-fast

This service provides lightweight and very fast dnsmasq-based ad blocking. Please see the README at [GitHub](https://docs.openwrt.melmac.net/adblock-fast/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/adblock-fast/README.md) and [OpenWrt Forum Thread](https://forum.openwrt.org/t/adblock-fast-ad-blocking-service-for-dnsmasq-and-unbound/) for further information. This package is an improved version of [simple-adblock](#simple-adblock--luci-app-simple-adblock).

### https-dns-proxy & luci-app-https-dns-proxy

This is a lean RFC8484-compatible DNS-over-HTTPS (DoH) proxy service which supports DoH servers ran by AdGuard, CleanBrowsing, Cloudflare, Google, ODVR (nic.cz) and Quad9. Please see the README at [GitHub](https://docs.openwrt.melmac.net/https-dns-proxy/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/https-dns-proxy/README.md) for further information.

### luci-app-advanced-reboot

This package enables Web UI for reboot to another partition functionality on supported (dual-partition) routers and to power off (power down) your router. Please see the README at [GitHub](https://docs.openwrt.melmac.net/luci-app-advanced-reboot/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/luci-app-advanced-reboot/README.md) and [OpenWrt Forum Thread](https://forum.openwrt.org/t/web-ui-to-reboot-to-another-partition-for-dual-partition-routers/3423) for further information.

### netclient

Netclient is the client for Netmaker networks. To learn more about Netmaker, see [Netmaker README](https://github.com/gravitl/netmaker). Please see the README at [GitHub](https://docs.openwrt.melmac.net/netclient/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/netclient/README.md) and [OpenWrt Forum Thread](https://forum.openwrt.org/t/netclient-the-client-for-netmaker-networks/) for further information.

### pbr & luci-app-pbr

This service can be used to enable policy-based routing for WAN/WAN6 interfaces and multiple VPN tunnels. Supported VPN protocols include: L2TP, Openconnect, OpenVPN, Softether and Wireguard. Policies can be based on domain names, IP addresses, ports or any combination of the above. This service supports policies for both outgoing and incoming traffic to target specific interfaces/tunnels. Please see the README at [GitHub](https://docs.openwrt.melmac.net/pbr/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/pbr/README.md) and [OpenWrt Forum Thread](https://forum.openwrt.org/t/policy-based-routing-pbr-package-discussion/) for further information.

## Description of outdated/obsolete packages

### antminer-monitor

This service can be used to monitor local BITMAIN Antminers. This is just the wrapper for [Antminer Monitor python app](https://github.com/anselal/antminer-monitor). **WARNING**: Requires a router with a lot of flash, 128Mb recommended. Please see the README at [GitHub](https://docs.openwrt.melmac.net/antminer-monitor/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/antminer-monitor/README.md) for further information.

### fakeinternet & luci-app-fakeinternet

This service can be used to fake internet connectivity for local devices.
Can be used on routers with no internet access to suppress warnings on local devices on no internet connectivity. Please see the README at [GitHub](https://docs.openwrt.melmac.net/fakeinternet/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/fakeinternet/README.md) and [OpenWrt Forum Thread](https://forum.openwrt.org/t/fakeinternet-service-package-wip/) for further information.

### libcurl with HTTP/3 and QUIC support

Instructions for building `libcurl` with HTTP/3 and QUIC support using out of the tree OpenSSL-QuicTLS can be found on [GitHub](https://docs.openwrt.melmac.net/curl/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/curl/README.md)

### luci-app-easyflash

This package installs Web UI for quickly updating your router firmware if you use automated snapshots build process which produces fully customized images and uploads them to your router. Requires sysupgrade-compatible upgrade file `/tmp/firmware.img` and a one-line description (target/version/filename info) in `/tmp/firmware.tag`. WARNING: does not keep your router settings.

### luci-mod-alt-reboot

This package enables Web UI for reboot to another partition functionality on supported (dual-partition) routers and to power off (power down) your router by overwriting default System --> Reboot page. Please see the README at [GitHub](https://docs.openwrt.melmac.net/luci-mod-alt-reboot/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/luci-mod-alt-reboot/README.md) for further information. This package has been superseded by `luci-app-advanced-reboot` and is no longer developed/supported.

### luci-theme-material-old

This package brings back the old button styles to the `luci-theme-material` on OpenWrt 18.06.0-rc2 and later. Please see the README at [GitHub](https://docs.openwrt.melmac.net/luci-theme-material-old/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/luci-theme-material-old/README.md) for further information.

### nebula

Nebula is a scalable overlay networking tool with a focus on performance, simplicity and security. It lets you seamlessly connect computers anywhere in the world. [Nebula is being developed by Slack](https://github.com/slackhq/nebula). Please see the README at [GitHub](https://docs.openwrt.melmac.net/nebula/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/nebula/README.md) and [OpenWrt Forum Thread](https://forum.openwrt.org/t/slacks-nebula-on-openwrt-discussion-thread/) for further information.

### simple-adblock & luci-app-simple-adblock

This service provides lightweight and very fast dnsmasq-based ad blocking. Please see the README at [GitHub](https://docs.openwrt.melmac.net/simple-adblock/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/simple-adblock/README.md) and [OpenWrt Forum Thread](https://forum.openwrt.org/t/simple-adblock-fast-lightweight-and-fully-uci-luci-configurable-ad-blocking/1327) for further information. This package has been obsoleted by [adblock-fast](#adblock-fast--luci-app-adblock-fast).

### slider-support

This package enables switching between `Router`, `Access Point` and `Wireless Repeater` modes of operation for supported routers equipped with slider switch. It also sets the correct `current mode` setting for the `WLAN Blinker` service (README at [GitHub](https://docs.openwrt.melmac.net/wlanblinker/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/wlanblinker/README.md)). Please see the README at [GitHub](https://docs.openwrt.melmac.net/slider-support/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/slider-support/README.md) for further information.

### vpnbypass & luci-app-vpnbypass

This service can be used to enable split tunneling for outgoing traffic for a single OpenVPN tunnel used as the default gateway. Supports accessing domains, IP ranges outside of your OpenVPN tunnel (bypassing OpenVPN tunnel) over IPv4. Please see the README at [GitHub](https://docs.openwrt.melmac.net/vpnbypass/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/vpnbypass/README.md) and [OpenWrt Forum Thread](https://forum.openwrt.org/t/vpn-bypass-split-tunneling-service-luci-ui/) for further information. This package has been obsoleted by [pbr](#pbr--luci-app-pbr).

### vpn-policy-routing & luci-app-vpn-policy-routing

This service can be used to enable policy-based routing for WAN/WAN6 interfaces and multiple VPN tunnels. Supported VPN protocols include: L2TP, Openconnect, OpenVPN and Wireguard. Policies can be based on domain names, IP addresses, ports or any combination of the above. This service supports policies for both outgoing and incoming traffic to target specific interfaces/tunnels. Please see the README at [GitHub](https://docs.openwrt.melmac.net/vpn-policy-routing/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/vpn-policy-routing/README.md) and [OpenWrt Forum Thread](https://forum.openwrt.org/t/vpn-policy-based-routing-web-ui-discussion/) for further information. This package has been obsoleted by [pbr](#pbr--luci-app-pbr).

### wlanblinker & luci-app-wlanblinker

This service can be used to indicate WLAN status by blinking the unused LED. Please see the README at [GitHub](https://docs.openwrt.melmac.net/wlanblinker/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/wlanblinker/README.md) for further information.

### wireshark-helper & luci-app-wireshark-helper

This service can be used to configure router to sniff packets to/from monitored device on the device running Wireshark app. Please see the README at [GitHub](https://docs.openwrt.melmac.net/wireshark-helper/)/[jsDelivr](https://cdn.jsdelivr.net/gh/stangri/docs.openwrt.melmac.net/wireshark-helper/README.md) for further information.

<!-- markdownlint-disable MD033 -->

<script defer src='https://static.cloudflareinsights.com/beacon.min.js' data-cf-beacon='{"token": "911798f2c34b45338f8f8182830a3eb6"}'></script>
