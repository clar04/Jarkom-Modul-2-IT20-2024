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
Pada Erangel dibuat suatu file erangel.sh yang berisi 
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.243.0.0/16
echo nameserver 192.168.122.1 > /etc/resolv.conf

```
Pada DNS Master (Pochinki) dan DNS Slave (Georgopol), masing-masing dibuat file poc.sh pada Pochinki dan geo.sh pada Georgopol yang berisi 
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install bind9 -y
```
Pada  setiap client, masing-masing dibuat file zharki.sh pada Zharki, yas.sh pada YasnayaPolyana, dan prim.sh pada Primorsk  yang berisi 
```
echo ‘nameserver 192.243.3.2       
nameserver 192.243.4.2’ > /etc/resolv.conf
apt-get update
apt-get install dnsutils -y
apt-get install lynx -y
apt-get install bind9 -y
```
Nameserver yang diinput merupakan IP dari DNS Master (Pochinki) `192.243.3.2` dan IP dari DNS Slave (Georgopol) `192.243.4.2` 

#### Dokumentasi test ping google.com pada masing-masing client
Pada client Zharki

<img width="583" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/ffb6fba1-8742-4b63-a260-2abc2b0277ad">


Pada client YasnayaPolyana

<img width="576" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/8e93ed75-802c-4d9f-851c-1c57688bff47">


Pada client Primorsk 

<img width="578" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/5da3677c-b687-4336-9b8a-076578393513">





## Soal 2
Karena para pasukan membutuhkan koordinasi untuk mengambil airdrop, maka buatlah sebuah domain yang mengarah ke Stalber dengan alamat airdrop.xxxx.com dengan alias www.airdrop.xxxx.com dimana xxxx merupakan kode kelompok.
### Penyelesaian
Pada node Pochinki membuat file soal2.sh yang berisikan script berikut untuk nantinya disimpan pada  file /etc/bind/named.conf.local
```
zone "airdrop.it20.com" {
	type master;
	file "/etc/bind/jarkom/airdrop.it20.com";
        
};
```
kemudian script berikut pada /etc/bind/jarkom/airdrop.it20.com dengan IP yang mengarah pada Stalber
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
Pada node Pochinki membuat file soal3.sh yang berisikan script berikut untuk nantinya disimpan pada  file /etc/bind/named.conf.local
```
zone "redzone.it20.com" {
	type master;
	file "/etc/bind/jarkom/redzone.it20.com";
};
```
kemudian script berikut pada /etc/bind/jarkom/redzone.it20.com dengan IP yang mengarah pada Serverny
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
Pada DNS Master pochinki  membuat file soal4.sh berisikan
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
##### airdrop.it20.com dan www.airdrop.it20.com  pada masing-masing client

<img width="474" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/7d25c1a8-4801-4cc7-9f9c-a11c67808e15">


<img width="434" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/9aac3328-575e-462b-ba2e-d7d9d53edde2">


<img width="431" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/2b5e5ede-584d-4146-9975-5d9f560eae14">


##### redzone.it20.com www.redzone.it20.com pada masing-masing client

<img width="479" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/0506b7b5-ef29-40a0-8639-53305e92a3a1">


<img width="410" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/a1c4c3ab-3b8e-4418-89fc-183191bc81f7">


<img width="424" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/5b634bea-d7ad-4cfe-b9ec-840051278301">


##### loot.it20.com www.loot.it20.com pada masing-masing client

<img width="422" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/16639813-b911-46e8-9a5e-65551c7e0a75">


<img width="412" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/942c6213-5f8e-4851-8bd3-11ce39b27816">


<img width="412" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/8547d335-205a-4ad8-9b6a-93da3d1353ca">




## Soal 6
Beberapa daerah memiliki keterbatasan yang menyebabkan hanya dapat mengakses domain secara langsung melalui alamat IP domain tersebut. Karena daerah tersebut tidak diketahui secara spesifik, pastikan semua komputer (client) dapat mengakses domain redzone.xxxx.com melalui alamat IP Severny (Notes : menggunakan pointer record)

Pada DNS Master pochinki  membuat file soal6.sh berisikan
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
#### Dokumentasi pada setiap client
<img width="372" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/723ff549-3641-4f17-bfc8-9cf5960d3737">


<img width="353" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/20df55e6-a4eb-411f-8061-41ac6715fbea">


<img width="354" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/ee495ca0-c922-412a-91ad-47aac53ee0d4">





## Soal 7
Akhir-akhir ini seringkali terjadi serangan siber ke DNS Server Utama, sebagai tindakan antisipasi kamu diperintahkan untuk membuat DNS Slave di Georgopol untuk semua domain yang sudah dibuat sebelumnya
### Penyelesaian

Pada DNS Master pochinki  membuat file soal7.sh berisikan
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

#### Dokumentasi
Stop bind9 pada Pochinki terlebih dahulu
<img width="725" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/a79c3366-778d-4f37-8402-ab110a08ebf3">


