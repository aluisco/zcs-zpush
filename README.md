# zcs-zpush
This repository is source for integrating Zimbra Single Server and Z-Push + Zimbra Backend to achieve ActiveSync on Zimbra OSE.

# Integrating Zimbra and Z-push 2.5.1 with zimbrabackend71 on Ubuntu 18.04/20.04 and Zimbra 8.8.15+

Install dependecies

```bash
apt update
apt install git php7.4-cli php7.4-cgi php7.4-soap php7.4-mbstring php7.4-curl php7.4-xml php-memcached -y
```

Clone repo

```bash
git clone https://github.com/aluisco/zcs-zpush.git
cd zcs-zpush
```

Create folder for log

```bash
mkdir -p /var/lib/z-push /var/log/z-push
chmod 755 -R /var/lib/z-push /var/log/z-push
chown zimbra:zimbra -R /var/lib/z-push /var/log/z-push
```

Save z-push folder on /opt/

```bash
cp -rvf z-push /opt/
```

Create symlink

```bash
ln -sf /opt/z-push /opt/zimbra/jetty/webapps/
```

Save php script on /usr/bin

```bash
cp php-cgi-fix.sh /usr/bin/php-cgi-fix.sh
chmod +x /usr/bin/php-cgi-fix.sh
```

Backup and replace jetty.xml.in

### For 8.8.15

```bash
cp /opt/zimbra/jetty/etc/jetty.xml.in /opt/zimbra/jetty/etc/jetty.xml.in.backup
cp jetty.xml.in-for-zcs-8815 /opt/zimbra/jetty/etc/jetty.xml.in
chown zimbra:zimbra /opt/zimbra/jetty/etc/jetty.xml.in
```

### For 9.0.0

```bash
cp /opt/zimbra/jetty/etc/jetty.xml.in /opt/zimbra/jetty/etc/jetty.xml.in.backup
cp jetty.xml.in-for-zcs-9 /opt/zimbra/jetty/etc/jetty.xml.in
chown zimbra:zimbra /opt/zimbra/jetty/etc/jetty.xml.in
```

Replace php.ini

```bash
cp /etc/php/7.4/cgi/php.ini /etc/php/7.4/cgi/php.ini.backup
cp php.ini /etc/php/7.4/cgi/php.ini
```

Restart Zimbra Mailbox

```bash
su - zimbra -c 'zmmailboxdctl restart'
```

For testing, please access https://ip-of-zimbra/Microsoft-Server-ActiveSync from your browser. Or you can configure your mobile devices and ensure exchange as protocol
