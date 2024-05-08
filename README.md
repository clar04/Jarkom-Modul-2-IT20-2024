# Jarkom-Modul-2-IT20-2024
Laporan Resmi Praktikum Jaringan Komputer Modul 2

**Kelompok IT20**
| Nama | NRP |
|-----------------------|--------------|
| Clara Valentina | 5027221016 |
| Muhammad Arsy Athallah| 5027221048 |

### Konfigurasi Awal
#### Prefix IP IT20
`192.243`
#### List IP 
`192.168.122.1` = Erangel
`192.243.1.2` = Zharki
`192.243.1.3` = YasnayaPolyana
`192.243.1.4` = Primorsk
`192.243.3.2` = Pochinki
`192.243.4.2` = Georgopol
`192.243.2.2` = Severny
`192.243.2.3` = Lipovka
`192.243.2.4` = Stalber
`192.243.2.5` = MyIta
#### Konfigurasi Erangel (Router)
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.243.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.243.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.243.3.1
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 192.243.4.1
	netmask 255.255.255.0
```
#### Konfigurasi Zharki (Client)
```
auto eth0
iface eth0 inet static
	address 192.243.1.2
	netmask 255.255.255.0
	gateway 192.243.1.1
```
#### Konfigurasi YasnayaPolyana (Client)
```
auto eth0
iface eth0 inet static
	address 192.243.1.3
	netmask 255.255.255.0
	gateway 192.243.1.1
```
#### Konfigurasi Primorsk (Client)
```
auto eth0
iface eth0 inet static
	address 192.243.1.4
	netmask 255.255.255.0
	gateway 192.243.1.1
```
### Konfigurasi Pochinki (DNS Master)
```
auto eth0
iface eth0 inet static
	address 192.243.3.2
	netmask 255.255.255.0
	gateway 192.243.3.1
```
### Konfigurasi Georgopol (DNS Slave)
```
auto eth0
iface eth0 inet static
	address 192.243.4.2
	netmask 255.255.255.0
	gateway 192.243.4.1
```
### Konfigurasi Severny (Web Server)
```
auto eth0
iface eth0 inet static
	address 192.243.2.2
	netmask 255.255.255.0
	gateway 192.243.2.1
```
### Konfigurasi Lipovka (Web Server)
```
auto eth0
iface eth0 inet static
	address 192.243.2.3
	netmask 255.255.255.0
	gateway 192.243.2.1
```
### Konfigurasi Stalber (Web Server)
```
auto eth0
iface eth0 inet static
	address 192.243.2.4
	netmask 255.255.255.0
	gateway 192.243.2.1
```
### Konfigurasi MyIta (Load Balancer) 
```
auto eth0
iface eth0 inet static
	address 192.243.2.5
	netmask 255.255.255.0
	gateway 192.243.2.1
