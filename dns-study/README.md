#### Packages
```
dpkg -L bind9
```

#### Version Info
```
named -v
```

#### Detailed Info
```
named -V
```

```
/etc/bind# sudo -u bind cat rndc.key
key "rndc-key" {
    algorithm hmac-md5;
    secret "";
};
```

#### Zone Files

DNS information is stored in a text file called Zones. BIND can auto-create entries with
$GENERATE


#### LOCALHOST

```
root@b242be2b6ff8:/etc/bind# cat db.local
;
; BIND data file for local loopback interface
;
$TTL    604800
@    IN    SOA    localhost. root.localhost. (
                  2        ; Serial
             604800        ; Refresh
              86400        ; Retry
            2419200        ; Expire
             604800 )    ; Negative Cache TTL
;
@    IN    NS    localhost.
@    IN    A    127.0.0.1
@    IN    AAAA    ::1
```

#### REVERSE LOOKUP (PTR records)

```
root@b242be2b6ff8:/etc/bind# cat db.127
;
; BIND reverse data file for local loopback interface
;
$TTL    604800
@    IN    SOA    localhost. root.localhost. (
                  1        ; Serial
             604800        ; Refresh
              86400        ; Retry
            2419200        ; Expire
             604800 )    ; Negative Cache TTL
;
@    IN    NS    localhost.
1.0.0    IN    PTR    localhost.
```

#### Knowing IP that accessed a service is one thing but knowing host is better.

```
$GENERATE 10-254 $ PTR dhcp-$.example.com
```

#### Zone files
```
root@b242be2b6ff8:/etc/bind# ls db*
db.0  db.127  db.255  db.empty  db.local  db.root
```

```
cat db.local
;
; BIND data file for local loopback interface
;
//START OF AUTHORITY RECORD SPECIFYING WHO LOOKS AFTER THIS ZONE
$TTL    604800
@    IN    SOA    localhost. root.localhost. (
                  2        ; Serial
             604800        ; Refresh
              86400        ; Retry
            2419200        ; Expire
             604800 )    ; Negative Cache TTL
;
// NAMESERVER - MASTER, SLAVE SERVERS
@    IN    NS    localhost.
// ADDRESS RECORDS
// IPV4 ADDRESS
@    IN    A    127.0.0.1
// IPV6 ADDRESS
@    IN    AAAA    ::1
```

#### Reference to Local Zone
```
root@b242be2b6ff8:/etc/bind# grep local named.conf.default-zones
// be authoritative for the localhost forward and reverse zones, and for
zone "localhost" {
    file "/etc/bind/db.local";
    
```

#### chroot jail
- Chroot Jail can protect against malicious attacks.
- The directory named runs from appears as the root of the filesystem

#### Bind9 File

```
root@a4e38c1ccf7d:/# cat /etc/default/bind9
#
# run resolvconf?
RESOLVCONF=no

# startup options for the server
OPTIONS="-u bind"
```

- RESOLVCONF: Do we want to use the client file as our forwarder (disabled by default)
- OPTIONS: Startup options

#### Controlling Named Daemon (Command rndc is used to control named service)

```
root@a4e38c1ccf7d:/# sudo -u bind rndc status
version: BIND 9.11.3-1ubuntu1.3-Ubuntu (Extended Support Version) <id:a375815>
running on a4e38c1ccf7d: Linux x86_64 4.9.87-linuxkit-aufs #1 SMP Wed Mar 14 15:12:16 UTC 2018
boot time: Mon, 19 Nov 2018 21:22:29 GMT
last configured: Mon, 19 Nov 2018 21:22:29 GMT
configuration file: /etc/bind/named.conf
CPUs found: 2
worker threads: 2
UDP listeners per interface: 1
number of zones: 101 (96 automatic)
debug level: 0
xfers running: 0
xfers deferred: 0
soa queries in progress: 0
query logging is OFF
recursive clients: 0/900/1000
tcp clients: 0/150
server is up and running
```

#### Allow access from other hosts

rndc-confgen
```
# Start of rndc.conf
key "rndc-key" {
    algorithm hmac-md5;
    secret "qUSpZU1Grpq3bUukNnxchA==";
};

options {
    default-key "rndc-key";
    default-server 127.0.0.1;
    default-port 953;
};
# End of rndc.conf

# Use with the following in named.conf, adjusting the allow list as needed:
# key "rndc-key" {
#     algorithm hmac-md5;
#     secret "qUSpZU1Grpq3bUukNnxchA==";
# };
#
# controls {
#     inet 127.0.0.1 port 953
#         allow { 127.0.0.1; } keys { "rndc-key"; };
# };
# End of named.conf
```

#### Service Status

```
sudo service bind9 status
 * bind9 is running
```

```
root@a4e38c1ccf7d:/# sudo -u bind rndc status
version: BIND 9.11.3-1ubuntu1.3-Ubuntu (Extended Support Version) <id:a375815>
running on a4e38c1ccf7d: Linux x86_64 4.9.87-linuxkit-aufs #1 SMP Wed Mar 14 15:12:16 UTC 2018
boot time: Mon, 19 Nov 2018 21:22:29 GMT
last configured: Mon, 19 Nov 2018 21:22:29 GMT
configuration file: /etc/bind/named.conf
CPUs found: 2
worker threads: 2
UDP listeners per interface: 1
number of zones: 101 (96 automatic)
debug level: 0
xfers running: 0
xfers deferred: 0
soa queries in progress: 0
query logging is OFF
recursive clients: 0/900/1000
tcp clients: 0/150
server is up and running
```

#### Syntax checks

```
root@a4e38c1ccf7d:/# sudo named-checkconf
root@a4e38c1ccf7d:/# sudo named-checkzone localhost /etc/bind/db.local
zone localhost/IN: loaded serial 2
OK
```

#### Dnsutils (Tools)
This includes dig and nslookup

```
root@a4e38c1ccf7d:/# dig www.pluralsight.com -t A

; <<>> DiG 9.11.3-1ubuntu1.3-Ubuntu <<>> www.pluralsight.com -t A
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 6724
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;www.pluralsight.com.        IN    A

;; ANSWER SECTION:
www.pluralsight.com.    38    IN    A    54.213.33.102
www.pluralsight.com.    38    IN    A    52.42.57.72
www.pluralsight.com.    38    IN    A    52.43.133.199

;; Query time: 144 msec
;; SERVER: 192.168.65.1#53(192.168.65.1)
;; WHEN: Mon Nov 19 21:53:14 UTC 2018
;; MSG SIZE  rcvd: 85

root@a4e38c1ccf7d:/# nslookup -query=A www.pluralsight.com
Server:        192.168.65.1
Address:    192.168.65.1#53

Non-authoritative answer:
Name:    www.pluralsight.com
Address: 54.213.33.102
Name:    www.pluralsight.com
Address: 52.42.57.72
Name:    www.pluralsight.com
Address: 52.43.133.199
```

#### dig with and without bind
@127.0.0.1 is bind
```
root@a4e38c1ccf7d:/# dig -t A www.pluralsight.com @127.0.0.1
root@a4e38c1ccf7d:/# dig -t A www.pluralsight.com
```
