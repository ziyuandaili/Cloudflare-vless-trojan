# Cloudflare-workers/pages代理脚本【目前版本：25.7.13】
### 1、本项目仅支持本地化部署
### 2、本项目配置都为本地化编辑，不使用订阅器、订阅转换等第三方外链引用
### 3、无需担心节点订阅信息被订阅器作者或者订阅转换作者后台查看
--------------------------------
## 脚本特色：
#### 1、懒人小白专用！默认节点都为CF官方IP，无需频繁更新订阅获取客户端优选IP
#### 2、为减少新手小白额外的成本，本项目不推荐使用自定义域名，如果你一定要用自定义域名，也可以
#### 3、当在CF点击部署按钮后，可直接手搓节点或者使用分享链接，最多设置一个uuid/密码，其他不用改
#### 4、Workers方式：支持vless+ws+tls、trojan+ws+tls、vless+ws、trojan+ws代理节点
#### 5、Pages方式：支持vless+ws+tls、trojan+ws+tls代理节点
#### 6、支持单节点链接、聚合通用节点链接、聚合通用节点订阅、sing-box节点订阅、clash节点订阅
#### 7、虽然仅乱码混淆版可用，但只有修改uuid/密码时才必须使用变量
#### 8、VLESS仅nat64套壳版将自动填充proxyip，无需且不支持proxyip设置，由[badafans](https://github.com/badafans)提供代码
-------------------------------------------------------------
### 全网资源联盟平台：[我的资源星球](https://zyxq.me)、[资源星球联盟](https://zyxq.org)、[网盘资源站](https://zyxq.xyz)、[在线影视站](https://zyxq.net)、[学搞钱平台](https://xuegaoqian.com)
---------------------------------------------

## 一：CF Vless节点可设置的变量内容 (仅nat64套壳版无需且不支持设置proxyip)

| 变量作用 | 变量名称| 变量值要求| 变量默认值| 变量要求|
| :--- | :--- | :--- | :--- | :--- |
| 1、必要的uuid | uuid (小写字母) |符合uuid规定格式 |万人骑uuid：86c50e3a-5b87-49dd-bd20-03c7f2735e40|建议|
| 2、全局节点能上CF类网站 | proxyip (小写字母) |443端口：ipv4地址、[ipv6地址]、域名。非443端口：IPV4地址:端口、[IPV6地址]:端口、域名:端口|proxyip：留空|可选|
| 3、订阅节点：优选IP | ip1到ip13，共13个 |CF官方IP、CF反代IP、CF优选域名| CF官方不同地区的visa域名|可选|
| 4、订阅节点：优选IP对应端口 | pt1到pt13，共13个 |CF13个标准端口、反代IP对应任意端口| CF13个标准端口|可选|


## 二：CF Trojan节点可设置的变量内容

| 变量作用 | 变量名称| 变量值要求| 变量默认值| 变量要求|
| :--- | :--- | :--- | :--- | :--- |
| 1、必要的密码 | pswd (小写字母) |建议字母数字 |万人骑密码：trojan|建议|
| 2、全局节点能上CF类网站 | proxyip (小写字母) |443端口：ipv4地址、[ipv6地址]、域名。非443端口：IPV4地址:端口、[IPV6地址]:端口、域名:端口|proxyip：留空|可选|
| 3、订阅节点：优选IP | ip1到ip13，共13个 |CF官方IP、CF反代IP、CF优选域名| CF官方不同地区的visa域名|可选|
| 4、订阅节点：优选IP对应端口 | pt1到pt13，共13个 |CF13个标准端口、反代IP对应任意端口| CF13个标准端口|可选|

#### 订阅节点中IP与端口的变量（3与4）特别注意 【新手小白可无视变量（3与4），使用默认即可】

0、由于现在只能用混淆代码，无法在文件上直接修改了，只能使用变量

1、切记：当你非要用订阅类的客户端，且要改优选IP时，才需要设置ip1到ip13，pt1到pt13的变量

2、ip1到ip7，pt1到pt7，在订阅分享链接中，仅支持80系端口关TLS节点

3、ip8到ip13，pt8到pt13，在订阅分享链接中，仅支持443系端口开TLS节点

4、设置官方IP，无需设置端口（默认已设置13个CF标准端口）；设置反代IP需要分开关TLS，端口变量也必须设置

---------------------------------
## 三：自定义proxyip

