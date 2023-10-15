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
Di Yudhistira DNS Master :

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

Di Sadewa Client :
ping arjuna.it23.com dan www.arjuna.it23.com

```ping arjuna.it23.com```
![ping arjuna it23 com](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/eb3d2857-6d10-4629-b1ab-ee66fc881704)

```ping www.arjuna.it23.com```
![ping www arjuna it23 com](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/41fdb8df-43b1-472f-ab12-f64a2308d5cb)


### Soal 3
#### Description :
Buatlah website utama dengan akses ke arjuna.it23.com dengan alias www.arjuna.it23.com 

#### Pengerjaan :
Membuka file di named.conf.local :
```nano /etc/bind/named.conf.local```

Code :
```bash
zone "arjuna.it23.com" {
	type master;
	file "/etc/bind/arjuna.it23.com";
};

zone "abimanyu.it23.com" {
	type master;
	file "/etc/bind/jarkom/abimanyu.it23.com";
};
```

Copy file db.local ke folder arjuna.it.23.com :
```cp /etc/bind/db.local /etc/bind/abimanyu.it23.com```

Buka file abimanyu.it23.com :
```nano /etc/bind/abimanyu.it23.com```

Code :
```bash
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.it23.com. root.abimanyu.it23.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@           IN      NS      abimanyu.it23.com.
@           IN      A       10.75.3.4 ; IP Abimanyu
www         IN      CNAME   abimanyu.it23.com.
@           IN      AAAA    ::1' > /etc/bind/abimanyu.it23.com


```

Restart bind :
```service bind9 restart```

Di Sadewa Client :
ping arjuna.it23.com dan www.arjuna.it23.com

```ping abimanyu.it23.com```
![ping abimanyu it23 com](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/a9d25198-c6f3-4d21-b2ad-300f5aa405a9)

```ping www.abimanyu.it23.com```
![ping www abimanyu it23 com](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/1acb66db-81d1-4b2b-a998-6bd55ae71348)


### Soal 4
#### Description :
Buatlah website utama dengan akses ke arjuna.it23.com dengan alias www.arjuna.it23.com 

#### Pengerjaan :


### Soal 5
#### Description :
Buatlah website utama dengan akses ke arjuna.it23.com dengan alias www.arjuna.it23.com 

#### Pengerjaan :
