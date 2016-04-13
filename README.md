# SYSUv6-DNS

这个项目是由 [SYSUv6-hosts](https://github.com/LGA1150/SYSUv6-hosts) 启发，利用 dnsmasq 实现的中山大学校园网 DNS，主要由 [LGA1150](https://github.com/LGA1150) 负责维护。

## 原理

在中山大学，对于一般的网络流量大多数的出口是中国联通和中国移动，平均带宽只有 [4Mbps 左右](http://helpdesk.sysu.edu.cn/images/Announce/noteshengji.png)，但实际上校园网的出口还有长城宽带和教育网，且教育网支持 IPv4 与 IPv6。本 DNS 能有效地将部分有域名解析到长城宽带、教育网的 CDN 上，从而提高网速。另外本 DNS 附带防污染功能，国外域名主要解析到香港的 IP 上。对于某些访问不通畅而又只提供 HTTPS 访问的域名，会解析到港澳的 SNI PROXY 上，以提高加载速度。

## 使用方法

你可以下载 `conf/` 内的配置，利用 dnsmasq 自行搭建 DNS，请注意对应路径和上游 DNS 的修改。

## 公共 DNS 细节

你可以直接使用我们搭建的 DNS。

若你在校园网内，只需要将 DNS 地址改为：`172.16.37.20` 与 `172.16.91.162` 即可。但请注意此 DNS 在寒暑假期间并不会提供服务。

这两个 DNS 节点分别部署在两台 Mac mini 上，其中一台通过千兆以太网与校园网相连，另外一台是百兆以太网，地点为珠海校区。虽然部署在学生宿舍，但是我们会尽量确保 DNS 服务器的正常运行。

这两个 DNS 以 [ChinaDNS](https://github.com/shadowsocks/ChinaDNS) 作为上游 DNS，开启双向过滤，以解决 DNS 污染和国内外 CDN 的问题。其中，国内 DNS 的选择是 `114.114.115.115`，海外 DNS 通过 [Shadowsocks-libev](https://github.com/shadowsocks/shadowsocks-libev) 的 ss-tunnel 功能加密转发 DNS 请求到香港阿里云的服务器上，此服务器上由 BIND 提供 DNS64 功能。