虽说脚本默认自带其他大佬的proxyip，但同时也支持自定义proxyip

支持IPV4、IPV6、域名三种方式（端口为443时，可不写:端口）

1、全局节点变量形式（上文一与二已说明）：

| proxyip端口 | IPv4形式| IPv6形式| 域名形式|
| :--- | :--- | :--- | :--- |
| 443端口 | IPV4地址 |[IPV6地址] |域名|
| 非443端口 | IPV4地址:端口 |[IPV6地址]:端口 |域名:端口|

2、单节点path路径形式：

| proxyip端口 | IPv4形式| IPv6形式| 域名形式|
| :--- | :--- | :--- | :--- |
| 443端口 | /pyip=IPV4地址 |/pyip=[IPV6地址] |/pyip=域名|
| 非443端口 | /pyip=IPV4地址:端口 |/pyip=[IPV6地址]:端口 |/pyip=域名:端口|

注意：

1、单节点path路径变更proxyip：仅影响当前客户端正在设置的单节点，并不影响其他单节点或者订阅节点的proxyip

2、全局节点变更proxyip：影响所有未设置path路径proxyip的节点

3、当节点的path路径出现```/pyip=```关键字时，此节点的proxyip只认准path路径设置的proxyip，全局proxyip不起作用

---------------------------------
## 四：无需socks5！小白利用reality协议一键自制proxyip、80系/443系的任意端口反代IP

### 1、Serv00专用：

修改自Serv00老王sing-box安装脚本，支持一键三协议：vless-reality、vmess-ws(argo)、hysteria2。

主要增加reality协议默认支持 CF vless/trojan 节点的proxyip以及非标端口的优选反代IP功能

### 2、VPS专用：

推荐使用 离中国近、便宜、流量多的纯IPV6的vps进行搭建。近可能避免使用IPV4，因为IPV4大概率被大佬们偷扫反代IP，成为他们的公益或收费反代IP库。如果非要用IPV4，请时常关注下自己VPS的流量，使用proxyip与客户端优选IP都会消耗VPS流量

### 3、可现实以下四种情况(推荐在TLS节点环境下)：

可选择现实1：仅用于客户端优选IP，即CF节点访问非CF网站的落地IP地区与VPS地区一致，访问CF网站落地IP地区根据proxyip决定

可选择现实2：仅用于proxyip，即CF节点访问CF网站的落地IP地区与VPS地区一致，访问非CF网站落地IP地区根据客户端优选IP决定

可选择现实3：同时用于客户端优选IP与proxyip，即CF节点访问CF网站的落地IP地区、访问非CF网站落地IP地区，两者都与VPS地区一致

可选择现实4：通过在VPS安装WARP全局双栈V4+V6功能，即访问非CF网站的客户端优选IP的落地IP（104.28……/2a09:……）现实固定，或访问CF网站的proxyip的落地IP（104.28……/2a09:……）现实WARP解锁功能效果

-------------------------------------------

## 五：查看配置信息与分享链接

CF Vless：在网页地址栏输入 https:// workers域名 或者 pages域名 或者 自定义域名 /自定义uuid

CF Trojan：在网页地址栏输入 https:// workers域名 或者 pages域名 或者 自定义域名 /自定义密码

注意：

1、workers域名 或者 pages域名 或者 自定义域名如果都被墙，必须开代理才能打开

2、使用自定域时，原先workers域名 或者 pages域名下的配置信息与分享链接依旧可用

---------------------------------

## 六：优选IP应用

CF官方优选80系端口：80、8080、8880、2052、2082、2086、2095

CF官方优选443系端口：443、2053、2083、2087、2096、8443

如果你没有天天最高速度或者选择国家的需求，使用默认的CF官方IP或者域名即可，不必更换

推荐好记的懒人专属CF官方IP如下，支持13个标准端口切换，称之为"冲在最前的不死IP"

104.16.0.0 

104.17.0.0 

104.18.0.0 

104.19.0.0 

104.20.0.0 

104.21.0.0 

104.22.0.0 

104.24.0.0 

104.25.0.0 

104.26.0.0 

104.27.0.0 

172.66.0.0

172.67.0.0

162.159.0.0

2606:4700::0 需IPV6环境

通过配置变量修改，可使用他人分享的IP或者域名，也可以自行本地优选，相关优选应用与脚本可参考视频教程

