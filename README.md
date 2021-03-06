![Logo](logo.png)

[![License](https://img.shields.io/badge/license-Public_domain-red.svg)](https://wiki.creativecommons.org/wiki/Public_domain)

About
----

**IPsum** is a threat intelligence feed based on 30+ different publicly available [lists](https://github.com/stamparm/maltrail) of suspicious and/or malicious IP addresses. All lists are automatically retrieved and parsed on a daily (24h) basis and the final result is pushed to this repository. List is made of IP addresses together with a total number of (black)list occurrence (for each). Greater the number, lesser the chance of false positive detection and/or dropping in (inbound) monitored traffic. Also, list is sorted from most (problematic) to least occurent IP addresses.

As an example, to get a fresh and ready-to-deploy auto-ban list of "bad IPs" that appear on at least 3 (black)lists you can run:

```
curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1
```

If you want to try it with `ipset`, you can do the following:

```
sudo su
apt-get -qq install iptables ipset
ipset -q flush ipsum
ipset -q create ipsum hash:net
for ip in $(curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1); do ipset add ipsum $ip; done
iptables -I INPUT -m set --match-set ipsum src -j DROP
```

In directory [levels](levels) you can find preprocessed raw IP lists based on number of blacklist occurrences (e.g. [levels/3.txt](levels/3.txt) holds IP addresses that can be found on 3 or more blacklists).

Wall of shame (2017-04-02)
----

|IP|Number of (black)lists|
|---|--:|
128.52.128.105|10
94.242.246.24|10
176.126.252.12|10
171.25.193.77|10
166.70.207.2|10
37.187.129.166|10
176.10.104.243|9
89.234.157.254|9
65.19.167.130|9
209.222.77.220|9
37.220.35.202|9
64.113.32.29|9
111.40.166.130|9
193.15.16.4|9
185.129.62.63|9
173.254.216.66|9
185.38.14.171|9
176.126.252.11|9
77.247.181.165|9
185.38.14.215|8
178.20.55.18|8
171.25.193.131|8
171.25.193.132|8
78.109.23.1|8
93.115.95.202|8
93.115.95.216|8
197.231.221.211|8
192.36.27.4|8
192.36.27.7|8
192.36.27.6|8
114.255.78.180|8
94.242.246.23|8
46.166.148.176|8
212.83.167.93|8
222.184.79.60|8
176.10.104.240|8
91.197.232.108|8
95.128.43.164|8
178.217.187.39|8
89.248.167.131|8
221.122.101.203|8
46.166.148.177|8
218.60.136.106|8
163.172.73.217|8
192.42.116.16|8
111.40.30.206|8
221.183.16.231|8
93.115.95.201|8
85.248.227.163|8
181.57.149.131|8
58.143.150.109|8
