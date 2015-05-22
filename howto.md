准备工作：

1、GCE服务器，亚洲1区

2、Ubuntu 系统

执行代码：

#sniproxy

apt-get update

sudo apt-get install  autotools-dev cdbs debhelper dh-autoreconf dpkg-dev gettext libev-dev libpcre3-dev libudns-dev pkg-config git

git clone https://github.com/dlundquist/sniproxy.git

cd sniproxy

./autogen.sh && dpkg-buildpackage

dpkg -i ../sniproxy_0.4.0_amd64.deb

然后修改配置文件：

vi /etc/sniproxy.conf

修改为：

user daemon

pidfile /var/run/sniproxy.pid

error_log {

    syslog daemon
    
    priority notice
    
}

listen 80 {
    proto http
}

listen 443 {
    proto tls
}

table {
    .\* *
}
