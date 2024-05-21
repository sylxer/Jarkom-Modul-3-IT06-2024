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

```
host -t A atreides.it06.com
host -t A harkonen.it06.com
```
- ![topologi]()
- ![topologi]()

# Soal 2
Client yang melalui House Harkonen mendapatkan range IP dari [prefix IP].1.14 - [prefix IP].1.28 dan [prefix IP].1.49 - [prefix IP].1.70

Langkah yang dilakukan yaitu melakukan konfigurasi pada DHCP Server seperti berikut:
### Script Solution
```
echo 'subnet 192.236.1.0 netmask 255.255.255.0 {
    range 192.236.1.14 192.236.1.28; # range ip untuk client
    range 192.236.1.49 192.236.1.70; # range ip untuk client
    option routers 192.236.1.0; # ip gateway switch1
}' > /etc/dhcp/dhcpd.conf
```

# Soal 3
Client yang melalui House Atreides mendapatkan range IP dari [prefix IP].2.15 - [prefix IP].2.25 dan [prefix IP].2 .200 - [prefix IP].2.210 

Sama seperti Question 2, langkah yang dilakukan adalah dengan menambahkan konfigurasi seperti berikut
### Script Solution
```
echo 'subnet 192.236.1.0 netmask 255.255.255.0 {
    range 192.236.1.14 192.236.1.28; # range ip untuk client
    range 192.236.1.49 192.236.1.70; # range ip untuk client
    option routers 192.236.1.0; # ip gateway switch1
}

subnet 192.236.2.0 netmask 255.255.255.0 {
    range 192.236.2.15 192.236.2.25;
    range 192.236.2.200 192.236.2.210;
    option routers 192.236.2.0;
}' > /etc/dhcp/dhcpd.conf
```

# Soal 4
Client mendapatkan DNS dari Princess Irulan dan dapat terhubung dengan internet melalui DNS tersebut

Agar Domain yang telah dibuat dapat digunakan, perlu menambahkan konfigurasi tambahan option broadcast-address dan option domain-name-servers pada dhcpd.conf
### Script Solution
```
echo 'subnet 192.236.1.0 netmask 255.255.255.0 {
    range 192.236.1.14 192.236.1.28; # range ip untuk client
    range 192.236.1.49 192.236.1.70; # range ip untuk client
    option routers 192.236.1.0; # ip gateway switch1
    option broadcast-address 192.236.1.255; # mirip ip subnet dengan byte terakhir 255
    option domain-name-servers 192.236.3.2; # ip dns server
}

subnet 192.236.2.0 netmask 255.255.255.0 {
    range 192.236.2.15 192.236.2.25;
    range 192.236.2.200 192.236.2.210;
    option routers 192.236.2.0;
    option broadcast-address 192.236.2.255;
    option domain-name-servers 192.236.3.2;
}' > /etc/dhcp/dhcpd.conf
```

# Soal 5
Durasi DHCP server meminjamkan alamat IP kepada Client yang melalui House Harkonen selama 5 menit sedangkan pada client yang melalui House Atreides selama 20 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 87 menit

### Script Solution
Untuk menambahkan durasi waktu dalam peminjaman IP, dibutuhkan konfigurasi tambahan default-lease-time dan max-lease-time pada dhcpd.conf
Melakukan konfigurasi pada DHCP Server seperti berikut:
```
echo 'subnet 192.236.1.0 netmask 255.255.255.0 {
    range 192.236.1.14 192.236.1.28; # range ip untuk client
    range 192.236.1.49 192.236.1.70; # range ip untuk client
    option routers 192.236.1.0; # ip gateway switch1
    option broadcast-address 192.236.1.255; # mirip ip subnet dengan byte terakhir 255
    option domain-name-servers 192.236.3.2; # ip dns server
    default-lease-time 300; # 5 menit
    max-lease-time 5220; # 87 menit
}

subnet 192.236.2.0 netmask 255.255.255.0 {
    range 192.236.2.15 192.236.2.25;
    range 192.236.2.200 192.236.2.210;
    option routers 192.236.2.0;
    option broadcast-address 192.236.2.255;
    option domain-name-servers 192.236.3.2;
    default-lease-time 1200; # 20 menit
    max-lease-time 5220; # 87 menit
}
subnet 192.236.3.0 netmask 255.255.255.0 {
}
subnet 192.236.4.0 netmask 255.255.255.0 {
}' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
service isc-dhcp-server status
```

