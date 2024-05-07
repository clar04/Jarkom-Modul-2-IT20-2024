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
