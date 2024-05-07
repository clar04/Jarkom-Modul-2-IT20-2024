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


## Soal 3
Para pasukan juga perlu mengetahui mana titik yang sedang di bombardir artileri, sehingga dibutuhkan domain lain yaitu redzone.xxxx.com dengan alias www.redzone.xxxx.com yang mengarah ke Severny
### Penyelesaian


## Soal 4
Markas pusat meminta dibuatnya domain khusus untuk menaruh informasi persenjataan dan suplai yang tersebar. Informasi persenjataan dan suplai tersebut mengarah ke Mylta dan domain yang ingin digunakan adalah loot.xxxx.com dengan alias www.loot.xxxx.com
### Penyelesaian


## Soal 5
Pastikan domain-domain tersebut dapat diakses oleh seluruh komputer (client) yang berada di Erangel
### Penyelesaian


## Soal 6
Beberapa daerah memiliki keterbatasan yang menyebabkan hanya dapat mengakses domain secara langsung melalui alamat IP domain tersebut. Karena daerah tersebut tidak diketahui secara spesifik, pastikan semua komputer (client) dapat mengakses domain redzone.xxxx.com melalui alamat IP Severny (Notes : menggunakan pointer record)
### Penyelesaian


## Soal 7
Akhir-akhir ini seringkali terjadi serangan siber ke DNS Server Utama, sebagai tindakan antisipasi kamu diperintahkan untuk membuat DNS Slave di Georgopol untuk semua domain yang sudah dibuat sebelumnya
### Penyelesaian


## Soal 8
Kamu juga diperintahkan untuk membuat subdomain khusus melacak airdrop berisi peralatan medis dengan subdomain medkit.airdrop.xxxx.com yang mengarah ke Lipovka
### Penyelesaian


## Soal 9
Terkadang red zone yang pada umumnya di bombardir artileri akan dijatuhi bom oleh pesawat tempur. Untuk melindungi warga, kita diperlukan untuk membuat sistem peringatan air raid dan memasukkannya ke domain siren.redzone.xxxx.com dalam folder siren dan pastikan dapat diakses secara mudah dengan menambahkan alias www.siren.redzone.xxxx.com dan mendelegasikan subdomain tersebut ke Georgopol dengan alamat IP menuju radar di Severny
### Penyelesaian


## Soal 10
Markas juga meminta catatan kapan saja pesawat tempur tersebut menjatuhkan bom, maka buatlah subdomain baru di subdomain siren yaitu log.siren.redzone.xxxx.com serta aliasnya www.log.siren.redzone.xxxx.com yang juga mengarah ke Severny
### Penyelesaian


## Soal 11

### Penyelesaian


## Soal 12

### Penyelesaian


## Soal 13

### Penyelesaian


## Soal 14

### Penyelesaian


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




