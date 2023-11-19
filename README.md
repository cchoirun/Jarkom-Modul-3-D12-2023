# Jarkom-Modul-3-D12-2023
Laporan Resmi Modul Jarkom 3 D12 2023
|Nama|NRP|
|-----|-----|
|Muhammad Revel Wivanto|5025211233|
|Muhammad Choirun Ni'am|5025221203|

<img width="466" alt="peta_topologi" src="https://github.com/cchoirun/Jarkom-Modul-2-D12-2023/assets/115228631/d83b9271-9419-471c-bf01-a6ec1aec0fbc">

Pertama-tama, kita akan membuat konfigurasi sesuai topologi yang diberikan : 
link github:
### https://github.com/cchoirun/Jarkom-Modul-3-D12-2023

### Aura
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.197.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.197.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.197.3.1
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 192.197.4.1
	netmask 255.255.255.0
```

### Himmel
```
auto eth0
iface eth0 inet static
	address 192.197.1.2
	netmask 255.255.255.0
	gateway 192.197.1.1
```

### Heiter
```
auto eth0
iface eth0 inet static
	address 192.197.1.3
	netmask 255.255.255.0
	gateway 192.197.1.1
```

### Denken
```
auto eth0
iface eth0 inet static
	address 192.197.2.2
	netmask 255.255.255.0
	gateway 192.197.2.1
```

### Eisen
```
auto eth0
iface eth0 inet static
	address 192.197.2.3
	netmask 255.255.255.0
	gateway 192.197.2.1
```

### Revolte
```
auto eth0
iface eth0 inet dhcp
```

### Richter
```
auto eth0
iface eth0 inet dhcp
```
### Lawine
```
auto eth0
iface eth0 inet static
	address 192.197.4.4
	netmask 255.255.255.0
	gateway 192.197.3.1
```

### Linie
```
auto eth0
iface eth0 inet static
	address 192.197.3.5
	netmask 255.255.255.0
	gateway 192.197.3.1
```

### Lugner
```
auto eth0
iface eth0 inet static
	address 192.197.3.6
	netmask 255.255.255.0
	gateway 192.197.3.1
```

### Sein
```
auto eth0
iface eth0 inet dhcp
```

### Stark
```
auto eth0
iface eth0 inet dhcp
```

### Frieren
```
auto eth0
iface eth0 inet static
	address 192.197.4.4
	netmask 255.255.255.0
	gateway 192.197.4.1
```

### Flamme
```
auto eth0
iface eth0 inet static
	address 192.197.4.5
	netmask 255.255.255.0
	gateway 192.197.4.1
```

### Fern
```
auto eth0
iface eth0 inet static
	address 192.197.4.6
	netmask 255.255.255.0
	gateway 192.197.4.1
```

### Selanjutnya kita configure untuk masing-masing node : 
Note : Pastikan untuk memasukkan command : ``` echo nameserver 192.168.122.1 > /etc/resolv.conf ``` sebelum menginstall sesuatu

### Aura
DHCP Relay 
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.197.0.0/16
echo nameserver 192.168.122.1 > /etc/resolve.conf
apt-get update
apt-get install isc-dhcp-relay
```
Lalu pada file ```etc/dhcp/dhcpd.conf```, kita dapat konfigurasi untuk forward ke IP DHCP server yakni Himmel dan menambahkan interfaces sesuai topologi yakni : ```eth 1 eth2 eth3 eth4``` dengan cara menambahkan kode berikut
```
SERVER = "192.197.1.2"
INTERFACES = "eth1 eth2 eth3 eth4"
OPTIONS = ""
```

### Heiter
DNS Server
```
echo nameserver 192.197.122.1 > /etc/resolv.conf
apt-get update
apt-get install bind9 -y
```

### Himmel
DHCP Server
```
echo nameserver 192.197.122.1 > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-server -y
```

### Denken
Database Server
```
echo 'nameserver 192.197.1.2' > /etc/resolv.conf
apt-get update
apt-get install mariadb-server -y
service mysql start
```

