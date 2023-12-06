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
| A8     | 192.194.128.0| 255.255.255.192   | 192.194.128.63   |
| A9     | 192.186.4.0  | 255.255.255.224   | 192.186.4.31     |
| A10    | 192.186.32.0 | 255.255.255.248   | 192.186.32.7     |
| A11    | 192.194.4.0  | 255.255.255.248   | 192.194.4.7      |
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


## Penggabungan IP - CIDR


## Config GNS
