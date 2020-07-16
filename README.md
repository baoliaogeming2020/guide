本项目所有文档为郭先生音频，通过支持 metalink 协议的下载软件下载音频，可以帮助向墙内战友传播。

<b>原理::</b>

metalink 下载协议支持 HTTP / FTP / Bittorrent 同时下载同一个文件，墙外战友在下载时可以通过Bittorrent向墙内分享流量，墙外战友下载同一个文件人数越多，墙内战友下载速度赶快。

metalink 是 xml 文件，内含相同文件的 HTTP / FTP / Bittorrent 链接，Bittorrent 以 btih 加密 hash 方式写入，而此 btih-hash 与 magnet-btih 完全相同，这样，墙外战友下载后可以直接将 btih-hash 构造成 magnet 文本后向墙内战友传播，墙内战友直接可以下载。而 magnet 首先会下载一个 Bittorrent 种子，然后可以通过所有 Bittorrent 软件进行下载。GFW 是无法完全封锁 Bittorrent 软件的 tracker 服务器的。

<b>tracker 服务器网站::</b>

https://newtrackon.com/list

<b>DHT.dat下载::</b>

https://github.com/P3TERX/aria2.conf

<b>支持 metalink 软件汇总::</b>

aria2:是一款自由、跨平台命令行下载管理器，支持的下载协议有：HTTP / HTTPS / FTP / Bittorrent / Metalink。无 shell 基础战友不建议使用。
AriaNg:
aria2webui:
yaaw:

<b>本项目文件发布::</b>

本网站发布郭先生音频文件同时发布同文件名的 torrent / metalink / magnet 三种下载链接，墙外战友下载时尽量不要用 HTTPS 模式下载，因为只有后三种模式能向墙内战友提供流量。

<b>声明::</b>

本项目为穿墙模式的一种试探，所有方法与技术实现不向爆料革命战友保留版权，任何爆料革命战友都可以用相同的方式传播爆料革命。如果有战友能够将此方法转为一键脚本，最好能与本项目作者沟通，因项目还在一步步完善。

<b>MAC系统批量生成::</b>

1. 安装 homebrew:
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
2. 安装aria2:
brew install aria2
3. 安装mktorrent:
brew insatll mktorrent
4. 生成torrent:
mktorrent input_file
5. 生成magnet:
aria2c -S input_file.torrent
6. 生成metalink:
正准备写个脚本

<b>metalink 文件格式::</b>

<?xml version="1.0" encoding="utf-8"?>
<metalink xmlns="urn:ietf:params:xml:ns:metalink">
  <origin dynamic="false">文件http / https / FTP 链接</origin>
  <generator>发布者</generator>
  <published>发布时间，如：2020-07-15T22:49:42Z</published>
  <file name="文件名">
    <description>文件描述</description>
    <size>文件大小，文件基本信息内的大小</size>
    <hash type="md5">md5加密值，命令md5，如：7ce944e72074154248058a1292aa79d8</hash>
    <hash type="btih">bt种子生成magnet时的加密值，如：a8c93686d09cab35b04e648dab805d2b9165e23e</hash>
    <hash type="sha-256">sha-256加密值，命令shasum，如：7027880efd8b1e6abaa8f5919a3146878c457a38702281bba132c6f6f5bcd1ee</hash>
    <url location="" priority="30">文件http / https / FTP 链接，此元素可以多个，每个链接到最终文件要是同一个文件</url>
    <metaurl mediatype="torrent" priority="2">种子链接</metaurl>
    <metaurl mediatype="magnet" priority="2">magnet链接，如：magnet:?xt=urn:btih:a8c93686d09cab35b04e648dab805d2b9165e23e</metaurl>
  </file>
</metalink>