### Eisen
Load Balancer
```
echo nameserver 192.197.1.2 > /etc/resolv.conf
apt-get update
apt-get install apcahe2-utils -y
apt-get install nginx -y
apt-get install lynx -y
```

### Lawine, Linie, dan Lugner
PHP worker
```
echo 'nameserver 192.197.1.2' > /etc/resolv.conf
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
### Revolte, Ricter, Sein, Stark
Clients
```
apt update
apt install lynx -y
apt install htop -y
apt install apache2-utils -y
apt-get install jq -y
```

### Frieren, Flamme, Fern
Laravel Workers
```
echo 'nameserver 192.197.1.2' > /etc/resolv.conf
apt-get update
apt-get install lynx -y
apt-get install mariadb-client -y
# Test connection from worker to database
# mariadb --host=192.197.2.1 --port=3306   --user=kelompokd12 --password=passwordd12 dbkelompokd12 -e "SHOW DATABASES;"
apt-get install -y lsb-release ca-certificates a   apt-transport-https software-properties-common gnupg2
curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
apt-get update
apt-get install php8.0-mbstring php8.0-xml php8.0-cli   php8.0-common php8.0-intl php8.0-opcache php8.0-readline php8.0-mysql php8.0-fpm php8.0-curl unzip wget -y
apt-get install nginx -y

service nginx start
service php8.0-fpm start
```

### Soal 1
Semua CLIENTS harus menggunakan konfigurasi dari DHCP Server.
sehinnga jalankan command berikut (no1.sh) di DNS Server (Heiter):
```
echo 'zone "riegel.canyon.d12.com" {
    type master;
    file "/etc/bind/sites/riegel.canyon.d12.com";
};

zone "granz.channel.d12.com" {
    type master;
    file "/etc/bind/sites/granz.channel.d12.com";
};

zone "1.197.192.in-addr.arpa" {
    type master;
    file "/etc/bind/sites/1.197.192.in-addr.arpa";
};' > /etc/bind/named.conf.local

mkdir -p /etc/bind/sites
cp /etc/bind/db.local /etc/bind/sites/riegel.canyon.d12.com
cp /etc/bind/db.local /etc/bind/sites/granz.channel.d12.com
cp /etc/bind/db.local /etc/bind/sites/1.197.192.in-addr.arpa

echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.d12.com. root.riegel.canyon.d12.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.d12.com.
@       IN      A       192.197.4.5     ; IP Fern
www     IN      CNAME   riegel.canyon.d12.com.' > /etc/bind/sites/riegel.canyon.d12.com

echo '
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.d12.com. root.granz.channel.d12.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.d12.com.
@       IN      A       192.197.3.5     ; IP Lugner
www     IN      CNAME   granz.channel.d12.com.' > /etc/bind/sites/granz.channel.d12.com

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

service bind9 start
```

### Hasil
![Screenshot 2023-11-16 171713](https://github.com/revelwivanto/Jarkom-Modul-1-D12-2023/assets/116476269/8d7d51a7-93a3-4f1b-8d99-c2618788b599)

### Soal 2 - 5
Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.16 - [prefix IP].3.32 dan [prefix IP].3.64 - [prefix IP].3.80 (2)
Client yang melalui Switch4 mendapatkan range IP dari [prefix IP].4.12 - [prefix IP].4.20 dan [prefix IP].4.160 - [prefix IP].4.168 (3)
Client mendapatkan DNS dari Heiter dan dapat terhubung dengan internet melalui DNS tersebut (4)
Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch3 selama 3 menit sedangkan pada client yang melalui Switch4 selama 12 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 96 menit (5)


```
echo 'subnet 192.197.1.0 netmask 255.255.255.0 {
}

subnet 192.197.2.0 netmask 255.255.255.0 {
}

subnet 192.197.3.0 netmask 255.255.255.0 {
    range 192.197.3.16 192.197.3.32;
    range 192.197.3.64 192.197.3.80;
    option routers 192.197.3.0;
    option broadcast-address 192.197.3.255;
    option domain-name-servers 192.197.1.2;
    default-lease-time 180;
    max-lease-time 5760;
}

