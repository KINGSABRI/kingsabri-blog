# How to Register Your Own Custom DNS Server for C2 and Data exfiltration

Skipping all DNS protocol, DNS tunneling and DNS data exfiltration. I've got a custom-built DNS server for a C2 and data exfiltration and I needed to add my nameservers to my domain provider.

### Step \#1 \| Setup your DNS Server

Whether you're going to use bind9 or a programmable server that you have coded \(e.g. [RubyDNS](https://github.com/socketry/rubydns/)\), all what you need is to add the records you want to serve. Explaining how to configure your own DNS is beyond this topic.

### Step \#2 \| Register Your NameServer

#### Register the NameServer

1. Click on the **MY DOMAINS** button, located on the top right hand corner.
2. Click the domain name you would like to manage.
3. Click **NS Registration** on the left side.
4. In the **Hostname** field, enter a prefix, such as **NS1**. In the **IP Address** field, enter the IP address that you need the nameserver to point to.
5. Click the **Register New Nameserver** button

#### Add Nameserver to the nameservers list

1. Click on the **My Domains** button, located on the top right hand corner.
2. Click the domain name you would like to manage.
3. Click **Nameservers** on the left side.
4. Click the **Delete All** button to clear the current nameservers away.  Alternatively, you can also Delete them one-by-one by clicking **Delete**, on the right-hand side. \(_If you do not delete the old nameservers before adding the new, it will create conflicts and the associated website/email will not work._\)
5. Enter the new nameserver in the empty box labeled **Add Nameserver** and then click the blue **Add** button. Be sure to only add one at a time. \(_You will need at least two nameservers for the domain to work_\)
6. Click **Apply Changes**.

### Step \#3 \| Test your Infrastructure

The best application for troubleshooting is `dnstracer` command which is available on Kali by default or you can install it using `apt install dnstracer` . Then run it as follows

```text
$ dnstracer -c4o sub.domain.com
```

Another helpful dig checks are

```text
$ dig sub.domain.com +short
$ dig TXT sub.domain.com +short
```

## **Resources**

* [Registering custom nameservers](https://www.name.com/support/articles/205934457-Registering-custom-nameservers)
* [Changing nameservers for DNS management](https://www.name.com/support/articles/205934547-Changing-nameservers-for-DNS-management?keyword=name%20servers)
* [Fun with DNS TXT Records and PowerShell](http://www.labofapenetrationtester.com/2015/01/fun-with-dns-txt-records-and-powershell.html)