### Script Solution
melakukan konfigurasi pada Router (DHCP Relay) seperti berikut:
```
echo '
SERVERS="192.236.3.1"
INTERFACES="eth1 eth2 eth3 eth4"
OPTIONS=""' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' > /etc/sysctl.conf

service isc-dhcp-relay restart
```

### Test Result
Jika telah melakukan konfigurasi DHCP Server dan Relay, selanjutnya adalah pembuktian (testing), dilakukan pada Client dengan menjalankan konfigurasi berikut:
Stop Client, Jalankan/Start Client kembali dan jalankan command berikut
```
ip a
```
- ![topologi]()
- ![topologi]()
- ![topologi]()
- ![topologi]()
- ![topologi]()
- ![topologi]()
    
# Soal 6
Vladimir Harkonen memerintahkan setiap worker(harkonen) PHP, untuk melakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3.

### Script Solution
melakukan konfigurasi pada Load Balancer seperti berikut:
```
echo '
 upstream myweb  {
        server 192.236.1.1; #IP Feyd
        server 192.236.1.2; #IP Rabban
        server 192.236.1.3; #IP Vladimir
 }

 server {
        listen 80;
        server_name harkonen.it06.com;

        location / {
        proxy_pass http://myweb;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```

Sebelum mengerjakan perlu untuk melakukan setup terlebih dahulu pada seluruh PHP Worker. Jika sudah, silahkan untuk melakukan konfigurasi tambahan sebagai berikut untuk melakukan download dan unzip menggunakan command wget.
melakukan konfigurasi pada PHP Worker seperti berikut:
```
mkdir -p /var/www/harkonen.it06

wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=1lmnXJUbyx1JDt2OA5z_1dEowxozfkn30' -O /var/www/harkonen.it06.zip
unzip /var/www/harkonen.it06.zip -d /var/www/harkonen.it06
mv /var/www/harkonen.it06/modul-3 /var/www/harkonen.it06
rm -rf /var/www/harkonen.it06.zip

echo '
server {

        listen 80;

        root /var/www/harkonen.it06;

        index index.php index.html index.htm;
        server_name _;

        location / {
                        try_files $uri $uri/ /index.php?$query_string;
        }

        # pass PHP scripts to FastCGI server
        location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.3-fpm.sock;
        }

location ~ /\.ht {
                        deny all;
        }

        error_log /var/log/nginx/jarkom_error.log;
        access_log /var/log/nginx/jarkom_access.log;
 }' > /etc/nginx/sites-available/harkonen.it06

echo '<!DOCTYPE html>
<html>
<head>
    <title>harkonen Map</title>
    <link rel="stylesheet" type="text/css" href="css/styles.css">
</head>
<body>
    <div class="container">
        <h1>Welcome to harkonen</h1>
        <p><?php
            $hostname = gethostname();
            echo "Request ini dihandle oleh: $hostname<br>"; ?> </p>
        <p>Enter your name to validate:</p>
        <form method="POST" action="index.php">
            <input type="text" name="name" id="nameInput">
            <button type="submit" id="submitButton">Submit</button>
        </form>
        <p id="greeting"><?php
            if(isset($_POST['name'])) {
                $name = $_POST['name'];
                echo "Hello, $name!";
            }
        ?></p>
    </div>

    <script src="js/script.js"></script>
</body>' > /var/www/harkonen.it06/index.php

ln -s /etc/nginx/sites-available/harkonen.it06 /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service php7.3-fpm start
service php7.3-fpm restart
service nginx restart
nginx -t
```

melakukan konfigurasi pada DNS Server seperti berikut:
```
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
@               IN      A       192.236.4.2 ; IP Stilgar Load Balancer' > /etc/bind/jarkom/harkonen.it06.com

service bind9 restart
```

### Test Result
```
lynx harkonen.it06.com
```
- ![topologi]()
- ![topologi]()
- ![topologi]()
  
# Soal 7
Aturlah agar Stilgar dari fremen dapat dapat bekerja sama dengan maksimal, lalu lakukan testing dengan 5000 request dan 150 request/second. 

```
ab -n 5000 -c 150 http://harkonen.it06.com/
```
Ketika request berhasil dijalankan maka hasilnya seperti berikut:

