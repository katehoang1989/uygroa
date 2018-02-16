uygroa - unleash yourself, get rid of ads
=============
Welcome to uygroa, a DNS based ad blocker forked from ublockr. uygroa redirects ad domains to pixelserv-tls webserver.

Requirements
--------------
* SSH/TELNET access
* Router with entware capabilities
* A swap enabled USB drive mounted to the router

Installation
--------------
1. `wget https://raw.githubusercontent.com/Knapoc/uygroa/master/uygroa -O /opt/bin/uygroa --no-check-certificate`
2. `wget https://raw.githubusercontent.com/Knapoc/uygroa/master/uygroa.cfg -O /opt/etc/uygroa.cfg --no-check-certificate`
3. `chmod +x /opt/bin/uygroa`
4. Run it periodically with cron... e.g: 0 0 * * * /opt/bin/uygroa

**NOTE**
* Pixelserv-TLS is installed automatically. It may be necessary to configure it. To do so please refer to the additional resources
* The configuration is done in **/opt/etc/uygroa.cfg**. AsusWRT (not MERLIN) shall configure **other**.
* If you place uygroa.cfg in a different directory, make sure to update the path in uygroa.

Additions to the original ublockr
--------------
* Compatibility with malware-filter (https://gitlab.com/swe_toast/malware-filter) by Toast
* Compatibility with privacy-filter (https://gitlab.com/swe_toast/privacy-filter) by Toast
* Clear cache function
* Update host file sources (listupdate)
* Option to disable whitelists
* Update only, when newer revision is available

Options
--------------
* **-update**

   Updates uygroa if a newer revision is available on github
* **-fupdate**

   Updates uygroa with the latest github version (force update)
* **-version**

   shows version number
* **-fetchall**

   Deletes ip.list, no.list and whitelist.filter and downloads them again from github.
* **-fetchbl**

   Deletes ip.list and no.list and downloads them again from github. These lists contain the various host file sources.
* **-fetchwl**

   Deletes whitelist.filter and downloads it again from github.
* **-clearcache**

   Deletes the content of the cache folder: ip.list, no.list, whitelist.filter, ipv4_hosts, ipv6_hosts
* **-certgen**

   Generates the Root CA Certificates for Pixelserv-TLS. **Requires OPENSSL to be installed**. Certificates are only generated, if ca.crt **AND** ca.key do not exist yet.
* **-certpurge**

   Purges all certificates, which are generated by Pixelserv-TLS. ca.crt and ca.key will not be removed.
Custom filtering
--------------
* **Whitelists**:

   `nano /opt/var/cache/uygroa/whitelist.filter` **Note**: -fetchall & - fetchwl delete your customized whitelist.
* **Sources**:

   `nano /opt/var/cache/uygroa/ip.list` or `nano /opt/var/cache/uygroa/no.list` depending on the layout of the new hostfile: if listed with ip addess, then use ip.list. **Note**: -fetchall & - fetchbl delete your customized host file sources.
* **Personal Blacklist**:

   You can use your own blocklist. Make sure that it follows dnsmasq standards (e.g. `address=/domain.com/<pixelserv-ip>`) and link it in dnsmasq.conf.add (e.g. `conf-file=/mypersonalblocklist.conf`).

Additional resources
--------------
* **Pixelserv-TLS**: https://github.com/kvic-z/pixelserv-tls
* **Entware on AsusWRT (stock)**: https://github.com/Entware-ng/Entware-ng/wiki/Install-on-Asus-stock-firmware
* **Entware on AsusWRT-Merlin**: https://github.com/RMerl/asuswrt-merlin/wiki/Entware
* **Entware on Padavan**: https://bitbucket.org/padavan/rt-n56u/wiki/EN/HowToConfigureEntware
* **Pixelserv-TLS entware configuration**: https://github.com/RMerl/asuswrt-merlin/wiki/How-to-use-Adblock-using-Pixelserv
* **uBlockr on SNB**: https://www.snbforums.com/threads/ublockr-a-minimalists-approach-to-adblocking.31683/
* **Pixelserv-TLS on SNB**: https://www.snbforums.com/threads/pixelserv-a-better-one-pixel-webserver-for-adblock.26114/
* **Purge certificates generated by pixelserv**: https://github.com/kvic-z/pixelserv-tls/wiki/What's-new-in-version-Kj-(v35.HZ12.Kj)

Uninstall uygroa
--------------
1. `rm /opt/bin/uygroa`
2. `rm /opt/etc/uygroa.cfg`
3. `rm -r /opt/var/cache/uygroa/`
4. edit dnsmasq config and remove the entry which links to /opt/var/cache/uygroa/ipv4_hosts (or ipv6_hosts).
5. restart dnsmasq or reboot

**Note**
* This will not uninstall pixelserv-tls. To do so `opkg remove pixelserv-tls`
* To remove all certificates **including the Root CA cert**: `rm /opt/var/cache/pixelserv/*` or (to delete the folder) `rm -r /opt/var/cache/pixelserv/`
