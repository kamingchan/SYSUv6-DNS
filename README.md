# SYSUv6-DNS

这个项目是由 [SYSUv6-hosts](https://github.com/LGA1150/SYSUv6-hosts) 启发，利用 dnsmasq 和 [Pcap_DNSProxy](https://github.com/chengr28/Pcap_DNSProxy)实现的中山大学校园网 DNS，主要由 [LGA1150](https://github.com/LGA1150) 负责维护。

## 原理

在中山大学，对于一般的网络流量大多数的出口是中国联通和中国移动，平均带宽只有 [4Mbps 左右](http://helpdesk.sysu.edu.cn/images/Announce/noteshengji.png)，但实际上校园网的出口还有长城宽带和教育网，且教育网支持 IPv4 与 IPv6。本 DNS 能有效地将部分有域名解析到长城宽带、教育网的 CDN 上，从而提高网速。另外本 DNS 附带防污染功能，国外域名主要解析到香港的 IP 上。对于某些访问不通畅而又只提供 HTTPS 访问的域名，会解析到港澳的 SNI PROXY 上，以提高加载速度。[点此查看加速的网站列表（不完整）](https://github.com/bazingaterry/SYSUv6-DNS/wiki/Accelerated-Unblocked-Websites-List)  

为了更好的上网体验，需要使用 [HTTPS Everywhere](https://www.eff.org/https-everywhere) 浏览器扩展，但目前该扩展对国内网站的支持较差，若访问国内网站出现问题，请尝试停用该网站规则或停用扩展（如无法登录新浪网的帐号，请尝试停用`sina.com.cn`的规则）。  

如果想新增加速网站，请提交 issue ，我们将会检测该网站是否可加速。  

## 使用方法

你可以下载 `conf/` 内的配置，利用 dnsmasq 和 [Pcap_DNSProxy](https://github.com/chengr28/Pcap_DNSProxy) 自行搭建 DNS，请注意对应路径和上游 DNS 的修改。

## 公共 DNS 细节

你可以直接使用我们搭建的 DNS。

若你在校园网内，只需要将 DNS 地址改为：`172.16.37.20` 与 `172.16.91.162` 即可。但请注意此 DNS 在寒暑假期间并不会提供服务。

这两个 DNS 节点分别部署在两台 Mac mini 上，其中一台通过千兆以太网与校园网相连，另外一台是百兆以太网，地点为珠海校区。虽然部署在学生宿舍，但是我们会尽量确保 DNS 服务器的正常运行。

这两个 DNS 以 [Pcap_DNSProxy](https://github.com/chengr28/Pcap_DNSProxy) 作为上游 DNS，开启双向过滤，以解决 DNS 污染和国内外 CDN 的问题。其中，国内 DNS 的选择是 `114.114.115.115`。

