OVPNOncerator
============

Quick and dirty python script to take values from your server.conf and plop them into ovpn and onc files. 

It assumes an installation of /etc/openvpn for your server.conf and /etc/openvpn/easy-rsa/pki for your PKI store. You can change these values with --config and --keystore, respectively. Also assumes you're using certificate-based auth and a TLS Authentication key. Supports PAM. 

Usage: 

```
sudo python ovpnoncorator.py 
```
or

```
sudo python ovpnoncorator.py -c /path/to/my/server.conf -k /path/to/my/keystore-directory
```

To get your onc files working on Chromebook:

1. On your Chromebook, open Chrome, chrome://settings/certificates.
2. Import & Bind to Device, select the p12. Currently, this is given an insecure "chrome" password on generation; you can change this in the script if you want. 
3. Then chrome://net-internals > ChromeOS.
4. Click Import ONC, navigate to your generated onc file, Import. The interface will tell you "no file chosen," but if you tap your wifi network icon in the system tray, tap VPN Connections, it should show up unless there was a parsing error. (If you find out where or whether these parsing errors get logged anywhere, lemme know - couldn't find 'em in /var/log/\*)
5. Connect. You'll be prompted for a password, you can put anything there if you're just using certificates, the server doesn't care if it doesn't need it, but Chrome won't let you connect without a value there.

WARNING: ChromeOS uses an old version of OpenVPN without TLS 1.2 support. If enabled on the server, it will never connect. Please do a solid and star the [Chromium bug](https://bugs.chromium.org/p/chromium/issues/detail?id=707517). (And any other OpenVPN-Chrome bugs you happen to see: OpenVPN support in Chrome needs love.)