subnet 192.197.4.0 netmask 255.255.255.0 {
    range 192.197.4.12 192.197.4.20;
    range 192.197.4.160 192.197.4.168;
    option routers 192.197.4.0;
    option broadcast-address 192.197.4.255;
    option domain-name-servers 192.197.1.2;
    default-lease-time 720;
    max-lease-time 5760;
}

service isc-dhcp-server restart
```

Restart node Clients dengan sehinnga memiliki IP

![Screenshot 2023-11-16 172129](https://github.com/revelwivanto/Jarkom-Modul-1-D12-2023/assets/116476269/6dea8b54-e6e9-46d4-834a-9cdb7fb3f45f)

### Soal 6
Pada masing-masing worker PHP, lakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3.

Setelah kita melakukan setup terhadap seluruh PHP worker, maka kita dapat mendownload file dan unzip menggunakan tools ```wget```
```
wget -O '/var/www/granz.channel.d12.com' 'https://drive.google.com/u/0/uc?id=1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1&export=download'
unzip -o /var/www/granz.channel.d12.com -d /var/www/
rm /var/www/granz.channel.d12.com
mv /var/www/modul-3 /var/www/granz.channel.d12.com
```

Setelah itu kia dapat mengkonfigurasi ```nginx```
```
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/granz.channel.d12.com
ln -s /etc/nginx/sites-available/granz.channel.d12.com /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

echo 'server {
    listen 80;
    server_name _;

    root /var/www/granz.channel.d12.com;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.3-fpm.sock; 
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}' > /etc/nginx/sites-available/granz.channel.d12.com

service nginx restart
```

## Soal 7
>Kepala suku dari Bredt Region memberikan resource server sebagai berikut: Lawine, 4GB, 2vCPU, dan 80 GB SSD. Linie, 2GB, 2vCPU, dan 50 GB SSD. Lugner 1GB, 1vCPU, dan 25 GB SSD. Aturlah agar Eisen dapat bekerja dengan maksimal, lalu lakukan testing dengan 1000 request dan 100 request/second

Sebelumnya kita perlu melakukan setup terhadap konfigurasi load balancing pada node Eisen dengan memasukkan script berikut : 
```
echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.d12.com. root.riegel.canyon.d12.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.d12.com.
@       IN      A       192.173.2.2     ; IP LB Eiken
www     IN      CNAME   riegel.canyon.d12.com.' > /etc/bind/sites/riegel.canyon.d12.com

echo '
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.d12.com. root.granz.channel.d12.com. (
                        2023111401      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.d12.com.
@       IN      A       192.173.2.2     ; IP LB Eiken
www     IN      CNAME   granz.channel.d12.com.' > /etc/bind/sites/granz.channel.d12.com
```
Lalu kita konfigurasi nginx pada node Eisen :
```
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/lb_php

echo ' upstream worker {
    server 1927.197.3.4;
    server 192.197.3.5;
    server 192.197.3.6;
}

server {
    listen 80;
    server_name granz.channel.d12.com www.granz.channel.d12.com;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;

    server_name _;

    location / {
        proxy_pass http://worker;
    }
} ' > /etc/nginx/sites-available/lb_php

ln -s /etc/nginx/sites-available/lb_php /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