### Test Result
```
lynx harkonen.it06.com
```
- ![topologi]()
- ![topologi]()


# Soal 8
Karena diminta untuk menuliskan peta tercepat menuju spice, buatlah analisis hasil testing dengan 500 request dan 50 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
- Nama Algoritma Load Balancer
- Report hasil testing pada Apache Benchmark
- Grafik request per second untuk masing masing algoritma. 
- Analisis

Request command yang dijalankan pada Client (setelah menjalankan konfigurasi Algoritma)
```
ab -n 500 -c 50 http://harkonen.it06.com/
```
Untuk hasil analisis dapat dilihat pada file IT06_Spice.pdf

Algoritma Round-Robin
```
apt-get install bind9 nginx -y

echo '
 upstream myweb  {
        server 192.236.1.1; #IP Feyd
        server 192.236.1.2; #IP Rabban
        server 192.236.1.3; #IP Vladimir
 }

 server {
        listen 80;
        server_name harkonen.it06.com;

        location / {
        proxy_pass http://myweb;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```
- ![topologi]()

Algoritma Weighted Round-Robin
```
echo '
 upstream myweb  {
        server 192.236.1.1; #IP Feyd
        server 192.236.1.2; #IP Rabban
        server 192.236.1.3; #IP Vladimir
 }

 server {
        listen 80;
        server_name harkonen.it06.com;

        location / {
        proxy_pass http://myweb;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

unlink /etc/nginx/sites-enabled/lb-jarkom
ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```
- ![topologi]()

Algoritma Least Connection
```
echo '
 upstream myweb  {
        server 192.236.1.1; #IP Feyd
        server 192.236.1.2; #IP Rabban
        server 192.236.1.3; #IP Vladimir
 }

 server {
        listen 80;
        server_name harkonen.it06.com;

        location / {
        proxy_pass http://myweb;
        proxy_set_header    X-Real-IP $remote_addr;
        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header    Host $http_host;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```
- ![topologi]()

Algoritma IP Hash
```
echo '
 upstream myweb  {
        ip_hash;
        server 192.236.1.1; #IP Feyd
        server 192.236.1.2; #IP Rabban
        server 192.236.1.3; #IP Vladimir
 }

 server {
        listen 80;
        server_name harkonen.it06.com;

        location / {
        proxy_pass http://myweb;
        proxy_set_header    X-Real-IP $remote_addr;
        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header    Host $http_host;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```
- ![topologi]()

Algoritma Generic Hash
```
echo '
 upstream myweb  {
        hash $request_uri consistent;
        server 192.236.1.1; #IP Feyd
        server 192.236.1.2; #IP Rabban
        server 192.236.1.3; #IP Vladimir
 }

 server {
        listen 80;
        server_name harkonen.it06.com;

        location / {
        proxy_pass http://myweb;
        proxy_set_header    X-Real-IP $remote_addr;
        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header    Host $http_host;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

unlink /etc/nginx/sites-enabled/lb-jarkom
ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```
- ![topologi]()

Grafik
- ![topologi]()

# Soal 9
Dengan menggunakan algoritma Least-Connection, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 1000 request dengan 10 request/second, kemudian tambahkan grafiknya pada peta.

```
echo '
 upstream myweb  {
        server 192.236.1.1; #IP Feyd
        server 192.236.1.2; #IP Rabban
        server 192.236.1.3; #IP Vladimir
 }

 server {
        listen 80;
        server_name harkonen.it06.com;

        location / {
        proxy_pass http://myweb;
        proxy_set_header    X-Real-IP $remote_addr;
        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header    Host $http_host;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```

Request command pada Client:
```
ab -n 1000 -c 10 http://harkonen.it06.com/
```

- 3 Worker
  ```
  3 Worker: 757.29 [#/sec]
  ```
- 2 Worker
  ```
  2 Worker: 799.75 [#/sec]
  ```
- 1 Worker
  ```
  1 Worker: 867.98 [#/sec]
  ```

Grafik

# Soal 10
Selanjutnya coba tambahkan keamanan dengan konfigurasi autentikasi di LB dengan dengan kombinasi username: “secmart” dan password: “kcksyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/supersecret/