```

### Topologi 5
#### Contoh
![05](https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/245ab361-1b40-4554-95e7-5cf653f56c29)


#### Punya IT20
![Screenshot 2024-05-03 000733](https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/ddb45e4e-fff4-4e30-96f2-fd474a538bdb)

## Soal 1
Untuk membantu pertempuran di Erangel, kamu ditugaskan untuk membuat jaringan komputer yang akan digunakan sebagai alat komunikasi. Sesuaikan rancangan Topologi dengan rancangan dan pembagian yang berada di link yang telah disediakan, dengan ketentuan nodenya sebagai berikut :
- DNS Master akan diberi nama Pochinki, sesuai dengan kota tempat dibuatnya server tersebut
- Karena ada kemungkinan musuh akan mencoba menyerang Server Utama, maka buatlah DNS Slave Georgopol yang mengarah ke Pochinki
- Markas pusat juga meminta dibuatkan tiga Web Server yaitu Severny, Stalber, dan Lipovka. Sedangkan Mylta akan bertindak sebagai Load Balancer untuk server-server tersebut 
### Penyelesaian 


## Soal 2
Karena para pasukan membutuhkan koordinasi untuk mengambil airdrop, maka buatlah sebuah domain yang mengarah ke Stalber dengan alamat airdrop.xxxx.com dengan alias www.airdrop.xxxx.com dimana xxxx merupakan kode kelompok.
### Penyelesaian

```
zone "airdrop.it20.com" {
	type master;
	file "/etc/bind/jarkom/airdrop.it20.com";
};
```

```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     airdrop.it20.com. root.airdrop.it20.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      airdrop.it20.com.
@       IN      A       192.243.2.4 //Stalber
www     IN      CNAME   airdrop.it20.com
```

## Soal 3
Para pasukan juga perlu mengetahui mana titik yang sedang di bombardir artileri, sehingga dibutuhkan domain lain yaitu redzone.xxxx.com dengan alias www.redzone.xxxx.com yang mengarah ke Severny
### Penyelesaian
```
zone "redzone.it20.com" {
	type master;
	file "/etc/bind/jarkom/redzone.it20.com";
};
```

```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     redzone.it20.com. root.redzone.it20.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      redzone.it20.com.
@       IN      A       192.243.2.2 //serverny
www     IN      CNAME   redzone.it20.com.
```


## Soal 4
Markas pusat meminta dibuatnya domain khusus untuk menaruh informasi persenjataan dan suplai yang tersebar. Informasi persenjataan dan suplai tersebut mengarah ke Mylta dan domain yang ingin digunakan adalah loot.xxxx.com dengan alias www.loot.xxxx.com
### Penyelesaian
```
zone "loot.it20.com" {
	type master;
	file "/etc/bind/jarkom/loot.it20.com";
};
```

```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     loot.it20.com. root.loot.it20.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      loot.it20.com.
@       IN      A       192.243.2.5 //MyIta
www     IN      CNAME   loot.it20.com.
```


## Soal 5
Pastikan domain-domain tersebut dapat diakses oleh seluruh komputer (client) yang berada di Erangel
### Penyelesaian
SS dokumentasi 

## Soal 6
Beberapa daerah memiliki keterbatasan yang menyebabkan hanya dapat mengakses domain secara langsung melalui alamat IP domain tersebut. Karena daerah tersebut tidak diketahui secara spesifik, pastikan semua komputer (client) dapat mengakses domain redzone.xxxx.com melalui alamat IP Severny (Notes : menggunakan pointer record)
### Penyelesaian
```
zone "2.243.192.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/2.243.192.in-addr.arpa";
};
```
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     redzone.it20.com. root.redzone.it20.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
2.243.192.in-addr.arpa.       IN      NS      redzone.it20.com.
2                             IN      PTR     redzone.it20.com.
'
```


## Soal 7
Akhir-akhir ini seringkali terjadi serangan siber ke DNS Server Utama, sebagai tindakan antisipasi kamu diperintahkan untuk membuat DNS Slave di Georgopol untuk semua domain yang sudah dibuat sebelumnya
### Penyelesaian
```
zone "airdrop.it20.com" {
    type master;
    notify yes;
    also-notify { 192.243.4.2; };  //georgopol
    allow-transfer { 192.243.4.2; };
    file "/etc/bind/jarkom/airdrop.it20.com";
};
zone "redzone.it20.com" {
    type master;
    notify yes;
    also-notify { 192.243.4.2; }; 
    allow-transfer { 192.243.4.2; };
    file "/etc/bind/jarkom/redzone.it20.com";
};
zone "loot.it20.com" {
    type master;
    notify yes;
    also-notify { 192.243.4.2; }; 
    allow-transfer { 192.243.4.2; };
    file "/etc/bind/jarkom/loot.it20.com";
};
zone "2.243.192.in-addr.arpa" {
    type master;
    notify yes;
    also-notify { 192.243.4.2; }; 
    allow-transfer { 192.243.4.2; };
    file "/etc/bind/jarkom/2.243.192.in-addr.arpa";
};
```
```
zone "airdrop.it20.com" {
    type slave;
    notify yes;
    also-notify {192.243.3.2; };   //pochinki
    allow-transfer { 192.243.3.2; };
    file "/etc/bind/jarkom/airdrop.it20.com";
};
zone "redzone.it20.com" {
    type slave;
    notify yes;
    also-notify { 192.243.3.2; }; 
    allow-transfer { 192.243.3.2; };
    file "/etc/bind/jarkom/redzone.it20.com";
};
zone "loot.it20.com" {
    type slave;
    notify yes;
    also-notify { 192.243.3.2; }; 
    allow-transfer { 192.243.3.2; };
    file "/etc/bind/jarkom/loot.it20.com";
};
zone "3.243.192.in-addr.arpa" {
    type slave;
    notify yes;
    also-notify { 192.243.3.2; }; 
    allow-transfer { 192.243.3.2; };
    file "/etc/bind/jarkom/3.243.192.in-addr.arpa";
};
```

