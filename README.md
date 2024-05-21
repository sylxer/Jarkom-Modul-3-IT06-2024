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
