Check disks SMART status and temperature for Nagios 
===================================================

This program implements a checking SMART status and temperature for Nagios, uses smartmontools. 
Initially based on utility check_smart. That two times not to rise, deduces temperature in a collectd format 
Designed by Phil Kulin for http://diphost.ru/ at year 2012 

DESCRIPTION
-----------
 
check_smart3 parse smartd daemon (from smartmontools) output and create report for nagios. 
That two times not to rise, deduces temperature in a collectd format too. 
 
The majority of similar tools parse monstrous smartctl output. Also smartctl 
demands separate exec on each disk. So smartd output more clean and simple. 
One of ideas of the check_smart3 consists that we don't need separate nagios alerts on 
problems of each disk. I consider all disks as one destruction point. But certainly 
check_smart3 can be used and for checks each disk separately. 
 
EXAMPLES 
--------
 
Nagios check: 
> check_smart3 -n -w 50 -c 55 
 
Collecting temperature with collectd: 
> check_smart3 -l 600,, | nc -U /var/run/collectd-unixsock 
 
crontab line for collecting temperature with collectd: 
> */5 * * * * /usr/bin/lockf -s -t 0 /var/run/check_smart3.lock /usr/local/sbin/check_smart3 -l 600,, | /usr/bin/nc -U /var/run/collectd-unixsock > /dev/null 
 
DONATE
------

For coffee and nuts
* Yandex.Money: 41001140237324
* PayPal: schors@gmail.com

--
[![LICENSE WTFPL](wtfpl-badge-1.png)](LICENSE)

