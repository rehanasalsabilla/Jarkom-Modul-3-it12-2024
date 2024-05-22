# Jarkom-Modul-3-it12-2024

### Kelompok: it12
### Anggota: 
Nama | NRP | 
--- | --- |
Rehnana Putri Salsabilla | 5027221015 | 
Muhammad Rifqi Oktaviansyah | 5027221067 | 

## Daftar isi
- [Topologi](#topologi)
- [Konfigurasi](#konfigurasi)
- [Setting Node](#Setting-Node)
- [Soal 1](#soal-1)
- [Soal 2](#soal-2)
- [Soal 3](#soal-3)
- [Soal 4](#soal-4)
- [Soal 5](#soal-5)
- [Soal 6](#soal-6)
- [Soal 7](#soal-7)
- [Soal 8](#soal-8)
- [Soal 9](#soal-9)
- [Soal 10](#soal-10)
- [Soal 11](#soal-11)
- [Soal 12](#soal-12)
- [Soal 13](#soal-13)
- [Soal 14](#soal-14)
- [Soal 15](#soal-15)
- [Soal 16](#soal-16)
- [Soal 17](#soal-17)
- [Soal 18](#soal-18)
- [Soal 19](#soal-19)
- [Soal 20](#soal-20)

## Topologi
![Screenshot 2024-05-19 211343](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/56e13101-32cb-4195-b7f5-87a86ef576e0)

## Konfigurasi
### Arakis ( Router (DHCP Relay) )
```
auto eth0
iface eth0 inet dhcp
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.173.0.0/16

auto eth1
iface eth1 inet static
	address 192.239.1.0
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.239.2.0
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.239.3.0
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 192.239.4.0
	netmask 255.255.255.0
```

### Mohiam ( DHCP Server )
```
auto eth0
iface eth0 inet static
	address 192.239.3.3
	netmask 255.255.255.0
	gateway 192.239.3.0
```

### Irulan ( DNS Server )
```
auto eth0
iface eth0 inet static
	address 192.239.3.2
	netmask 255.255.255.0
	gateway 192.239.3.0
```

### Chani ( Database Server )
```
auto eth0
iface eth0 inet static
	address 192.173.4.3
	netmask 255.255.255.0
	gateway 192.173.4.0
```

### Stilgar ( Load Balancer )
```
auto eth0
iface eth0 inet static
	address 192.239.4.2
	netmask 255.255.255.0
	gateway 192.239.4.0
```

### Leto ( Laravel Worker )
```
auto eth0
iface eth0 inet static
	address 192.239.2.3
	netmask 255.255.255.0
	gateway 192.239.2.0
```

### Duncan ( Laravel Worker )
```
auto eth0
iface eth0 inet static
	address 192.239.2.4
	netmask 255.255.255.0
	gateway 192.239.2.0
```

### Jessica ( Laravel Worker )
```
auto eth0
iface eth0 inet static
	address 192.239.2.5
	netmask 255.255.255.0
	gateway 192.239.2.0
```

### Vladimir ( PHP Worker )
```
auto eth0
iface eth0 inet static
	address 192.239.1.3
	netmask 255.255.255.0
	gateway 192.239.1.0
```

### Rabban ( PHP Worker )
```
auto eth0
iface eth0 inet static
	address 192.239.1.4
	netmask 255.255.255.0
	gateway 192.239.1.0
```

### Feyd ( PHP Worker )
```
auto eth0
iface eth0 inet static
	address 192.239.1.5
	netmask 255.255.255.0
	gateway 192.239.1.0
```

### Dmitri & Paul ( Client )
```
auto eth0
iface eth0 inet dhcp
```

## Setting Node 
- Melakukan Pengaturan pada ``*.bashrc*`` atau melakukan setting pada script masing" node nya.
### DNS Server
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install bind9 -y
```
### DHCP Server
```
echo 'nameserver 192.239.3.2' > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-server -y
```
### Router (DHCP Relay)
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.239.0.0/16
apt-get update
apt install isc-dhcp-relay -y
```
### Database Server
```
echo 'nameserver 192.239.3.2' > /etc/resolv.conf
apt-get update
apt-get install mariadb-server -y
service mysql start
```
### Load Balancer
```
echo 'nameserver 192.239.3.2' > /etc/resolv.conf
apt-get update
apt-get install apache2-utils -y
apt-get install nginx -y
apt-get install lynx -y
```
### Laravel Worker
```
```
### PHP Worker
```
echo 'nameserver 192.239.3.2' > /etc/resolv.conf
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
### Client
```
apt update
apt install lynx -y
apt install htop -y
apt install apache2-utils -y
apt-get install jq -y
```

# Penyelesaian 
## Soal 1
Lakukan konfigurasi sesuai dengan peta yang sudah diberikan.
Planet Caladan sedang mengalami krisis karena kehabisan spice, klan atreides berencana untuk melakukan eksplorasi ke planet arakis dipimpin oleh duke leto mereka meregister domain name atreides.yyy.com untuk worker Laravel mengarah pada Leto Atreides . Namun ternyata tidak hanya klan atreides yang berusaha melakukan eksplorasi, Klan harkonen sudah mendaftarkan domain name harkonen.yyy.com untuk worker PHP (0) mengarah pada Vladimir Harkonen.
#### Penyelesaian 
- Mengatur Script pada Node **Irulan.sh** ( DNS Server )
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install bind9 -y

echo 'options {
      directory "/var/cache/bind";

      forwarders {
              192.168.122.1;
      };

      // dnssec-validation auto;
      allow-query{any;};
      auth-nxdomain no;    # conform to RFC1035
      listen-on-v6 { any; };
}; ' > /etc/bind/named.conf.options

echo "zone \"atreides.it12.com\" {
	type master;
	file \"/etc/bind/jarkom/atreides.it12.com\";
};

zone \"harkonen.it12.com\" {
	type master;
	file \"/etc/bind/jarkom/harkonen.it12.com\";
};
" > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

atreides="
;
;BIND data file for local loopback interface
;
\$TTL    604800
@    IN    SOA    atreides.it12.com. root.atreides.it12.com. (
        2        ; Serial
                604800        ; Refresh
                86400        ; Retry
                2419200        ; Expire
                604800 )    ; Negative Cache TTL
;                   
@    IN    NS    atreides.it12.com.
@       IN    A    192.239.2.3
"
echo "$atreides" > /etc/bind/jarkom/atreides.it12.com

harkonen="
;
;BIND data file for local loopback interface
;
\$TTL    604800
@    IN    SOA    harkonen.it12.com. root.harkonen.it12.com. (
        2        ; Serial
                604800        ; Refresh
                86400        ; Retry
                2419200        ; Expire
                604800 )    ; Negative Cache TTL
;                   
@    IN    NS    harkonen.it12.com.
@       IN    A    192.239.1.3
"
echo "$harkonen" > /etc/bind/jarkom/harkonen.it12.com


service bind9 start
```
## Result Nomor 1
#### Paul ( Client )
![Screenshot 2024-05-19 212734](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/7654f5fc-2dd4-4768-9437-595906e415c6)
![Screenshot 2024-05-19 212811](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/176c4925-4274-4796-bbb1-04f276c8921d)

#### Dmitri ( Client )
![Screenshot 2024-05-19 212945](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/ad5b4b5c-97a4-41bf-ab3d-d697b8863067)
![Screenshot 2024-05-19 213022](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/56dba604-f055-4836-af79-13066bffc716)


## Soal 2
Kemudian, karena masih banyak spice yang harus dikumpulkan, bantulah para aterides untuk bersaing dengan harkonen dengan kriteria berikut.:
Semua CLIENT harus menggunakan konfigurasi dari DHCP Server.
Client yang melalui House Harkonen mendapatkan range IP dari 192.239.1.14 - 192.239.1.28 dan 192.239.1.49 - 192.239.1.70
#### Penyelesaian 
- Melakaukan setup untuk Node **Mohiam.sh** ( DHCP Server )

```
echo 'nameserver 192.239.3.2' > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-server -y

interfaces="INTERFACESv4=\"eth0\"
INTERFACESv6=\"\"
"
echo "$interfaces" > /etc/default/isc-dhcp-server

subnet="option domain-name \"example.org\";
option domain-name-servers ns1.example.org, ns2.example.org;

default-lease-time 600;
max-lease-time 7200;

ddns-update-style-none;

subnet 192.239.1.0 netmask 255.255.255.0 {
    range 192.239.1.14 192.239.1.28;
    range 192.239.1.49 192.239.1.70;
    option routers 192.239.1.0;
}
```

## Soal 3
Client yang melalui House Atreides mendapatkan range IP dari 192.239.2.15 - 192.239.2.25 dan 192.239.2 .200 - 192.239.2.210
- Melakaukan setup untuk Node **Mohiam.sh** ( DHCP Server )
```
echo 'nameserver 192.239.3.2' > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-server -y

interfaces="INTERFACESv4=\"eth0\"
INTERFACESv6=\"\"
"
echo "$interfaces" > /etc/default/isc-dhcp-server

subnet="option domain-name \"example.org\";
option domain-name-servers ns1.example.org, ns2.example.org;

default-lease-time 600;
max-lease-time 7200;

ddns-update-style-none;

subnet 192.239.1.0 netmask 255.255.255.0 {
    range 192.239.1.14 192.239.1.28;
    range 192.239.1.49 192.239.1.70;
    option routers 192.239.1.0;
}

subnet 192.239.2.0 netmask 255.255.255.0 {
    range 192.239.2.15 192.239.2.25;
    range 192.239.2.200 192.239.2.210;
    option routers 192.239.2.0;
}
```

## Soal 4
Client mendapatkan DNS dari Princess Irulan dan dapat terhubung dengan internet melalui DNS tersebut 
- Melakaukan setup untuk Node **Mohiam.sh** ( DHCP Server )
```
echo 'nameserver 192.239.3.2' > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-server -y

interfaces="INTERFACESv4=\"eth0\"
INTERFACESv6=\"\"
"
echo "$interfaces" > /etc/default/isc-dhcp-server

subnet="option domain-name \"example.org\";
option domain-name-servers ns1.example.org, ns2.example.org;

default-lease-time 600;
max-lease-time 7200;

ddns-update-style-none;

subnet 192.239.1.0 netmask 255.255.255.0 {
    range 192.239.1.14 192.239.1.28;
    range 192.239.1.49 192.239.1.70;
    option routers 192.239.1.0;
    option broadcast-address 192.239.1.255;
    option domain-name-servers 192.239.3.2;
}

subnet 192.239.2.0 netmask 255.255.255.0 {
    range 192.239.2.15 192.239.2.25;
    range 192.239.2.200 192.239.2.210;
    option routers 192.239.2.0;
    option broadcast-address 192.239.2.255;
    option domain-name-servers 192.239.3.2;
}

subnet 192.239.3.0 netmask 255.255.255.0 {
}

subnet 192.239.4.0 netmask 255.255.255.0 {
}
```


## Soal 5 
Durasi DHCP server meminjamkan alamat IP kepada Client yang melalui House Harkonen selama 5 menit sedangkan pada client yang melalui House Atreides selama 20 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 87 menit 
- Melakaukan setup untuk Node **Mohiam.sh** ( DHCP Server )
```
echo 'nameserver 192.239.3.2' > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-server -y

interfaces="INTERFACESv4=\"eth0\"
INTERFACESv6=\"\"
"
echo "$interfaces" > /etc/default/isc-dhcp-server

subnet="option domain-name \"example.org\";
option domain-name-servers ns1.example.org, ns2.example.org;

default-lease-time 600;
max-lease-time 7200;

ddns-update-style-none;

subnet 192.239.1.0 netmask 255.255.255.0 {
    range 192.239.1.14 192.239.1.28;
    range 192.239.1.49 192.239.1.70;
    option routers 192.239.1.0;
    option broadcast-address 192.239.1.255;
    option domain-name-servers 192.239.3.2;
    default-lease-time 300;
    max-lease-time 5220;
}

subnet 192.239.2.0 netmask 255.255.255.0 {
    range 192.239.2.15 192.239.2.25;
    range 192.239.2.200 192.239.2.210;
    option routers 192.239.2.0;
    option broadcast-address 192.239.2.255;
    option domain-name-servers 192.239.3.2;
    default-lease-time 1200;
    max-lease-time 5220;
}

subnet 192.239.3.0 netmask 255.255.255.0 {
}

subnet 192.239.4.0 netmask 255.255.255.0 {
}
```

## Result Nomor 5
![Screenshot 2024-05-19 212606](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/dcadf4b5-fcc0-47cf-b15d-ff27ae72bfac)
![Screenshot 2024-05-19 212908](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/8500411a-f462-4bb5-8e3e-544fa4597f88)

## Soal 6
Seiring berjalannya waktu kondisi semakin memanas, untuk bersiap perang. Klan Harkonen melakukan deployment sebagai berikut
Vladimir Harkonen memerintahkan setiap worker(harkonen) PHP, untuk melakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3.
- Konfigurasi untuk masing masing Worker
### ex : Vladimir.sh
```
echo 'nameserver 192.239.3.2' > /etc/resolv.conf
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

wget -O '/var/www/harkonen.it12.com' 'https://drive.usercontent.google.com/download?id=1lmnXJUbyx1JDt2OA5z_1dEowxozfkn30&export=download&authuser=0' 
unzip -o /var/www/harkonen.it12.com -d /var/www/
rm /var/www/harkonen.it12.com
mv /var/www/modul-3 /var/www/harkonen.it12.com


cp /etc/nginx/sites-available/default /etc/nginx/sites-available/harkonen.it12.com
ln -s /etc/nginx/sites-available/harkonen.it12.com /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

echo 'server {
     listen 80;
     server_name _;

     root /var/www/harkonen.it12.com;
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
 }' > /etc/nginx/sites-available/harkonen.it12.com

 service nginx restart
```
- Melakukan command pada worker ```lynx localhost``` untuk cek konfigurasi webnya

## Result Nomor 6
![Screenshot 2024-05-19 224304](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/8512605c-4542-4464-93f5-5adc0be5fecf)
![Screenshot 2024-05-19 224830](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/9990e715-c38e-4557-b391-e177d6508004)
![Screenshot 2024-05-19 224934](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/59ddc3d5-95d6-45f9-8064-a675b82bb7d4)

## Soal 7
Aturlah agar Stilgar dari fremen dapat dapat bekerja sama dengan maksimal, lalu lakukan testing dengan 5000 request dan 150 request/second.
- Mengarahkan Domain pada DNS Server ke domain Load Balancer Eisen :
```
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install bind9 -y

echo 'options {
      directory "/var/cache/bind";

      forwarders {
              192.168.122.1;
      };

      // dnssec-validation auto;
      allow-query{any;};
      auth-nxdomain no;    # conform to RFC1035
      listen-on-v6 { any; };
}; ' > /etc/bind/named.conf.options

echo "zone \"atreides.it12.com\" {
	type master;
	file \"/etc/bind/jarkom/atreides.it12.com\";
};

zone \"harkonen.it12.com\" {
	type master;
	file \"/etc/bind/jarkom/harkonen.it12.com\";
};
" > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

atreides="
;
;BIND data file for local loopback interface
;
\$TTL    604800
@    IN    SOA    atreides.it12.com. root.atreides.it12.com. (
        2        ; Serial
                604800        ; Refresh
                86400        ; Retry
                2419200        ; Expire
                604800 )    ; Negative Cache TTL
;                   
@    IN    NS    atreides.it12.com.
@       IN    A    192.239.4.2
"
echo "$atreides" > /etc/bind/jarkom/atreides.it12.com

harkonen="
;
;BIND data file for local loopback interface
;
\$TTL    604800
@    IN    SOA    harkonen.it12.com. root.harkonen.it12.com. (
        2        ; Serial
                604800        ; Refresh
                86400        ; Retry
                2419200        ; Expire
                604800 )    ; Negative Cache TTL
;                   
@    IN    NS    harkonen.it12.com.
@       IN    A    192.239.4.2
"
echo "$harkonen" > /etc/bind/jarkom/harkonen.it12.com


service bind9 start
```
- Melakukan konfigurasi pada Stilgar *( Load Balancer )*
```
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/lb_php


echo ' upstream worker {
    server 192.239.1.3;
    server 192.239.1.4;
    server 192.239.1.5;
}

server {
    listen 80;
    server_name harkonen.it12.com www.harkonen.it12.com;

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
- Melakukan run konfigurasi pada Client ( Paul )
```
apt update
apt install lynx -y
apt install htop -y
apt install apache2-utils -y
apt-get install jq -y
```
- Melakukan Command pada client ```ab -n 5000 -c 150 http://harkonen.it12.com/```

## Result Nomor 7
![Screenshot 2024-05-19 232848](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/f082b389-aa29-4e14-b00f-15f8201038f7)
![Screenshot 2024-05-19 232858](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/0a214aab-3f66-403f-b7a1-2313ee51de5c)
## Soal 8 
Karena diminta untuk menuliskan peta tercepat menuju spice, buatlah analisis hasil testing dengan 500 request dan 50 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
a. Nama Algoritma Load Balancer
b. Report hasil testing pada Apache Benchmark
c. Grafik request per second untuk masing masing algoritma. 
d. Analisis 

- Script masih sama dengannomor 7. Namun disini melakukan run dan konfigurasi ulang yang berbeda sebanyak 4 kali sesuai load balancer yang diminta
### Round-robin
```
echo ' upstream worker {
    server 192.239.1.3;
    server 192.239.1.4;
    server 192.239.1.5;
}
```
### Generic Hash
```
echo ' upstream worker {
    hash $request_uri consistent;
    server 192.239.1.3;
    server 192.239.1.4;
    server 192.239.1.5;
}
```
### Least Connection
```
echo ' upstream worker {
    least_conn;
    server 192.239.1.3;
    server 192.239.1.4;
    server 192.239.1.5;
}
```
### IP Hash
```
echo ' upstream worker {
    ip_hash;
    server 192.239.1.3;
    server 192.239.1.4;
    server 192.239.1.5;
}
```
### Konfigurasi lengkap Stilgar.sh
```
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/lb_php


echo ' upstream worker {
    #    hash $request_uri consistent;
    #    least_conn;
    #    ip_hash;
    server 192.239.1.3;
    server 192.239.1.4;
    server 192.239.1.5;
}

server {
    listen 80;
    server_name harkonen.it12.com www.harkonen.it12.com;

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
- Melakukan Command pada client ```ab -n 500 -c 50 http://harkonen.it12.com/```

## Result Nomor 8
### Round-robin
![Screenshot 2024-05-22 091941](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/8fdb649a-7838-491a-b59a-c7cb8bac66b7)
![Screenshot 2024-05-22 091952](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/7a38e4b9-50be-47e0-b354-e37c271dc1f6)

### Generic Hash
![Screenshot 2024-05-19 233000](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/08712c5e-5a0a-4f5a-b9ba-f600920ebe7c)
![Screenshot 2024-05-19 233011](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/32bd38b2-bb55-40c4-9b22-eea0c8bd092b)

### Least Connection
![Screenshot 2024-05-19 233128](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/36705651-d173-4356-8e6f-fc1539ef3e9a)
![Screenshot 2024-05-19 233135](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/638a401c-d6d2-42b8-9192-f2ac48199aee)

### IP Hash
![Screenshot 2024-05-19 233446](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/7bc3e472-9215-4388-9411-a30baadfe9e1)
![Screenshot 2024-05-19 233451](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/4f07a840-7aa2-4c86-9ddf-2793a2f76df6)

### Grafik : 
![Points scored](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/8939b7ce-e153-4d19-837d-ae0a677a5d0d)

### Analisis :
Algoritma Round-robin menunjukkan performa terbaik dengan sekitar 380 poin, mengindikasikan efisiensi tinggi dalam distribusi beban secara merata. Algoritma Least Connection dan Generic Hash berada di posisi menengah dengan masing-masing sekitar 250 dan 220 poin, menunjukkan kemampuan yang cukup kompetitif namun sedikit kurang optimal dibandingkan Round-robin. Sementara itu, algoritma IP Hash memiliki performa terendah dengan sekitar 200 poin, kemungkinan disebabkan oleh distribusi beban yang tidak merata dari alamat IP klien. Dengan demikian, Round-robin menjadi pilihan paling efisien dalam skenario ini

## Soal 9 
Dengan menggunakan algoritma Least-Connection, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 1000 request dengan 10 request/second, kemudian tambahkan grafiknya pada peta
- Script masih sama dengannomor 7. Namun disini melakukan run dan konfigurasi ulang yang berbeda sebanyak 3 kali sesuai jumlah worker yang diminta soal
### Worker 1
```
echo ' upstream worker {
    server 192.239.1.3;
}
```
### Worker 2
```
echo ' upstream worker {
    server 192.239.1.3;
    server 192.239.1.4;
}
```
### Worker 3
```
echo ' upstream worker {
    server 192.239.1.3;
    server 192.239.1.4;
    server 192.239.1.5;
}
```
### Konfigurasi lengkap Stilgar.sh ( Contoh untuk 1 worker )
```
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/lb_php


echo ' upstream worker {
    server 192.239.1.3;
    # server 192.239.1.4;
    # server 192.239.1.5;
}

server {
    listen 80;
    server_name harkonen.it12.com www.harkonen.it12.com;

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
- Melakukan Command pada client ```ab -n 1000 -c 10 http://harkonen.it12.com/```

## Result Nomor 9
### Worker 1
![Screenshot 2024-05-19 234410](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/14b1e7c0-8478-49b9-acf2-cb848338a3f7)
![Screenshot 2024-05-19 234418](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/286090ca-6280-4983-b617-171ec4567f70)

### Worker 2
![Screenshot 2024-05-19 234318](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/bbb42ea4-366b-4eef-a440-9aaca2fed2f5)
![Screenshot 2024-05-19 234324](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/4a51889b-aeea-49b3-8161-b0e0b403df17)

### worker 3 
![Screenshot 2024-05-20 235234](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/863e4738-560d-4986-8b91-01b813ab536f)
![Screenshot 2024-05-20 235249](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/9a4b276c-242d-4948-99ff-2656ca46a000)

### Grafik :
![Points scored (1)](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/2bc983f5-88cf-4793-8837-6aa81bad9f02)

### Analisis : 
Berdasarkan grafik performa pengujian algoritma Least-Connection dengan 1000 request pada laju 10 request per detik, terlihat bahwa dengan tiga worker, performa mencapai sekitar 380 poin, yang menunjukkan efisiensi tinggi dalam distribusi beban. Dengan dua worker, performa sedikit menurun menjadi sekitar 350 poin, menunjukkan bahwa sistem masih efisien meskipun beban per worker meningkat. Dengan satu worker, performa tetap sekitar 350 poin, menandakan bahwa satu worker mampu menangani beban dengan baik, meskipun tanpa redundansi. Secara keseluruhan, algoritma Least-Connection menunjukkan kemampuan yang baik dalam mendistribusikan beban secara efisien, dengan performa terbaik dicapai saat menggunakan tiga worker.

## Soal 10 
Selanjutnya coba tambahkan keamanan dengan konfigurasi autentikasi di LB dengan dengan kombinasi username: “secmart” dan password: “kcksyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/supersecret/ 
- Menambahkan script untuk mkdir dan juga auth didalam Stilgar.sh
```
mkdir /etc/nginx/supersecret
htpasswd -c /etc/nginx/supersecret/htpasswd secmart
```
```
zauth_basic "Restricted Content";
auth_basic_user_file /etc/nginx/supersecret/htpasswd;
```
### Script Stilgar.sh lengkap 
```
cp /etc/nginx/sites-available/default /etc/nginx/sites-available/lb_php
mkdir /etc/nginx/supersecret
htpasswd -c /etc/nginx/supersecret/htpasswd secmart

echo ' upstream worker {
    server 192.239.1.3;
    # server 192.239.1.4;
    # server 192.239.1.5;
}

server {
    listen 80;
    server_name harkonen.it12.com www.harkonen.it12.com;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;

    server_name _;

    location / {

        proxy_pass http://worker;
	zauth_basic "Restricted Content";
	auth_basic_user_file /etc/nginx/supersecret/htpasswd;
}

} ' > /etc/nginx/sites-available/lb_php

ln -s /etc/nginx/sites-available/lb_php /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

service nginx restart
```

- Melakukan Command pada client ```lynx http://harkonen.it12.com/```


## Result Nomor 10
![Screenshot 2024-05-21 001441](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/e39b8b0d-0df5-4671-8fd6-1b2e23bb57e8)
![Screenshot 2024-05-21 001457](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/bf3b9e1f-304a-452b-90c3-6c5e4ae40a33)
![Screenshot 2024-05-21 001516](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/dbad016f-50f1-45a8-a4ca-9fedbe87ef96)

## Soal 11 
Lalu buat untuk setiap request yang mengandung /dune akan di proxy passing menuju halaman https://www.dunemovie.com.au/.
- Menambahkan script pada stilgar.sh ( Load balancer )
```
      location /dune {
        proxy_pass https://www.dunemovie.com.au/;
        proxy_set_header Host www.dunemovie.com.au;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
}
```

#### Script Stilgar.sh lengkap 
```
echo 'nameserver 192.239.3.2' > /etc/resolv.conf
apt-get update
apt-get install apache2-utils -y
apt-get install nginx -y
apt-get install lynx -y

service nginx start

cp /etc/nginx/sites-available/default /etc/nginx/sites-available/lb_php
# mkdir /etc/nginx/supersecret
# htpasswd -c /etc/nginx/supersecret/htpasswd secmart


echo ' upstream worker {
    #    hash $request_uri consistent;
    #    least_conn;
    #    ip_hash;
    server 192.239.1.3;
    server 192.239.1.4;
    server 192.239.1.5;
}

server {
    listen 80;
    server_name harkonen.it12.com www.harkonen.it12.com;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;

    server_name _;
        proxy_pass http://worker;
        # zauth_basic "Restricted Content";
        # auth_basic_user_file /etc/nginx/supersecret/htpasswd;
}
#       location /dune {
#         proxy_pass https://www.dunemovie.com.au/;
#         proxy_set_header Host www.dunemovie.com.au;
#         proxy_set_header X-Real-IP $remote_addr;
#         proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
#         proxy_set_header X-Forwarded-Proto $scheme;
# }

} ' > /etc/nginx/sites-available/lb_php

ln -s /etc/nginx/sites-available/lb_php /etc/nginx/sites-enabled/
rm /etc/nginx/sites-enabled/default

service nginx restart
```

- Melakukan Command pada client ```lynx http://harkonen.it12.com/dune```

## Result Nomor 11
![Screenshot 2024-05-21 011558](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/b9df6f72-5fb4-424d-8d2c-7fdee3bb006d)

## Soal 12
Selanjutnya LB ini hanya boleh diakses oleh client dengan IP 192.239.1.37, 192.239.1.67, 192.239.2.203, dan 192.239.2.207.
- Menambahkan script pada stilgar.sh
```
location / {
    allow 192.239.1.37;
    allow 192.239.1.67;
    allow 192.239.2.203;  
    allow 192.239.2.207;
    deny all;
proxy_pass http://worker;
```

- Selanjutnya menentukan client mana yang dapat memiliki akses ( disini saya menggunakan Paul ). Tambahkan konfigurasi pada Mohiam.sh
```
host Paul {
    hardware ethernet f2:ec:68:ce:25:0e;
    fixed-address 192.239.2.203;
}
```

- Selanjutnya juga menambahkan konfigurasi pada script di node client
```
apt update
apt install lynx -y
apt install htop -y
apt install apache2-utils -y
apt-get install jq -y

config="auto eth0
iface eth0 inet dhcp
hwaddress ether 72:b7:93:55:30:f5
"
echo "$config" > /etc/network/interfaces
```

- Melakukan Command pada client paul ```lynx http://harkonen.it12.com/\```

#### IP Paul setelah konfigurasi:
![Screenshot 2024-05-21 005030](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/f5e6ef2f-22c0-41a5-b539-eae47399abb2)

## Result Nomor 12
### Selain Paul
![Screenshot 2024-05-21 005650](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/8c5facf8-d4df-4013-9b23-80cdc824b922)
![Screenshot 2024-05-21 005657](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/c965a950-60de-4345-87fd-42640625d62e)
### Pada client Paul
![Screenshot 2024-05-21 005456](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/136863633/89113de8-6e7b-4e4f-a078-1af75cb73b3c)

## Soal 13
Tidak mau kalah dalam perburuan spice, House atreides juga mengatur para pekerja di atreides.yyy.com.
Semua data yang diperlukan, diatur pada Chani dan harus dapat diakses oleh Leto, Duncan, dan Jessica.

### Penyelesaian
Masukkan konfigurasi berikut pada ```Database Server``` yaitu ```Chani```
```
echo 'nameserver 192.239.3.2' > /etc/resolv.conf
apt-get update
apt-get install mariadb-server -y
service mysql start

# Db akan diakses oleh 3 worker, maka 
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


cd /etc/mysql/mariadb.conf.d
nano 50-server.cnf

service mysql restart
```
Lalu, ubah ```bind-address``` pada path ```/etc/mysql/mariadb.conf.d/50-server.cnf``` menjadi ```0.0.0.0```
```
bind-address            = 0.0.0.0
```
Jangan lupa untuk merestart mysql dengan ```service mysql restart```
Setelah itu, masuk mysql dengan command ```mysql -u root -p``` dan jalankan command berikut 
```
#CREATE USER 'kelompokit12'@'%' IDENTIFIED BY 'passwordit12';
#CREATE USER 'kelompokit12'@'localhost' IDENTIFIED BY 'passwordit12';
#CREATE DATABASE dbkelompokit12;
#GRANT ALL PRIVILEGES ON *.* TO 'kelompokit12'@'%';
#GRANT ALL PRIVILEGES ON *.* TO 'kelompokit12'@'localhost';
#FLUSH PRIVILEGES;
```
### Hasil
Setelah itu lakukan pengecekan di salah satu Laravel Worker. Disini akan dilakukan pengecekan di worker ```Leto``` dengan memasukkan command berikut
```
mariadb --host=192.239.4.3 --port=3306 --user=kelompokit12 --password=passwordit12 dbkelompokit12 -e "SHOW DATABASES;"
```
![no13 worker](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/143682058/1a51fd71-02ac-4e9a-89e9-ddb40b6b3b5e)

## Soal 14
Leto, Duncan, dan Jessica memiliki atreides Channel sesuai dengan quest guide berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer

### Penyelesaian
Masukkan command berikut pada Laravel Worker untuk menginstall ```composer```, ```git```, dan ```clone repo```
```
wget https://getcomposer.org/download/2.0.13/composer.phar
chmod +x composer.phar
mv composer.phar /usr/local/bin/composer

apt-get install git -y
cd /var/www && git clone https://github.com/martuafernando/laravel-praktikum-jarkom
cd /var/www/laravel-praktikum-jarkom && composer update

cd /var/www/laravel-praktikum-jarkom && cp .env.example .env
echo 'APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=192.239.4.3
DB_PORT=3306
DB_DATABASE=dbkelompokit12
DB_USERNAME=kelompokit12
DB_PASSWORD=passwordit12

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
cd /var/www/laravel-praktikum-jarkom && php artisan key:generate
cd /var/www/laravel-praktikum-jarkom && php artisan config:cache
cd /var/www/laravel-praktikum-jarkom && php artisan migrate
cd /var/www/laravel-praktikum-jarkom && php artisan db:seed
cd /var/www/laravel-praktikum-jarkom && php artisan storage:link
cd /var/www/laravel-praktikum-jarkom && php artisan jwt:secret
cd /var/www/laravel-praktikum-jarkom && php artisan config:clear
chown -R www-data.www-data /var/www/laravel-praktikum-jarkom/storage
```
Lalu, lakukan konfigurasi ```nginx``` sebagai berikut pada masing-masing worker dimana portnya sebagai berikut
```
192.239.2.3:8001; # leto 
192.239.2.4:8002; # Duncan
192.239.2.5:8003; # Jessica
```
Dengan konfigurasi sebagai berikut
```
echo 'server {
    listen <X>; 

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

# Enable the site and restart Nginx
ln -s /etc/nginx/sites-available/laravel-worker /etc/nginx/sites-enabled/
nginx -t
/etc/init.d/nginx restart
/etc/init.d/php8.0-fpm restart
```
Dimana <X> merupakan port masing-masing worker.
### Hasil
Setelah berhasil melakukan langkah-langkah diatas lakukan testing dengan cara mengetik command
```
lynx localhost:[PORT]
```
Dimana PORT yang ada adalah ```8001``` ```8002``` dan ```8003``` sesuai dengan setup nginx sebelumnya
![no14 isi laravel](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/143682058/ed62c58a-3e02-46f6-ab1f-1d093d50a539)
## Soal 15
atreides Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada peta.
a. POST /auth/register

### Penyelesaian
Untuk mengerjakan soal ini diperlukan melakukan testing menggunakan Apache Benchmark pada salah satu worker saja. Disini kami menggunakan worker laravel ```Leto``` yang nantinya akan ditesting oleh client ```Paul```. Sebelum dilakukan testing, kami menggunakan file .json yang akan digunakan sebagai body yang akan dikirim pada endpoint /api/auth/register seperti berikut
```
echo '
{
  "username": "kelompokit12",
  "password": "passwordit12",
}' > creds.json
```
Lalu, ketik command berikut pada client ```Paul```
```
ab -n 100 -c 10 -p creds.json -T application/json http://192.239.2.3:8001/api/auth/register
```
### Hasil
![no15](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/143682058/606d1440-fbbe-4658-8df0-36505e623753)

## Soal 16 
b. POST /auth/login

### Penyelesaian
Untuk mengerjakan soal ini diperlukan melakukan testing menggunakan Apache Benchmark pada salah satu worker saja. Disini kami menggunakan worker laravel ```Leto``` yang nantinya akan ditesting oleh client ```Paul```. Sebelum dilakukan testing, kami menggunakan file .json yang sama dengan soal sebelumnya yang akan digunakan sebagai body yang akan dikirim pada endpoint /api/auth/login seperti berikut

Ketik command berikut pada client ```Paul```
```
ab -n 100 -c 10 -p creds.json -T application/json http://192.239.2.5:8003/api/auth/login
```
### Hasil 
![no16](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/143682058/a9181274-21dd-4a6f-9b20-ea1986642abc)

## Soal 17 
GET /me

### Penyelesaian 
Untuk mengerjakan soal ini diperlukan melakukan testing menggunakan Apache Benchmark pada salah satu worker saja. Disini kami menggunakan worker laravel ```Leto``` yang nantinya akan ditesting oleh client ```Paul```.Kami menggunakan file .json yang sama dengan soal sebelumnya.  Sebelum dilakukan testing, ada beberapa konfigurasi yang perlu dilakukan

Dapatkan token terlebih dahulu dengan mengakses endpoint /api/me
```
curl -X POST -H "Content-Type: application/json" -d @creds.json http://192.239.2.3:8001/api/auth/login > login_output.txt
```
Lalu, jalankan command berikut untuk melakukan set ```token``` secara global
```
token=$(cat login_output.txt | jq -r '.token')
```
Setelah, itu jalankan perintah tersebut untuk melakukan testing
```
ab -n 100 -c 10 -H "Authorization: Bearer $token" http://192.239.2.3:8001/api/api/me
```
### Hasil
![no17](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/143682058/81327707-89a6-47f3-b7e1-678e9c738e1f)
## Soal 18 
Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur atreides Channel maka implementasikan Proxy Bind pada Stilgar untuk mengaitkan IP dari Leto, Duncan, dan Jessica.

### Penyelesaian
Sebelum mengerjakan perlu untuk melakukan setup terlebih dahulu. Setelah itu, karena hanya diberikan perintah ketiga worker berjalan secara adil, kami memberikan implementasi dari ```Load Balancing``` karena sesuai dengan definisi nya yaitu membagi rata beban kerja. Maka dari itu, berikut merupakan konfigurasi ```nginx```
```
echo 'upstream worker {
    server 192.239.2.3:8001;
    server 192.239.2.4:8002;
    server 192.239.2.5:8003;
}

server {
    listen 80;
    server_name atreides.channel.it26.com www.atreides.channel.it26.com;

    location / {
        proxy_pass http://worker;
    }
} 
' > /etc/nginx/sites-available/laravel-worker

ln -s /etc/nginx/sites-available/laravel-worker /etc/nginx/sites-enabled/laravel-worker

service nginx restart
```
### Hasil 
Setelah melakukan konfigurasi pada load balancer pada ```Stilgar```. Sekarang waktunya melakukan testing pada client ```Paul``` dengan menjalankan perintah berikut
```
ab -n 100 -c 10 -p creds.json -T application/json http://www.atreides.channel.it12.com/api/auth/login
```
Dengan hasil sebagai berikut
![no18 benchmark](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/143682058/65fddc5a-53d5-488e-a24f-c4e8b4d65a06)

Jessica

![no18 jessica](https://github.com/rehanasalsabilla/Jarkom-Modul-3-it12-2024/assets/143682058/1c73cfc4-23a8-4a6b-a660-0db0b3a8e6cf)
## Soal 19 
Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada Leto, Duncan, dan Jessica. Untuk testing kinerja naikkan 
- pm.max_children
- pm.start_servers
- pm.min_spare_servers
- pm.max_spare_servers
sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second kemudian berikan hasil analisisnya pada PDF.

### Penyelesaian
Untuk mengerjakan soal ini terdapat beberapa penjelasan sebagai berikut

```pm.max_children``` Menentukan jumlah maksimum pekerja PHP (proses anak) yang dapat berjalan secara bersamaan. Nilai ini sebaiknya disesuaikan dengan kapasitas sumber daya server. Jika terlalu rendah, server mungkin tidak dapat menangani banyak permintaan secara bersamaan, sementara jika terlalu tinggi, dapat menyebabkan kelebihan beban dan kekurangan sumber daya.

```pm.start_servers``` Menentukan jumlah pekerja PHP yang akan dimulai secara otomatis ketika PHP-FPM pertama kali dijalankan atau direstart. Ini membantu dalam mengoptimalkan performa pada saat server pertama kali dimulai.

```pm.min_spare_servers``` Menentukan jumlah minimum pekerja PHP yang tetap berjalan saat server berjalan. Ini membantu menjaga agar server tetap responsif terhadap permintaan bahkan saat lalu lintas rendah.

```pm.max_spare_servers``` Menentukan jumlah maksimum pekerja PHP yang dapat berjalan tetapi tidak menangani permintaan. Jumlah ini disesuaikan dengan kebutuhan untuk menangani lonjakan lalu lintas tanpa menambahkan terlalu banyak sumber daya ketika beban rendah.

Akan ada 4 konfigurasi terhadap proses ```package manager``` pada masing-masing worker yang nantinya akan dilakukan untuk testing.

- Script 1
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

- Script 2
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

- Script 3
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

- Script 4
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
pm.max_children = 75
pm.start_servers = 10
pm.min_spare_servers = 5
pm.max_spare_servers = 20' > /etc/php/8.0/fpm/pool.d/www.conf

service php8.0-fpm restart
```

### Hasil 

## Soal 20 
Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Stilgar. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second.

### Penyelesaian
Karena proses yang telah di konfigurasi sebelumnya pada masing-masing ```worker``` tepatnya pada ```package manager``` dan ternyata hasil yang diberikan juga tidak cukup untuk meningkatkan performa worker. Oleh karena itu, ditambahkan algoritma pada ```load balancer``` tersebut dengan menggunakan ```Least-connection``` dimana algoritma ini akan melakukan prioritas pembagian dari beban kinerja yang paling rendah. ```Node master``` akan mencatat semua beban dan kinerja dari semua node, dan akan melakukan prioritas dari beban yang paling rendah. Sehingga diharapkan tidak ada server dengan beban yang rendah.
```
echo 'upstream worker {
    least_conn;
    server 192.239.2.3:8001;
    server 192.239.2.4:8002;
    server 192.239.2.5:8003;
}

server {
    listen 80;
    server_name atreides.channel.it12.com www.atreides.channel.it12.com;

    location / {
        proxy_pass http://worker;
    }
} 
' > /etc/nginx/sites-available/laravel-worker

service nginx restart
```
Disini masih digunakan setup pada ```package manager``` sebagai berikut
```
pm = dynamic
pm.max_children = 75
pm.start_servers = 10
pm.min_spare_servers = 5
pm.max_spare_servers = 20
```

### Hasil