service nginx restart
```
## Soal 8
> Karena diminta untuk menuliskan grimoire, buatlah analisis hasil testing dengan 200 request dan 10 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
a. Nama Algoritma Load Balancer
b. Report hasil testing pada Apache Benchmark
c. Grafik request per second untuk masing masing algoritma. 
d. Analisis

Seperti biasa kita lakukan setup untuk load balancing seperti nomor 7.

Kemudian kita jalankan pada client Revolte command berikut : 
```
ab -n 200 -c 10 http://www.granz.channel.d12.com/
```
## Soal 9
> Dengan menggunakan algoritma Round Robin, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 100 request dengan 10 request/second, kemudian tambahkan grafiknya pada grimoire.

Kita perlu melakukan setup pada node Eisen dan melakukan testing pada load balancer sebelumnya namun dengan 1 worker, 2 worker, dan 3 worker.
Kemudian kita jalankan pada client Revolte command berikut : 
```
ab -n 100 -c 10 http://www.granz.channel.d12.com/
```

## Soal 10
> Selanjutnya coba tambahkan konfigurasi autentikasi di LB dengan dengan kombinasi username: “netics” dan password: “ajkyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/rahasisakita/

Seperti biasa kita setup seperti sebelumnya kemudian lakukan konfigurasi berikut : 
```
mkdir /etc/nginx/rahasisakita
htpasswd -c /etc/nginx/rahasisakita/htpasswd netics
```
<img width="348" alt="2023-11-19 21_17_50-LAPORAN JARKOM 3" src="https://github.com/cchoirun/Jarkom-Modul-3-D12-2023/assets/115228631/268e91c3-209d-4fd2-81e5-626b21ac19e4">

Kemudian password kita masukkan ```ajkd12```. Lalu kita masukkan command pada setup nginx : 
```
auth_basic "Restricted Content";
auth_basic_user_file /etc/nginx/rahasisakita/htpasswd;
```
## Soal 11
> Lalu buat untuk setiap request yang mengandung /its akan di proxy passing menuju halaman https://www.its.ac.id.

Setelah melakukan setup kemudian kita dapat memasukkan script berikut : 
```
echo 'upstream worker {
    server 192.173.3.1;
    server 192.173.3.2;
    server 192.173.3.3;
}

server {
    listen 80;
    server_name granz.channel.d12.com www.granz.channel.d12.com;

    root /var/www/html;
    index index.html index.htm index.nginx-debian.html;

    location / {
        proxy_pass http://worker;
    }

    location ~ /its {
        proxy_pass https://www.its.ac.id;
        proxy_set_header Host www.its.ac.id;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}' > /etc/nginx/sites-available/lb_php
```

## Soal 12
> Selanjutnya LB ini hanya boleh diakses oleh client dengan IP [Prefix IP].3.69, [Prefix IP].3.70, [Prefix IP].4.167, dan [Prefix IP].4.168.

Setelah melakukan setup maka kita dapat memasukkan script berikut : 
```
echo 'upstream worker {
    server 192.173.3.1;
    server 192.173.3.2;
    server 192.173.3.3;
}

server {
    listen 80;
    server_name granz.channel.d12.com www.granz.channel.d12.com;

    root /var/www/html;
    index index.html index.htm index.nginx-debian.html;

    location / {
        allow 192.197.3.69;
        allow 192.197.3.70;
        allow 192.197.4.167;
        allow 192.197.4.168;
        deny all;
        proxy_pass http://worker;
    }

    location /its {
        proxy_pass https://www.its.ac.id;
        proxy_set_header Host www.its.ac.id;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}' > /etc/nginx/sites-available/lb_php
```

Dengan memasukkan script tersebut maka hanya ada beberapa IP yang diizinkan sesuai dengan ketentuan soal.

### Soal 13
```
echo '# This group is read both by the client and the server
# use it for options that affect everything
[client-server]

# Import all .cnf files from configuration directory
!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mariadb.conf.d/

# Options affecting the MySQL server (mysqld)
[mysqld]
skip-networking=0
skip-bind-address
' > /etc/mysql/my.cnf
```
<ul>
<li>Ubah bind-address  = 0.0.0.0</li>
<li>service mysql restart</li>
</ul>

jalankan command:
![Screenshot 2023-11-16 201107](https://github.com/revelwivanto/Jarkom-Modul-1-D12-2023/assets/116476269/d2abc88d-78dd-48b0-8e31-c099773b42ef)
![Screenshot 2023-11-16 201544](https://github.com/revelwivanto/Jarkom-Modul-1-D12-2023/assets/116476269/758ca6d4-7a63-45ce-a48d-3c26a6b5a10e)