## Soal 8
Kamu juga diperintahkan untuk membuat subdomain khusus melacak airdrop berisi peralatan medis dengan subdomain medkit.airdrop.xxxx.com yang mengarah ke Lipovka
### Penyelesaian
```
'zone "airdrop.it20.com" {
	type master;
	file "/etc/bind/jarkom/airdrop.it20.com";
};
```

```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     airdrop.it20.com. root.airdrop.it20.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      airdrop.it20.com.
@       IN      A       192.243.2.4 //stalber 
medkit  IN      A       192.243.2.3 //lipovka
www     IN      CNAME   airdrop.it20.com.
```

## Soal 9
Terkadang red zone yang pada umumnya di bombardir artileri akan dijatuhi bom oleh pesawat tempur. Untuk melindungi warga, kita diperlukan untuk membuat sistem peringatan air raid dan memasukkannya ke domain siren.redzone.xxxx.com dalam folder siren dan pastikan dapat diakses secara mudah dengan menambahkan alias www.siren.redzone.xxxx.com dan mendelegasikan subdomain tersebut ke Georgopol dengan alamat IP menuju radar di Severny
### Penyelesaian


## Soal 10
Markas juga meminta catatan kapan saja pesawat tempur tersebut menjatuhkan bom, maka buatlah subdomain baru di subdomain siren yaitu log.siren.redzone.xxxx.com serta aliasnya www.log.siren.redzone.xxxx.com yang juga mengarah ke Severny
### Penyelesaian
Untuk menambahkan `log` kita bisa menambahkan code berikut pada `/etc/bind/delegasi/siren.redzone.it20.com` seperti berikut:
~~~
log     IN      A       10.66.1.2
www.log IN      CNAME   www.siren.redzone.it05.com.
~~~

## Soal 11
Setelah pertempuran mereda, warga Erangel dapat kembali mengakses jaringan luar, tetapi hanya warga Pochinki saja yang dapat mengakses jaringan luar secara langsung. Buatlah konfigurasi agar warga Erangel yang berada diluar Pochinki dapat mengakses jaringan luar melalui DNS Server Pochinki
### Penyelesaian
~~~
options {
    directory "/var/cache/bind";

    // If there is a firewall between you and nameservers you want
    // to talk to, you may need to fix the firewall to allow multiple
    // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

    // If your ISP provided one or more IP addresses for stable
    // nameservers, you probably want to use them as forwarders.
    // Uncomment the following block, and insert the addresses replacing
    // the all-0's placeholder.

    forwarders {
          192.168.122.1;
     };

    //========================================================================
    // If BIND logs error messages about the root key being expired,
    // you will need to update your keys.  See https://www.isc.org/bind-keys
//========================================================================
    //dnssec-validation auto;
    allow-query {any;};

    auth-nxdomain no;
    listen-on-v6 { any; };
};
~~~
etc/bind/named.conf.options

![image](https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/128389289/30669139-20e4-4cab-a371-e4b8b54bcd10)

![image](https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/128389289/d2f58014-70d0-48e8-b6da-4e6065a3f085)

![image](https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/128389289/4b747eb5-6dd7-4815-9ac4-c1f6eb5c990b)

![image](https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/128389289/4f791ec5-d5cc-4d9f-8acb-0646cebbeb1c)


## Soal 12

### Penyelesaian


## Soal 13

### Penyelesaian


## Soal 14
Mereka juga belum merasa puas jadi pusat meminta agar web servernya dan load balancer nya diubah menjadi nginx
### Penyelesaian
Jadi kita akan merubah dari apache menjadi nginx dengan menjalankan script pada severny, lipovka, dan stalber denagnmenggunakan script sebagai berikut:
~~~
server {
    listen 8002;
    root /var/www/html/mylta.it05.com/;
    index index.php index.html index.htm;

    server_name mylta.it05.com;

    location / {
        try_files $uri $uri/ /index.php$is_args$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}

server {
    listen 8002;
    server_name www.mylta.it05.com;  

    root /var/www/html/www.mylta.it05.com/;  

}
~~~
Setelah itu kita jalankan dengan command `service nginx restart`

## Soal 15

### Penyelesaian


## Soal 16

### Penyelesaian


## Soal 17

### Penyelesaian


## Soal 18

### Penyelesaian


## Soal 19

### Penyelesaian


## Soal 20

### Penyelesaian




