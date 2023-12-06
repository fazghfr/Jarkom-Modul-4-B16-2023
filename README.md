# Jarkom-Modul-4-B16-2023
**Praktikum Jaringan Komputer Modul 4 Tahun 2023**

# Kelompok B16
| Nama | NRP |Github |
|---------------------------|------------|--------|
|Ahmad Fauzan A | 5025211091 | https://github.com/fazghfr |
|Syomeron Ansell W | 5025211250 | https://github.com/Ansell10 |

# Laporan Resmi

## Pembagian Subnet
![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/96367502/540db2c8-d7f0-4dc9-a0c5-bbd3ed1238ab)

# Ilustrasi Pembagian Subnet
![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/96367502/bbb502c8-7fe9-47a3-8b4c-79fa33613944)

# VLSM 
## Perhitungan VLSM

Diketahui subnet keseluruhan adalah /19. Maka diawali dengan **192.186.0.0/19**. Kemudian, kami disini akan sorting subnet secara descending pada
jumlah host setiap subnet ditambah 2. Penambahan 2 ini untuk memperhitungkan broadcast address dan juga NID.

Berikut sorted subnet : 

![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/96367502/540db2c8-d7f0-4dc9-a0c5-bbd3ed1238ab)

# Detail Perhitungan
Disini, akan kami jelaskan salah satu perhitungan pembagian ip menggunakan vlsm. Disini kami akan mendemokan perhitungan untuk subnet terbesar dan subnet pertama, yaitu **A1**.

**A1** Membutuhkan **1023 Host** + 2 = **1025 Host**. Merujuk pada tabel di modul : 

![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/96367502/aff1a5c7-9939-4a27-af3c-b821d5c413a2)

1025 Host membutuhkan subnet **/22** untuk mengakomodir kebutuhan A1. Untuk pembagian IP adalah sebagai berikut:

```
A1 menggunakan subnet /22
Berarti ada 22 bit untuk network dan 10 bit untuk host

Atau netmask : 11111111.11111111.11111100.00000000 -> 255.255.252.0

terlihat bahwa bit yang berubah hanya 10 bit terakhir (untuk host) dan pada oktet pertama dan kedua, tidak ada bit yang bisa dipakai untuk host. maka ip akan dimulai dari
192.168.x.x

kemudian, karena ada 10 bit untuk host, maka jumlah yang dialokasikan adalan 2^(10+1) = 2048

Karena subnet awal adalah 192.186.0.0/19,
untuk range awal A1 adalah 192.186.0.0/22
untuk range akhir A1 adalah range awal + 2048 host

atau jika dikonversikan menjadi ip maka
range awal 192.186.0.0/22
range akhir 192.186.7.255/22

Ini bisa kita cek, dimana dari oktet ke 0 - 1 ada 256 host,
maka 256x8 = 2048 -> sesuai dengan jumlah yang dialokasikan
```

Kemudian step yang sama dilakukan untuk mencari ip pada subnet subnet berikutnya. Berikut step-step yang kami rangkum untuk mencari range IP subnet :
- tentukan netmask menggunakan jumlah host (dapat merujuk pada tabel terlampir)
- menentukan jumlah alokasi ip yang tersedia (dapat merujuk pada tabel atau menggunakan perhitungan manual)
- range awal IP adalah [range terakhir ip]+1. contoh pada x step, range akhir adalah 192.186.7.255 maka x+1 awalnya adalah 192.186.8.0
- range akhir IP adalah [range awal] + jumlah alokasi

Step di atas dilakukan secara sekuensial mengikuti tabel subnet yang disortir berdasarkan jumlah host, sehingga mendapatkan pembagian sebagai berikut : 

![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/96367502/e32fc8c2-253f-42b0-b750-1a29bdf5811a)

## Routing VLSM

Untuk routing, terilustrasi sebagai berikut : 

![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/96367502/00440b33-38d8-488e-a69c-262256445a6a)

Panah hijau menunjukkan default routing tersebut kemana. Jadi jika suatu router mendapati ada paket ingin pergi ke suatu subnet 
yang router tersebut tidak memiliki routingnya, maka akan ditendang ke rute hijau ini.

merujuk pada fakta tersebut maka :
- Semua subnet pada sayap atas, router yang tahu semua arah adalah router Aura. Dimana jika turun satu level dari aura, maka router tersebut akan tahu routing ke subnet level bawahnya.
- Semua subnet pada sayap bawah, router yang tahu semua arah adalah router Eisen. Dimana jika turun satu level dari aura, maka router tersebut akan tahu routing ke subnet level bawahnya.