本地电脑端优选项目推荐（可在上面代码区直接下载）：

1、CDN优选域名V23.8.18 (电脑win64)

2、CF优选反代IP (电脑版，带测速)

3、CF优选官方IP (电脑版、可选择部分国家)

4、CF优选官方IP (美、亚、欧三地区无交互电脑版)

5、CF优选官方IP (电脑版，带测速)

注意：多个CF节点在客户端使用负载均衡或者自动选择时，建议所有应用的节点都为同一个国家地区，以避免不同国家之间的IP乱跳现象

---------------------------------

## 七：客户端推荐

#### 启用分片(Fragment)功能的好处：无视域名被墙TLS阻断，从而让workers等被墙的域名支持TLS节点
#### 提示：未被墙TLS阻断的自定义域名或pages域名无需开启分片就可使用TLS节点
 
目前支持该功能的平台客户端如下（点击名称即跳转到官方下载地址）

1、安卓Android：[v2rayNG](https://github.com/2dust/v2rayNG/tags)、[Nekobox](https://github.com/starifly/NekoBoxForAndroid/releases)、[Karing](https://github.com/KaringX/karing/tags)、v2box

2、电脑Windows：[v2rayN](https://github.com/2dust/v2rayN/tags)、[Hiddify](https://github.com/hiddify/hiddify-next/tags)、[Karing](https://github.com/KaringX/karing/tags)

3、苹果Ios：Karing、Hiddify Proxy & VPN、Shadowrocket(小火箭)、Streisand、v2box

4、软路由：passwall、ssr-plus、homeproxy

注意：其他平台客户端未开启分片功能情况下，workers域的6个443系TLS节点是不可用的

注意：Shadowrocket(小火箭)、v2box、v2rayn、v2rayng客户端对trojan+ws有强制开启TLS问题，造成trojan+ws不通。且clash订阅没有trojan+ws节点。特此说明

---------------------------------
---------------------------------
## 优选域名、优选官方IP+反代IP一键脚本（在本地网络环境下利用termux或者ish运行）：

1、安卓请使用termux官方项目下载客户端（谷歌商店下载的不可用！）：https://github.com/termux/termux-app/releases/tag/v0.118.1

首次安装后，请先安装依赖：```pkg upgrade```，然后运行以下你要使用的脚本

2、苹果手机用户，由于ISH最新版有BUG导致脚本运行卡住，请使用ISH_1.2.2版本，可以用巨魔先安装再降级，网上也有其它指定旧版IPA安装的教程

首次安装后，请先安装依赖：```apk add curl bash```，然后运行以下你要使用的脚本

-------------------------------------------------------------
### 脚本1：CF-优选官方IP (默认美、亚、欧三地区 强烈推荐！！！)，安卓苹果手机平板专用：
```
curl -sSL https://raw.githubusercontent.com/ziyuandaili/Cloudflare_vless_trojan/main/cf/cf.sh -o cf.sh && chmod +x cf.sh && bash cf.sh
```
-------------------------------------------------------------

### 脚本2：CF-CDN优选公共大厂域名脚本，苹果安卓手机平板专用：
```
curl -sSL https://gitlab.com/rwkgyg/CFwarp/raw/main/point/CFcdnym.sh -o CFcdnym.sh && chmod +x CFcdnym.sh && bash CFcdnym.sh
```
------------------------------------------------------------------------
### 脚本3：CF-优选官方IP+反代IP二合一脚本（带测速），苹果安卓手机平板专用：
```
curl -sSL https://gitlab.com/rwkgyg/CFwarp/raw/main/point/cfip.sh -o cfip.sh && chmod +x cfip.sh && bash cfip.sh
```
------------------------------------------------------------------------
### 代码来源：[ca110us](https://github.com/ca110us/epeius)、[emn178](https://github.com/emn178/js-sha256/blob/master/src/sha256.js)、[3Kmfi6HP](https://github.com/3Kmfi6HP/EDtunnel)、[badafans](https://github.com/badafans/Cloudflare-IP-SpeedTest)、[XIU2](https://github.com/XIU2/CloudflareSpeedTest)
### 声明：所有代码来源于Github社区，并通过ChatGPT进行整合

[![Powered by DartNode](https://dartnode.com/branding/DN-Open-Source-sm.png)](https://dartnode.com "Powered by DartNode - Free VPS for Open Source")
