# RouterOS-v7-Cloudflare-IPV6-DDNS
ROS v7.15.3 部署Cloudflare的IPV6 DDNS服务的脚本
ROS v7.15.3 Script for deploying Cloudflare's IPV6 DDNS service

该脚本通过DHCPv6 Client来获取ipv6地址（因为学校的路由器只分配v6的address，不分配prefix）。因此，若您通过pppoe等方式获取v6地址，需要对改脚本的代码稍作修改。
The script uses the DHCPv6 Client to get the ipv6 address (because the school router only assigns the v6 address, not the prefix). Therefore, if you obtain v6 addresses through pppoe, you need to modify the code of the script.

我使用 ":set WanIP6 [/ipv6 dhcp-client get [find interface=$WAN6Interface status=bound] address];"的方式获取当前WAN口的IPV6地址：
I use ":set WanIP6 [/ipv6 dhcp-client get [find interface=$WAN6Interface status=bound] address];" method to obtain the IPV6 address of the current WAN interface:
![address](https://github.com/user-attachments/assets/8791353c-9bb5-4be6-bc3c-d70be563feb2)

实际得到的address由"真正的address, address expires after"两部分构成，因此需要使用":set WanIP6 [:pick $WanIP6 0 [:find $WanIP6 ", "]];"命令去截断并得到前半部分。
The actual address is composed of a two-tuples "REAL address, address expires after", so need to use ":set WanIP6 [:pick $WANIP60 [:find $WanIP6 ", "]];" to truncate  and get the first half.

参考文献：
References:
https://github.com/kiss2u/ros-cloudflare-ddns/tree/master
https://www.bilibili.com/video/BV12y411q7q4（纯v4的Cloudflare DDNS教程）
https://www.cloudrw.com/article/routeros-ddns-cloudflare（此教程存在多处错误，注意鉴别）