Sebelum mengerjakan perlu untuk melakukan setup terlebih dahulu. Setelah itu, lakukan beberapa konfigurasi /etc/nginx/supersecret/ sebagai berikut 
```
mkdir -p /etc/nginx/supersecret/
htpasswd -c -b /etc/nginx/supersecret/.htpasswd secmart kcksit06

echo '
 upstream myweb  {
        server 192.236.1.1; #IP Feyd
        server 192.236.1.2; #IP Rabban
        server 192.236.1.3; #IP Vladimir
 }

 server {
        listen 80;
        server_name harkonen.it06.com;

        location / {
        proxy_pass http://myweb;
        auth_basic "Restricted Access";
        auth_basic_user_file /etc/nginx/supersecret/.htpasswd;
        }
 }' > /etc/nginx/sites-available/lb-jarkom

unlink /etc/nginx/sites-enabled/lb-jarkom
ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```

### Test Result
Alert saat pertama kali membuka Website
- ![topologi]()
Tampilan ketika diperintahkan untuk memasukkan Username
- ![topologi]()
Tampilan ketika diperintahkan untuk memasukkan Password 
- ![topologi]()
Hasil ketika berhasil memasukkan Username dan Password dengan benar  
- ![topologi]()

# Soal 11

Lalu buat untuk setiap request yang mengandung /dune akan di proxy passing menuju halaman https://www.dunemovie.com.au/. (11) hint: (proxy_pass)

## Stilgar

Dilakukan konfigurasi pada Load Balancer Stilgar untuk mengarahkan endpoint /dune ke https://www.dunemovie.com.au/ dengan menggunakan proxy pass.

```
echo '
upstream myweb  {
        server 192.236.1.1; #IP Feyd
        server 192.236.1.2; #IP Rabban
        server 192.236.1.3; #IP Vladimir
}

server {
        listen 80;
        server_name harkonen.it06.com;

        location / {
        proxy_pass http://myweb;
        auth_basic "Restricted Access";
        auth_basic_user_file /etc/nginx/supersecret/.htpasswd;
        }

        location /dune {
        proxy_pass https://www.dunemovie.com.au/;
        proxy_set_header Host www.dunemovie.com.au;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        }

}' > /etc/nginx/sites-available/lb-jarkom

unlink /etc/nginx/sites-enabled/lb-jarkom
ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```

## Testing
Dilakukan lynx harkonen.it06.com/dune pada client
![Screenshot 2024-05-17 211732](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/8927ee77-e4b0-497d-8683-d6d1be9fab2b)

# Soal 12

Selanjutnya LB ini hanya boleh diakses oleh client dengan IP [Prefix IP].1.37, [Prefix IP].1.67, [Prefix IP].2.203, dan [Prefix IP].2.207. (12) hint: (fixed in dulu clientnya)

## Stilgar

Dilakukan konfigurasi untuk melakukan allow kepada IP-IP tersebut dan deny pada IP lainnya.

```
echo '
upstream myweb  {
        server 192.236.1.1; #IP Feyd
        server 192.236.1.2; #IP Rabban
        server 192.236.1.3; #IP Vladimir
}

server {
        listen 80;
        server_name harkonen.it06.com;

        location / {
        allow 192.236.1.37;
        allow 192.236.1.67;
        allow 192.236.2.203;
        allow 192.236.2.207;
        deny all;

        proxy_pass http://myweb;
        auth_basic "Restricted Access";
        auth_basic_user_file /etc/nginx/supersecret/.htpasswd;
        }

        location /dune {
        proxy_pass https://www.dunemovie.com.au/;
        proxy_set_header Host www.dunemovie.com.au;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        }

}' > /etc/nginx/sites-available/lb-jarkom

unlink /etc/nginx/sites-enabled/lb-jarkom
ln -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
rm -rf /etc/nginx/sites-enabled/default

service nginx restart
nginx -t
```

## Testing
Dilakukan lynx harkonen.it06.com pada client. Berikut adalah hasil ketika IP yang sedang mengakses harkonen.it06.com bukan IP yang diperbolehkan mengakses web server.

![Screenshot 2024-05-17 211929](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/861bdf33-2ec8-41e3-903e-6c3037ef16ea)

Diperlukan allow IP client jika ingin melihat hasil ketika IP diperbolehkan mengakses web server dengan menambahkan "allow [IP];" pada konfigurasi Load Balancer. Berikut adalah hasil ketika IP diperbolehkan mengakses web server.

