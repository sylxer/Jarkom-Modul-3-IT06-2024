# Laporan-Jarkom-Modul-3-IT06-2024
Praktikum Jaringan Komputer Modul 3 Tahun 2024

## Anggota
| Nama | NRP |
| ----------- | ----------- |
| Sylvia Febrianti | 5027221019 |
| Muhammad Harvian Dito Syahputra | 5027221039 |

# Laporan Resmi
## Topologi
- ![topologi]()

## Config
- Arakis
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.236.1.0
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.236.2.0
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.236.3.0
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 192.236.4.0
	netmask 255.255.255.0
```

## Mohiam
```
auto eth0
iface eth0 inet static
	address 192.236.3.1
	netmask 255.255.255.0
	gateway 192.236.3.0
```

## Irulan
```
auto eth0
iface eth0 inet static
	address 192.236.3.2
	netmask 255.255.255.0
	gateway 192.236.3.0
```

## Chani
```
auto eth0
iface eth0 inet static
	address 192.236.4.1
	netmask 255.255.255.0
	gateway 192.236.4.0
```

## Stilgar
```
auto eth0
iface eth0 inet static
	address 192.236.4.2
	netmask 255.255.255.0
	gateway 192.236.4.0
```

## Leto
```
auto eth0
iface eth0 inet static
	address 192.236.2.3
	netmask 255.255.255.0
	gateway 192.236.2.0
```

## Duncan
```
auto eth0
iface eth0 inet static
	address 192.236.2.2
	netmask 255.255.255.0
	gateway 192.236.2.0
```

## Jessica
```
auto eth0
iface eth0 inet static
	address 192.236.2.1
	netmask 255.255.255.0
	gateway 192.236.2.0
```

## Vladimir
```
auto eth0
iface eth0 inet static
	address 192.236.1.3
	netmask 255.255.255.0
	gateway 192.236.1.0
```

## Rabban
```
auto eth0
iface eth0 inet static
	address 192.236.1.2
	netmask 255.255.255.0
	gateway 192.236.1.0
```

## Feyd
```
auto eth0
iface eth0 inet static
	address 192.236.1.1
	netmask 255.255.255.0
	gateway 192.236.1.0
```

## Client Dmitri & Paul
```
auto eth0
iface eth0 inet dhcp
```

# Sebelum Memulai
setiap node, kita inisiasi pada .bashrc menggunakan nano
## DNS Server
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install bind9 -y  
```

## DHCP Server
```
echo '
nameserver 192.236.3.2
nameserver 192.168.122.1' > /etc/resolv.conf   # Pastikan DNS Server sudah berjalan
apt-get update
apt-get install isc-dhcp-server -y
dhcpd --version

echo INTERFACES="eth0" > /etc/default/isc-dhcp-server
```

## DHCP Relay
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.236.0.0/16
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt install isc-dhcp-relay -y
```

## Database Server
```
echo 'nameserver 192.236.3.2' > /etc/resolv.conf
apt-get update
apt-get install mariadb-server -y
service mysql start

Lalu jangan lupa untuk mengganti [bind-address] pada file /etc/mysql/mariadb.conf.d/50-server.cnf menjadi 0.0.0.0 dan jangan lupa untuk melakukan restart mysql kembali
```

## Load Balancer
```
echo '
nameserver 192.168.122.1
nameserver 192.236.3.2' > /etc/resolv.conf

apt-get update
apt-get install apache2-utils -y
apt-get install nginx -y
apt-get install lynx -y
apt-get install bind9 nginx -y

service nginx start
```

## Worker php
```
echo '
nameserver 192.168.122.1
nameserver 192.236.3.2' > /etc/resolv.conf
apt-get update
apt-get install nginx -y
apt-get install wget -y
apt-get install unzip -y
apt-get install lynx -y
apt-get install htop -y
apt-get install apache2-utils -y
apt-get install php7.3-fpm php7.3-common php7.3-mysql php7.3-gmp php7.3-curl php7.3-intl php7.3-mbstring php7.3-xmlrpc php7.3-gd php7.3-xml php7.3-cli php7.3-zip -y

service nginx start
service php7.3-fpm start
```

##  Worker Laravel
```
echo 'nameserver 192.236.3.2' > /etc/resolv.conf
apt-get update
apt-get install lynx -y
apt-get install mariadb-client -y
# Test connection from worker to database
# mariadb --host=192.236.4.1 --port=3306   --user=kelompoka09 --password=passworda09 dbkelompoka09 -e "SHOW DATABASES;"
apt-get install -y lsb-release ca-certificates apt-transport-https software-properties-common gnupg2
curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
apt-get update
apt-get install php8.0-mbstring php8.0-xml php8.0-cli   php8.0-common php8.0-intl php8.0-opcache php8.0-readline php8.0-mysql php8.0-fpm php8.0-curl unzip wget -y
apt-get install nginx -y

service nginx start
service php8.0-fpm start
```

## client
```
echo '
nameserver 192.236.3.2 # IP irulan
nameserver 192.168.122.1' > /etc/resolv.conf

apt update
apt install lynx -y
apt install htop -y
apt install apache2-utils -y
apt-get install jq -y
apt-get install dnsutils -y
```

# Soal 1
Lakukan konfigurasi sesuai dengan peta yang sudah diberikan.

Langkah yang dilakukan yaitu melakukan konfigurasi pada DNS Server seperti berikut:
### Script Solution
```
echo 'zone "atreides.it06.com" {
        type master;
        file "/etc/bind/jarkom/atreides.it06.com";
};

zone "harkonen.it06.com" {
        type master;
        file "/etc/bind/jarkom/harkonen.it06.com";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     atreides.it06.com. root.atreides.it06.com. (
                        2023111301      ; Serial
                        604800          ; Refresh
                        86400           ; Retry
                        2419200         ; Expire
                        604800 )        ; Negative Cache TTL
;
@               IN      NS      atreides.it06.com.
@               IN      A       192.236.2.3 ; IP Leto Laravel Workerr' > /etc/bind/jarkom/atreides.it06.com

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     harkonen.it06.com.  root.harkonen.it06.com.  (
                        2023111301      ; Serial
                        604800          ; Refresh
                        86400           ; Retry
                        2419200         ; Expire
                        604800 )        ; Negative Cache TTL
;
@               IN      NS      harkonen.it06.com.
@               IN      A       192.236.1.3 ; IP Vladimir PHP Worker' > /etc/bind/jarkom/harkonen.it06.com

echo 'options {
        directory "/var/cache/bind";

        forwarders {
                192.168.122.1;
        };

        // dnssec-validation auto;
        allow-query{any;};
        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
}; ' >/etc/bind/named.conf.options

service bind9 restart
```

### Test Result
ubah setting config pada Client yang semula Dynamic menjadi Static untuk keperluan testing Domain. Contoh pada node paul
```
auto eth0
iface eth0 inet static
	address 192.236.2.4
	netmask 255.255.255.0
	gateway 192.236.2.0
```
