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
- [Setting Node](#Setting_Node)
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


## Soal 2
Kemudian, karena masih banyak spice yang harus dikumpulkan, bantulah para aterides untuk bersaing dengan harkonen dengan kriteria berikut.:
Semua CLIENT harus menggunakan konfigurasi dari DHCP Server.
Client yang melalui House Harkonen mendapatkan range IP dari 192.239.1.14 - 192.239.1.28 dan 192.239.1.49 - 192.239.1.70
#### Penyelesaian 
- Melakaukan setup untuk Node **Mohiam.sh** ( DHCP Server )

## Result Nomor 2

## Soal 3
Client yang melalui House Atreides mendapatkan range IP dari 192.239.2.15 - 192.239.2.25 dan 192.239.2 .200 - 192.239.2.210

## Result Nomor 3

## Soal 4
Client mendapatkan DNS dari Princess Irulan dan dapat terhubung dengan internet melalui DNS tersebut 

## Result Nomor 4

## Soal 5 
Durasi DHCP server meminjamkan alamat IP kepada Client yang melalui House Harkonen selama 5 menit sedangkan pada client yang melalui House Atreides selama 20 menit. Dengan waktu maksimal dialokasikan untuk peminjaman alamat IP selama 87 menit 

## Result Nomor 5

## Soal 6
Seiring berjalannya waktu kondisi semakin memanas, untuk bersiap perang. Klan Harkonen melakukan deployment sebagai berikut
Vladimir Harkonen memerintahkan setiap worker(harkonen) PHP, untuk melakukan konfigurasi virtual host untuk website berikut dengan menggunakan php 7.3.

## Result Nomor 6

## Soal 7
Aturlah agar Stilgar dari fremen dapat dapat bekerja sama dengan maksimal, lalu lakukan testing dengan 5000 request dan 150 request/second.

## Result Nomor 7

## Soal 8 
Karena diminta untuk menuliskan peta tercepat menuju spice, buatlah analisis hasil testing dengan 500 request dan 50 request/second masing-masing algoritma Load Balancer dengan ketentuan sebagai berikut:
a. Nama Algoritma Load Balancer
b. Report hasil testing pada Apache Benchmark
c. Grafik request per second untuk masing masing algoritma. 
d. Analisis 

## Result Nomor 8

## Soal 9 
Dengan menggunakan algoritma Least-Connection, lakukan testing dengan menggunakan 3 worker, 2 worker, dan 1 worker sebanyak 1000 request dengan 10 request/second, kemudian tambahkan grafiknya pada peta.

## Result Nomor 9

## Soal 10 
Selanjutnya coba tambahkan keamanan dengan konfigurasi autentikasi di LB dengan dengan kombinasi username: “secmart” dan password: “kcksyyy”, dengan yyy merupakan kode kelompok. Terakhir simpan file “htpasswd” nya di /etc/nginx/supersecret/ 

## Result Nomor 10

## Soal 11 
Lalu buat untuk setiap request yang mengandung /dune akan di proxy passing menuju halaman https://www.dunemovie.com.au/.

## Result Nomor 11

## Soal 12
Selanjutnya LB ini hanya boleh diakses oleh client dengan IP 192.239.1.37, 192.239.1.67, 192.239.2.203, dan 192.239.2.207.

## Result Nomor 12

## Soal 13
Tidak mau kalah dalam perburuan spice, House atreides juga mengatur para pekerja di atreides.yyy.com.
Semua data yang diperlukan, diatur pada Chani dan harus dapat diakses oleh Leto, Duncan, dan Jessica.

## Soal 14
Leto, Duncan, dan Jessica memiliki atreides Channel sesuai dengan quest guide berikut. Jangan lupa melakukan instalasi PHP8.0 dan Composer

## Soal 15
atreides Channel memiliki beberapa endpoint yang harus ditesting sebanyak 100 request dengan 10 request/second. Tambahkan response dan hasil testing pada peta.
a. POST /auth/register

## Soal 16 
b. POST /auth/login

## Soal 17 
GET /me

## Soal 18 
Untuk memastikan ketiganya bekerja sama secara adil untuk mengatur atreides Channel maka implementasikan Proxy Bind pada Stilgar untuk mengaitkan IP dari Leto, Duncan, dan Jessica.

## Soal 19 
Untuk meningkatkan performa dari Worker, coba implementasikan PHP-FPM pada Leto, Duncan, dan Jessica. Untuk testing kinerja naikkan 
- pm.max_children
- pm.start_servers
- pm.min_spare_servers
- pm.max_spare_servers
sebanyak tiga percobaan dan lakukan testing sebanyak 100 request dengan 10 request/second kemudian berikan hasil analisisnya pada PDF.

## Soal 20 
Nampaknya hanya menggunakan PHP-FPM tidak cukup untuk meningkatkan performa dari worker maka implementasikan Least-Conn pada Stilgar. Untuk testing kinerja dari worker tersebut dilakukan sebanyak 100 request dengan 10 request/second.