![Screenshot 2024-05-17 212751](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/86120aef-d843-4c9a-8ed7-1daaf60651ec)

# Soal 13

Semua data yang diperlukan, diatur pada Chani dan harus dapat diakses oleh Leto, Duncan, dan Jessica. (13)

## Chani

Dilakukan pembuatan user dan database pada CHANI dengan script berikut.

```
mysql -u root -p <<EOF
CREATE USER 'kelompokit06'@'%' IDENTIFIED BY 'passwordit06';
CREATE USER 'kelompokit06'@'localhost' IDENTIFIED BY 'passwordit06';
CREATE DATABASE dbkelompokit06;
GRANT ALL PRIVILEGES ON *.* TO 'kelompokit06'@'%';
GRANT ALL PRIVILEGES ON *.* TO 'kelompokit06'@'localhost';
FLUSH PRIVILEGES;
quit
EOF

mysql -u kelompokit06 -p'passwordit06' <<EOF
SHOW DATABASES;
quit
EOF
```

Kemudian dibuat konfigurasi pada /etc/mysql/my.cnf sebagai berikut.

```
echo "
[client-server]

!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mariadb.conf.d/

[mysqld]
skip-networking=0
skip-bind-address" > /etc/mysql/my.cnf

service mysql restart
```

## Testing
Dilakukan perintah sheel “mariadb --host=192.236.4.1 --port=3306 --user=kelompokit06 --password=passwordit06” di salah satu laravel worker. Kemudian lakukan “SHOW DATABASES;”.

![Screenshot 2024-05-18 084812](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/3775b2ce-b495-46ac-9bc3-749216115c14)

# Soal 14

Leto, Duncan, dan Jessica memiliki atreides Channel sesuai dengan quest guide berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer (14)

## Laravel Worker

Pertama, dilakukan instalasi requirements untuk melakukan konfigurasi web server sesuai soal.

```
apt-get update
apt-get install -y lsb-release ca-certificates apt-transport-https software-properties-common gnupg2

curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg

sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
apt-get update

apt-get install php8.0-mbstring php8.0-xml php8.0-cli php8.0-common php8.0-intl php8.0-opcache php8.0-readline php8.0-mysql php8.0-fpm php8.0-curl unzip wget -y
apt-get install nginx -y

wget https://getcomposer.org/download/2.0.13/composer.phar
chmod +x composer.phar
mv composer.phar /usr/bin/composer

apt-get install git -y

cd /var/www
git clone https://github.com/martuafernando/laravel-praktikum-jarkom.git
cd /var/www/laravel-praktikum-jarkom
cp .env.example .env
```

Kemudian, dilakukan konfigurasi environment pada laravel-praktikum-jarkom.

```
echo 'APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=192.236.4.1
DB_PORT=3306
DB_DATABASE=dbkelompokit06
DB_USERNAME=kelompokit06
DB_PASSWORD=passwordit06

BROADCAST_DRIVER=log
CACHE_DRIVER=file
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=mt1

VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
VITE_PUSHER_HOST="${PUSHER_HOST}"
VITE_PUSHER_PORT="${PUSHER_PORT}"
VITE_PUSHER_SCHEME="${PUSHER_SCHEME}"  
VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"' > /var/www/laravel-praktikum-jarkom/.env

cd /var/www/laravel-praktikum-jarkom && composer update && composer install

cd /var/www/laravel-praktikum-jarkom && php artisan key:generate
cd /var/www/laravel-praktikum-jarkom && php artisan config:cache
cd /var/www/laravel-praktikum-jarkom && php artisan migrate
cd /var/www/laravel-praktikum-jarkom && php artisan db:seed
cd /var/www/laravel-praktikum-jarkom && php artisan storage:link
cd /var/www/laravel-praktikum-jarkom && php artisan jwt:secret
cd /var/www/laravel-praktikum-jarkom && php artisan config:clear
```

Setelah itu dilakukan konfigurasi web server nginx pada laravel worker.

```
echo 'server {
    listen 800x;

    root /var/www/laravel-praktikum-jarkom/public;

    index index.php index.html index.htm;
    server_name _;

    location / {
            try_files $uri $uri/ /index.php?$query_string;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
      include snippets/fastcgi-php.conf;
      fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
    }

    location ~ /\.ht {
            deny all;
    }

    error_log /var/log/nginx/implementasi_error.log;
    access_log /var/log/nginx/implementasi_access.log;
}' > /etc/nginx/sites-available/laravel-worker

ln -s /etc/nginx/sites-available/laravel-worker /etc/nginx/sites-enabled/

chown -R www-data.www-data /var/www/laravel-parktikum-jarkom/storage

service nginx start
service php8.0-fpm start
```