# CIDR
CIDR adalah singkatan dari Classless Inter-Domain Routing. Ini adalah metode untuk mengalamati dan merencanakan alamat IP dalam jaringan komputer. CIDR memungkinkan fleksibilitas dalam penggunaan alamat IP dengan memungkinkan subnetting, yaitu membagi jaringan besar menjadi jaringan yang lebih kecil.
 
Dalam CIDR, alamat IP ditulis dalam bentuk notasi, yang terdiri dari alamat IP itu sendiri diikuti oleh jumlah bit yang digunakan untuk menunjukkan bagian jaringan (subnet) dan bagian host. Notasi ini sering disebut sebagai "slash notation" atau "prefix length".
```
192.168.1.0/24
```
192.168.1.0 adalah alamat jaringan.
 
/24 menunjukkan bahwa 24 bit digunakan untuk bagian jaringan, menyisakan 8 bit untuk bagian host (karena alamat IPv4 memiliki total 32 bit).
 
Dengan menggunakan CIDR, administrator jaringan dapat mengelola penggunaan alamat IP secara lebih efisien dan membagi jaringan ke dalam sub-jaringan yang lebih kecil sesuai kebutuhan.
 
## Penggabungan IP - CIDR
### Node Awal
![1](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/dd53453e-9eab-4aa0-8c0c-157822de98c6)

### Penggabungan 1
![3](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/cca671ac-0e4f-45ee-91fc-ffd48aec1a2e)
![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/06ad610f-c9aa-44e2-91c5-339e571a8856)

### Penggabungan 2
![4](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/39aebcad-d1ad-4ddb-9906-af599faa377c)
![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/9553e7d7-92ae-4b34-bb83-1f27de85c619)


### Penggabungan 3
![5](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/7a0f10d7-4fc1-4c09-86e1-5f8c029d1194)
![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/831f3fb9-187e-4eff-981e-0e18a60836a9)


### Penggabungan 4
![6](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/e8728e67-5e54-46a3-91ca-c7ed4326ec83)
![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/e28a1488-a407-4969-a49d-b94f88849718)


### Penggabungan 5
![7](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/f6dca664-f1b2-4c73-8f3c-aed760468ed2)
![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/096d684d-c7f4-4085-b8b1-965cbb4301c1)


### Penggabungan 6
![8](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/e5f7cbe8-296c-426f-a5d6-a380f7f08385)
![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/352bd01e-851f-4725-8dcd-39f99bbec933)


### Penggabungan 7
![9](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/60db4b11-cf99-4b22-b72f-2a2fcdc9af91)
![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/9febf315-b945-45e3-9486-7e632bc9624c)


### Penggabungan 8
![10](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/95ea3c6a-4752-46ae-9b77-1a5db7a07b2d)
![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/91bc003f-56ff-429b-9bb2-5ba19ca61e01)


### Penggabungan 9
![11](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/aaa1870f-09e2-4e21-9a4b-d881aefbc854)
![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/5c40ad91-cbac-4dee-8447-f70bfb4ece1a)


### Penggabungan 10
![12](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/34cea64d-a5c2-42d6-b88e-7e0d4c72d4da)
![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/3477295e-6c6c-458b-86b2-c3f589e0f246)


### Penggabungan 11
![13](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/c80761af-c815-4921-bdf4-88c8002e94ce)
![image](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/1610e853-8a8c-498b-a80e-4935566c6491)


