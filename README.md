# SYSUv6-DNS

这个项目是由 [SYSUv6-hosts](https://github.com/LGA1150/SYSUv6-hosts) 启发，利用 dnsmasq 和 [Pcap_DNSProxy](https://github.com/chengr28/Pcap_DNSProxy) 实现的中山大学校园网 DNS，主要由 [LGA1150](https://github.com/LGA1150) 负责维护。

## 原理

在中山大学，对于一般的网络流量大多数的出口是中国联通和中国移动，平均带宽只有 6Mbps 左右，但实际上校园网的出口还有长城宽带和教育网，且教育网支持 IPv4 与 IPv6。本 DNS 能有效地将部分有域名解析到长城宽带、教育网的 CDN 上，从而提高网速。

为了更好的上网体验，需要使用 [HTTPS Everywhere](https://www.eff.org/https-everywhere) 浏览器扩展，但目前该扩展对国内网站的支持较差，若访问国内网站出现问题，请尝试停用该网站规则或停用扩展（如无法登录新浪网的帐号，请尝试停用`sina.com.cn`的规则）。

如果想新增加速网站，请提交 issue ，我们将会检测该网站是否可加速。

## 使用方法

你可以下载 `conf/` 内的配置，利用 dnsmasq 和 [Pcap_DNSProxy](https://github.com/chengr28/Pcap_DNSProxy) 自行搭建 DNS，请注意对应路径和上游 DNS 的修改。

## 公共 DNS 细节

你可以直接使用我们搭建的 DNS。

若你在校园网内，只需要将主 DNS 地址改为：`172.18.157.17`，备用 DNS 地址改为：`172.18.156.31` 即可，但请注意此 DNS 在寒暑假期间并不会提供服务。

主 DNS 节点部署在一台 WRT1900ACv2 上，通过千兆以太网与校园网相连；而备用 DNS 节点部署在 斐讯K2 上，通过百兆以太网与校园网相连。地点为东校区。虽然部署在学生宿舍，但是我们会尽量确保 DNS 服务器的正常运行。

## 其他
[如何在路由器后获取到 IPv6 地址](https://github.com/bazingaterry/SYSUv6-DNS/wiki/%E5%A6%82%E4%BD%95%E5%9C%A8%E8%B7%AF%E7%94%B1%E5%99%A8%E5%90%8E%E8%8E%B7%E5%8F%96-IPv6-%E5%9C%B0%E5%9D%80)

## 许可

本仓库的所有内容使用 [![CC Image]][CC BY-NC-SA 4.0] 4.0 许可。



[CC Image]: https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png
[CC BY-NC-SA 4.0]: https://creativecommons.org/licenses/by-nc-sa/4.0/