notes: pada bagian "listen 800x" dengan x adalah pilihan port pada masing-masing worker, misal 8001, 8002, dst.

## Testing
Dilakukan lynx localhost:[PORT] di worker. [PORT] di sini merupakan port yang digunakan pada masing-masing worker.

![Screenshot 2024-05-18 210814](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/9f90f0e2-aa7e-4368-9277-418be9229045)

# Soal 15

atreides Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada peta.
POST /auth/register (15)

## Client

Dilakukan pembuatan script untuk memanfaatkan json sebagai file untuk register.

```
echo '
{
  "username": "kelompokit06",
  "password": "passwordit06"
}' > register.json
```

## Testing
Dilakukan perintah shell berikut. Percobaan dilakukan ke salah satu worker (di sini mengarah ke worker Leto).

```
ab -n 100 -c 10 -p register.json -T application/json http://192.236.2.3:8001/api/auth/register
```
![Screenshot 2024-05-18 211336](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/6d0fc8d1-c051-40cb-b918-6bef7361e948)

# Soal 16

atreides Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada peta.
POST /auth/login (16)

## Client

Dilakukan pembuatan script untuk memanfaatkan json sebagai file untuk login.

```
echo '
{
  "username": "kelompokit06",
  "password": "passwordit06"
}' > login.json
```

## Testing
Dilakukan perintah shell berikut. Percobaan dilakukan ke salah satu worker (di sini mengarah ke worker Leto).

```
ab -n 100 -c 10 -p login.json -T application/json http://192.236.2.3:8001/api/auth/login
```
![Screenshot 2024-05-18 211848](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/8be3362c-654d-4838-8de0-8cf30fa85451)

# Soal 17

atreides Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada peta.
GET /me (17)

## Client

Dilakukan pembuatan script untuk memanfaatkan json sebagai file untuk get endpoint /me.

```
curl -X POST -H "Content-Type: application/json" -d @login.json http://192.236.2.3:8001/api/auth/login > login_output.txt

token=$(cat login_output.txt | jq -r '.token')
```

## Testing
Dilakukan perintah shell berikut. Percobaan dilakukan ke salah satu worker (di sini mengarah ke worker Leto).

```
ab -n 100 -c 10 -H "Authorization: Bearer $token" http://192.236.2.3:8001/api/me
```
![Screenshot 2024-05-18 215032](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/9abed29e-c9a1-46fd-9124-e43e24b42456)

# Soal 18

Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur atreides Channel maka implementasikan Proxy Bind pada Stilgar untuk mengaitkan IP dari Leto, Duncan, dan Jessica. (18)

## Irulan

Dilakukan konfigurasi pada DNS server atreides.it06.com yang sebelumnya mengarah ke Leto diubah menjadi mengarah ke Stilgar.

```
echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     atreides.it06.com.  root.atreides.it06.com.  (
                        2023111302      ; Serial
                        604800          ; Refresh
                        86400           ; Retry
                        2419200         ; Expire
                        604800 )        ; Negative Cache TTL
;
@               IN      NS      atreides.it06.com.
@               IN      A       192.236.4.2 ; IP Stilgar Load Balancer' > /etc/bind/jarkom/atreides.it06.com

service bind9 restart
```

## Stilgar

Dilakukan konfigurasi pembuatan Load Balancer untuk house atreides.

```
echo 'upstream worker {
    server 192.236.2.3:8001; # IP Leto
    server 192.236.2.2:8002; # IP Duncan
    server 192.236.2.1:8003; # IP Jessica
}

server {
    listen 80;
    server_name atreides.it06.com;

    location / {
        proxy_pass http://worker;
    }
}
' > /etc/nginx/sites-available/laravel-worker

ln -s /etc/nginx/sites-available/laravel-worker /etc/nginx/sites-enabled/laravel-worker

service nginx restart
```
## Testing
Dilakukan perintah shell "ab -n 100 -c 10 -p login.json -T application/json http://atreides.it06.com/api/auth/login" di client