## Tree
![CIDR-tree new drawio](https://github.com/fazghfr/Jarkom-Modul-4-B16-2023/assets/114125933/b455f04b-2b7b-46e9-bf55-7d5ccd85a81c)

## Pembagian IP - CIDR
| Subnet | Network ID   | Netmask           | Broadcast        |
|--------|--------------|-------------------|------------------|
| A1     | 192.186.16.0 | 255.255.248.0     | 192.186.23.255   |
| A2     | 192.186.0.0  | 255.255.252.0     | 192.186.3.255    |
| A3     | 192.187.0.0  | 255.255.252.0     | 192.187.3.255    |
| A4     | 192.194.0.0  | 255.255.252.0     | 192.194.3.255    |
| A5     | 192.194.16.0 | 255.255.254.0     | 192.194.17.255   |
| A6     | 192.195.0.0  | 255.255.255.0     | 192.195.0.255    |
| A7     | 192.190.0.0  | 255.255.255.0     | 192.190.0.255    |
| A8     | 192.194.128.0| 255.255.255.224   | 192.194.128.63   |
| A9     | 192.186.4.0  | 255.255.255.248   | 192.186.4.31     |
| A10    | 192.186.32.0 | 255.255.255.248   | 192.186.32.7     |
| A11    | 192.194.4.0  | 255.255.255.192   | 192.194.4.7      |
| A12    | 192.186.8.0  | 255.255.255.252   | 192.186.8.3      |
| A13    | 192.186.4.4  | 255.255.255.252   | 192.186.4.7      |
| A14    | 192.194.64.0 | 255.255.255.252   | 192.194.64.3     |
| A15    | 192.186.128.0| 255.255.255.252   | 192.186.128.3    |
| A16    | 192.198.0.0  | 255.255.255.252   | 192.198.0.3      |
| A17    | 192.196.0.0  | 255.255.255.252   | 192.196.0.3      |
| A18    | 192.188.0.0  | 255.255.255.252   | 192.188.0.3      |
| A19    | 192.186.64.0 | 255.255.255.252   | 192.186.64.3     |
| A20    | 192.194.32.0 | 255.255.255.252   | 192.194.32.3     |
| A21    | 192.194.8.0  | 255.255.255.252   | 192.194.8.3      |
| L1     | 192.186.0.0  | 255.240.0.0       | 192.201.255.255  |
| K1     | 192.186.0.0  | 255.248.0.0       | 192.193.255.255  |
| J2     | 192.186.0.0  | 255.252.0.0       | 192.189.255.255  |
| I2     | 192.186.0.0  | 255.254.0.0       | 192.187.255.255  |
| H2     | 192.186.0.0  | 255.255.0.0       | 192.186.255.255  |
| G2     | 192.186.0.0  | 255.255.128.0     | 192.186.127.255  |
| F2     | 192.186.0.0  | 255.255.192.0     | 192.186.63.255   |
| E2     | 192.186.0.0  | 255.255.224.0     | 192.186.31.255   |
| D2     | 192.186.0.0  | 255.255.240.0     | 192.186.15.255   |
| C2     | 192.186.0.0  | 255.255.255.0     | 192.186.7.255    |
| B2     | 192.186.0.0  | 255.255.255.128   | 192.186.3.255    |
| J1     | 192.194.0.0  | 255.252.0.0       | 192.197.255.255  |
| I1     | 192.194.0.0  | 255.254.0.0       | 192.195.255.255  |
| H1     | 192.194.0.0  | 255.255.0.0       | 192.194.255.255  |
| G1     | 192.194.0.0  | 255.255.128.0     | 192.194.127.255  |
| F1     | 192.194.0.0  | 255.255.192.0     | 192.194.63.255   |
| E1     | 192.194.0.0  | 255.255.224.0     | 192.194.31.255   |
| D1     | 192.194.0.0  | 255.255.240.0     | 192.194.15.255   |
| C2     | 192.194.0.0  | 255.255.255.0     | 192.194.7.255    |
| B1     | 192.194.0.0  | 255.255.255.128   | 192.194.3.255    |


## Config GNS
- Fren
```
#A12
auto eth0
iface eth0 inet static
address 192.186.8.1
netmask 255.255.255.252

#A1
auto eth1
iface eth1 inet static
address 192.186.8.1
netmask 255.255.255.252
```

- AppetitRegion
```
auto eth0
iface eth0 inet static
	address 192.186.16.10
	netmask 255.255.248.0
	gateway 192.186.16.1
```

- LaubHills
```
auto eth0
iface eth0 inet static
	address 192.186.19.10
	netmask 255.255.248.0
	gateway 192.186.16.1
```

- Flamme
```
#A14
auto eth0
iface eth0 inet static
address 192.194.64.1
netmask 255.255.255.252

#A13
auto eth1
iface eth1 inet static
address 192.186.4.5
netmask 255.255.255.252

#A2
auto eth2
iface eth2 inet static
address 192.186.0.1
netmask 255.255.252.0

#A12
auto eth3
iface eth3 inet static
address 192.186.8.2
netmask 255.255.255.252
```

- RohrRoad
```
#A2
auto eth0
iface eth0 inet static
address 192.186.0.2
netmask 255.255.252.0
gateway 192.186.0.1
```

- Himmel
```
#A13
auto eth0
iface eth0 inet static
address 192.186.4.6
netmask 255.255.255.252

#A9
auto eth1
iface eth1 inet static
address 192.186.4.1
netmask 255.255.255.248
```

- SchwerMountains
```
auto eth0
iface eth0 inet static
address 192.186.4.2
netmask 255.255.255.248
gateway 192.186.4.1
```

- Frieren
```
#A15
auto eth0
iface eth0 inet static
address 192.186.128.0
netmask 255.255.255.252

#A14
auto eth1
iface eth1 inet static
address 192.194.64.0
netmask 255.255.255.252

#A8
auto eth2
iface eth2 inet static
address 192.194.128.1
netmask 255.255.255.224
```
- LakeKorridor
```
#A8
auto eth0
iface eth0 inet static
address 192.194.128.2
netmask 255.255.255.224
gateway 192.194.128.1
```

- Aura
```
auto eth0
iface eth0 inet dhcp

#A15
auto eth1
iface eth1 inet static
address 192.186.8.1
netmask 255.255.255.252

#A16
auto eth2
iface eth2 inet static
address 192.198.0.1
netmask 255.255.255.252

#A17
auto eth3
iface eth3 inet static
address 192.196.0.1
netmask 255.255.255.252
```

- Denken
```
#A16
auto eth0
iface eth0 inet static
address 192.198.0.2
netmask 255.255.255.252

#A7
auto eth1
iface eth1 inet static
address 192.190.0.1
netmask 255.255.255.0
```

- RoyalCapital
```
#A7
auto eth0
iface eth0 inet static
address 192.190.0.2
netmask 255.255.255.0
gateway 192.190.0.1
```

- WilleRegion
```
#A7
auto eth0
iface eth0 inet static
address 192.190.0.67
netmask 255.255.255.0
gateway 192.190.0.1
```

- Eisen
```
#A17
auto eth0
iface eth0 inet static
address 192.196.0.2
netmask 255.255.255.252

#A10
auto eth1
iface eth1 inet static
address 192.186.32.1
netmask 255.255.255.248

#A18
auto eth2
iface eth2 inet static
address 192.188.0.1
netmask 255.255.255.252

#A19
auto eth3
iface eth3 inet static
address 192.186.64.0
netmask 255.255.255.252

#A20
auto eth4
iface eth4 inet static
address 192.194.32.0
netmask 255.255.255.252
```

- Richter 
```
auto eth0
iface eth0 inet static
address 192.186.32.2
netmask 255.255.252.0
gateway 192.186.32.1
```

- Revolte
```
auto eth0
iface eth0 inet static
address 192.186.32.5
netmask 255.255.252.0
gateway 192.186.32.1
```

- Stark
```
auto eth0
iface eth0 inet static
address 192.188.0.2
netmask 255.255.252.0
gateway 192.188.0.1
```

- Lugner
```

#A19
auto eth0
iface eth0 inet static
address 192.186.64.2
netmask 255.255.255.252

#A3
auto eth1
iface eth1 inet static
address 192.187.0.1
netmask 255.255.252.0

#A6
auto eth2
iface eth2 inet static
address 192.195.0.1
netmask 255.255.255.0
```

- TurkRegion
```
#A3
auto eth0
iface eth0 inet static
address 192.187.0.2
netmask 255.255.252.0
gateway 192.187.0.1
```

- GrobeForest
```
#A6
auto eth0
iface eth0 inet static
address 192.195.0.2
netmask 255.255.255.0
gateway 192.195.0.1
```

- Linie
```
auto lo
iface lo inet loopback

#A20
auto eth0
iface eth0 inet static
address 192.194.32.1
netmask 255.255.255.252

#A5
auto eth1
iface eth1 inet static
address 192.194.16.1
netmask 255.255.254.0

#A21
auto eth2
iface eth2 inet static
address 192.194.8.1
netmask 255.255.255.252
```

- GranzChannel
```
#A5
auto eth0
iface eth0 inet static
address 192.194.16.2
netmask 255.255.254.0
gateway 192.194.16.1
```

- Lawine
```
#A21
auto eth2
iface eth2 inet static
address 192.194.8.2
netmask 255.255.255.252

#A11
auto eth1
iface eth1 inet static
address 192.194.4.1
netmask 255.255.255.192
```

- BredRegion
```
auto eth0
iface eth0 inet static
address 192.194.4.2
netmask 255.255.255.192
gateway 192.194.4.1
```

- Heiter
```
#A11
auto eth0
iface eth0 inet static
address 192.194.4.6
netmask 255.255.255.192

#A4
auto eth1
iface eth1 inet static
address 192.194.0.1
netmask 255.255.252.0
```

- Sein
```
#A4
auto eth0
iface eth0 inet static
address 192.194.0.2
netmask 255.255.252.0
gateway 192.194.0.1
```

-RiegelCanyon
```
#A4
auto eth0
iface eth0 inet static
address 192.194.0.200
netmask 255.255.252.0
gateway 192.194.0.1
```