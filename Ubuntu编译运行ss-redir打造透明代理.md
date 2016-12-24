# Ubuntu编译运行ss-redir打造透明代理

```
sudo apt-get update

sudo apt-get install --no-install-recommends build-essential autoconf libtool libssl-dev \
    gawk debhelper dh-systemd init-system-helpers pkg-config asciidoc xmlto apg libpcre3-dev

git clone https://github.com/shadowsocks/shadowsocks-libev.git

cd shadowsocks-libev

dpkg-buildpackage -b -us -uc -i

cd ..

sudo dpkg -i shadowsocks-libev*.deb
```

```
sudo ss-redir -c <your_config.json> -v -u
```
注意这里的local_address一定要填写0.0.0.0，默认是127.0.0.1

```
sudo -i
iptables -t nat -A PREROUTING -p tcp -s 10.42.0.0/16 -j REDIRECT --to-ports 1080
iptables -t nat -A PREROUTING -p udp -s 10.42.0.0/16 -j REDIRECT --to-ports 1080
iptables -t nat -L -n
```