![Screenshot 2024-05-18 231959](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/c68353d3-cd2a-4f9a-b53e-9d44f001f283)

Dilakukan perintah shell berikut "cat /var/log/nginx/implementasi_access.log" pada masing-masing worker untuk mengetahui log yang mengakses masing-masing worker.

- Leto
![Screenshot 2024-05-18 232252](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/2b27522d-644e-47fc-8dcb-df3cc393b890)
- Duncan
![Screenshot 2024-05-18 232231](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/9fb49957-f3c0-4f9f-91b0-13c56215ecb5)
- Jessica
![Screenshot 2024-05-18 232333](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/9304c2fb-1989-47ff-817f-a4d818afb99c)

# Soal 19

Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada Leto, Duncan, dan Jessica. Untuk testing kinerja naikkan 
- pm.max_children
- pm.start_servers
- pm.min_spare_servers
- pm.max_spare_servers
sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second kemudian berikan hasil analisisnya pada PDF.(19)

## Laravel Worker

Dilakukan pembuatan beberapa script untuk masing-masing konfigurasi implementasi PHP-FPM. Setiap konfigurasi memiliki tingkatan setting yang berbeda.

#### Konfigurasi Pertama
```
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 5
pm.start_servers = 2
pm.min_spare_servers = 1
pm.max_spare_servers = 3' > /etc/php/8.0/fpm/pool.d/www.conf

service php8.0-fpm restart
```

#### Konfigurasi Kedua
```
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 25
pm.start_servers = 5
pm.min_spare_servers = 3
pm.max_spare_servers = 10' > /etc/php/8.0/fpm/pool.d/www.conf

service php8.0-fpm restart
```

#### Konfigurasi Ketiga
```
echo '[www]
user = www-data
group = www-data
listen = /run/php/php8.0-fpm.sock
listen.owner = www-data
listen.group = www-data
php_admin_value[disable_functions] = exec,passthru,shell_exec,system
php_admin_flag[allow_url_fopen] = off

; Choose how the process manager will control the number of child processes.

pm = dynamic
pm.max_children = 50
pm.start_servers = 8
pm.min_spare_servers = 5
pm.max_spare_servers = 15' > /etc/php/8.0/fpm/pool.d/www.conf

service php8.0-fpm restart
```

## Testing
Dilakukan perintah shell "ab -n 100 -c 10 -p login.json -T application/json http://atreides.it06.com/api/auth/login" di client pada setiap konfigurasi

#### Konfigurasi Pertama
![Screenshot 2024-05-19 123929](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/f1f91732-7220-403a-9619-3d9c89130027)
![Screenshot 2024-05-19 123851](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/27ff8c65-8c0f-4c66-986d-ded265cf80f0)

#### Konfigurasi Kedua
![Screenshot 2024-05-19 124212](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/76b3e97b-c4f6-446e-9088-10a863f960a7)
![Screenshot 2024-05-19 124143](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/239ca6cd-2996-4ad6-9b34-bc55d2c4df38)

#### Konfigurasi Ketiga
![Screenshot 2024-05-19 125553](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/d0613a93-6080-4c65-9269-c7a52c7667d7)
![Screenshot 2024-05-19 124830](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/1895da11-007c-45d3-83ae-55742d5a5cd2)

# Soal 20

Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Stilgar. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second. (20)

## Stilgar

Dilakukan konfigurasi ulang Load Balancer untuk mengubah algoritma Load Balaner yang digunakan menjadi least-conn.

```
echo 'upstream worker {
    least_conn;
    server 192.236.2.3:8001; # IP Leto
    server 192.236.2.2:8002; # IP Duncan
    server 192.236.2.1:8003; # IP Jessica
}

server {
    listen 80;
    server_name atreides.it06.com;

    location / {
        proxy_pass http://worker;
    }
}
' > /etc/nginx/sites-available/laravel-worker

ln -s /etc/nginx/sites-available/laravel-worker /etc/nginx/sites-enabled/laravel-worker

service nginx restart
```

## Testing
Dilakukan perintah shell "ab -n 100 -c 10 -p login.json -T application/json http://atreides.it06.com/api/auth/login" di client.

![Screenshot 2024-05-19 122234](https://github.com/sylxer/Jarkom-Modul-3-IT06-2024/assets/115382618/3502e842-edd8-42ac-a5d0-14844b50f8c1)
