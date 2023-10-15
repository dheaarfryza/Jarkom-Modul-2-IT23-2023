# Jarkom-Modul-2-IT23-2023
# Laporan Praktikum Modul 2 Jaringan Komputer
## Kelompok IT23
Anggota Kelompok :

5027211006 - Rendy Anfi Yudha

5027211013 - Dhea Arfryza Ananda Prasetyo

- [Soal 1](#soal-1)
- [Soal 2](#soal-2)
- [Soal 3](#soal-3)
- [Soal 4](#soal-4)
- [Soal 5](#soal-5)
- [Soal 7](#soal-7)
- [Soal 8](#soal-8)
- [Soal 9](#soal-9)
- [Soal 10](#soal-10)

### Soal 1
#### Description :
Membuat topologi berdasarkan pada folder drive yang diminta, yaitu topologi ke-2. Dengan Yudhistira sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna sebagai Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni.

#### Pengerjaan :
Berikut adalah hasil dari Topologi yang sudah dibuat :
![topologi(1)](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/967003e3-d590-4188-bd21-0e3238a69c54)
Dengan Yudhistira sebagai DNS Master nya dan Werkudara sebagai DNS Slave nya, serta Sadewa dan Nakula sebagai Client nya.


### Soal 2
#### Description :
Buatlah website utama dengan akses ke arjuna.it23.com dengan alias www.arjuna.it23.com 

#### Pengerjaan :
Install :
```
apt-get update
apt-get install bind9 -y
```

Membuka file di named.conf.local :
```nano /etc/bind/named.conf.local```

Code :
```bash
zone "arjuna.it23.com" {
	type master;
	file "/etc/bind/arjuna.it23.com";
};
```

Copy file db.local ke folder arjuna.it.23.com :
```cp /etc/bind/db.local /etc/bind/arjuna.it23.com```

Buka file arjuna.it23.com :
```nano /etc/bind/arjuna.it23.com```

Code :
```bash
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     arjuna.it23.com. root.arjuna.it23.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@           IN      NS      arjuna.it23.com.
@           IN      A       10.75.2.3 ; IP Arjuna
www         IN      CNAME   arjuna.it23.com.
@           IN      AAAA    ::1

```

Restart bind :
```service bind9 restart```

ping arjuna.it23.com dan www.arjuna.it23.com
```ping arjuna.it23.com```
![ping arjuna it23 com](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/05933456-e943-48b9-aa8a-ca6722b39e49)

```ping www.arjuna.it23.com```
![ping www arjuna it23 com](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/27e092ba-a98f-4e78-b1e8-221c444e08c4)


### Soal 1
#### Description :
Membuat topologi berdasarkan pada folder drive yang diminta, yaitu topologi ke-2. Dengan Yudhistira sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna sebagai Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni.

#### PoC :

### Soal 1
#### Description :
Membuat topologi berdasarkan pada folder drive yang diminta, yaitu topologi ke-2. Dengan Yudhistira sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna sebagai Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni.

#### PoC :

### Soal 1
#### Description :
Membuat topologi berdasarkan pada folder drive yang diminta, yaitu topologi ke-2. Dengan Yudhistira sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna sebagai Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni.

#### PoC :

### Soal 1
#### Description :
Membuat topologi berdasarkan pada folder drive yang diminta, yaitu topologi ke-2. Dengan Yudhistira sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna sebagai Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni.

#### PoC :