Kemudian menjalankan soal7.sh pada georgopol 
<img width="727" alt="image" src="https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/0c1c7abb-5ae8-4d6b-8c16-28250a83011e">


Lalu mengecek dengan ping pada setiap domain yang telah dibuat sebelumnya pada client Zharki

![Screenshot 2024-05-04 062744](https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/3019ddff-6e36-4cfb-9cbb-d7100628f2a7)



## Soal 8
Kamu juga diperintahkan untuk membuat subdomain khusus melacak airdrop berisi peralatan medis dengan subdomain medkit.airdrop.xxxx.com yang mengarah ke Lipovka

### Penyelesaian
Memuat file soal8.sh berisi konfig berikut
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

#### Dokumentasi
![Screenshot 2024-05-04 094412](https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/123356941/b91e8f55-fae2-4052-829f-900c94fcd451)



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
Untuk konfigurasi agar warga Erangel yang berada diluar Pochinki dapat mengakses jaringan luar melalui DNS Server Pochinki, kita bisa menggunakan port forwarding IP 192.168.122.1 dalam file /etc/bind/named.conf.options pada node Pochinki sebagai berikut:
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


## Soal 12

### Penyelesaian
Untuk mendeploy website menggunakan apache, lakukan config pada file /etc/apache2/sites-available/default
~~~
server {
    listen 8002;
    root /var/www/html/mylta.it20.com/;
    index index.php index.html index.htm;

    server_name mylta.it20.com;
    server_alias www.mylta.it20.com

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
~~~

## Soal 13
Tapi pusat merasa tidak puas dengan performanya karena traffic yang tinggi maka pusat meminta kita memasang load balancer pada web nya, dengan Severny, Stalber, Lipovka sebagai worker dan Mylta sebagai Load Balancer menggunakan apache sebagai web server nya dan load balancer nya
### Penyelesaian
Pada bagian Web Server yaitu Stalber, severny, dan lipovka kita bisa membuat script yang berfungsi sebagai web server dengan script sebagai berikut:
~~~
echo nameserver 192.168.122.1 > /etc/resolv.conf

apt-get update
apt-get install lynx apache2 php libapache2-mod-php7.0 nginx -y

echo nameserver 192.243.3.2 > /etc/resolv.conf

echo '
<VirtualHost *:8080>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/jarkom-it20
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
' > /etc/apache2/sites-available/jarkom-it20.conf

echo '
Listen 80
Listen 8080

<IfModule ssl_module>
        Listen 443
</IfModule>

<IfModule mod_gnutls.c>
        Listen 443
</IfModule>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
' > /etc/apache2/ports.conf

mkdir /var/www/jarkom-it20

cp /root/index.php /var/www/jarkom-it20/index.php

a2enmod proxy
a2enmod proxy_http

cd /etc/apache2/sites-available

a2ensite jarkom-it20.conf

cd /root

service apache2 restart
~~~
Setelah itu kita jalankan dengan menggunakan `bash script.sh` lalu kita masuk ke MyIta untuk membuat Script yang berfungsi sebagai `Load Balancer` dengan script sebagai berikut:
~~~
echo nameserver 192.168.122.1 > /etc/resolv.conf

apt-get update
apt-get install lynx apache2 php libapache2-mod-php7.0 nginx -y

echo nameserver 192.243.3.2 > /etc/resolv.conf

echo '
<VirtualHost *:8080>
        <proxy balancer://jarkombalancer>
                BalancerMember http://192.243.2.2:8080
                BalancerMember http://192.243.2.3:8080
                BalancerMember http://192.243.2.4:8080
                ProxySet lbmethod=bytraffic
        </proxy>
        ProxyPreserveHost On
        ProxyPass / balancer://jarkombalancer/
        ProxyPassReverse / balancer://jarkombalancer/
</VirtualHost>
' > /etc/apache2/sites-available/jarkom-it20.conf

echo '
Listen 80
Listen 8080

<IfModule ssl_module>
        Listen 443
</IfModule>

<IfModule mod_gnutls.c>
        Listen 443
</IfModule>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
' > /etc/apache2/ports.conf

a2enmod proxy
a2enmod proxy_http
a2enmod proxy_balancer
a2enmod lbmethod_bytraffic

cd /etc/apache2/sites-available

a2ensite jarkom-it20.conf

cd /root

service apache2 restart
~~~
Setelah load balancer di jalankan kita masuk ke salah satu client seperti zharki dan disitu kita akan mengetes dengan menggunakan command `lynx [IP Client]` yang tampilan nya sebagai berikut:
![image](https://github.com/clar04/Jarkom-Modul-2-IT20-2024/assets/128389289/862d38ff-ac93-4465-b0b6-e0d0f13bcba6)



## Soal 14
Mereka juga belum merasa puas jadi pusat meminta agar web servernya dan load balancer nya diubah menjadi nginx
### Penyelesaian
Jadi kita akan merubah dari apache menjadi nginx dengan menjalankan script pada severny, lipovka, dan stalber dengan menggunakan script sebagai berikut:
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




