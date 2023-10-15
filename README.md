## Laporan Praktikum Modul 2 Jaringan Komputer
## Kelompok IT23
Anggota Kelompok :

5027211006 - Rendy Anfi Yudha

5027211013 - Dhea Arfryza Ananda Prasetyo

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

### Soal 1
#### Description :
Membuat topologi berdasarkan pada folder drive yang diminta, yaitu topologi ke-2. Dengan Yudhistira sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna sebagai Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni.

#### Pengerjaan :
Berikut adalah hasil dari Topologi yang sudah dibuat :
![topologi(1)](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/967003e3-d590-4188-bd21-0e3238a69c54)
Dengan Yudhistira sebagai DNS Master nya dan Werkudara sebagai DNS Slave nya, serta Sadewa dan Nakula sebagai Client nya.

Configure Pandudewanata :
```bash
# Static config for eth0
auto eth0
iface eth0 inet dhcp

# Static config for eth1
auto eth1
iface eth1 inet static
	address 10.75.1.1
	netmask 255.255.255.0

# Static config for eth2
auto eth2
iface eth2 inet static
	address 10.75.2.1
	netmask 255.255.255.0

# Static config for eth3
auto eth3
iface eth3 inet static
	address 10.75.3.1
	netmask 255.255.255.0

```

Yudhistira :
```bash
auto eth0
iface eth0 inet static
	address 10.75.3.2
	netmask 255.255.255.0
	gateway 10.75.3.1
```

Werkudara :
```bash
auto eth0
iface eth0 inet static
	address 10.75.2.2
	netmask 255.255.255.0
	gateway 10.75.2.1
```

Arjuna :
```bash
auto eth0
iface eth0 inet static
	address 10.75.2.3
	netmask 255.255.255.0
	gateway 10.75.2.1
```

Abimanyu :
```bash
auto eth0
iface eth0 inet static
	address 10.75.2.4
	netmask 255.255.255.0
	gateway 10.75.2.1
```


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
```cp /etc/bind/db.local /etc/bind/it23/arjuna.it23.com```

Buka file arjuna.it23.com :
```nano /etc/bind/it23/arjuna.it23.com```

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

Setting nameserver pada client:
```nano /etc/resolv.conf```
```
nameserver 192.168.122.1
```

Di Sadewa Client :

Setting nameserver pada client:
```nano /etc/resolv.conf```
```
nameserver 10.75.3.2 # IP Yudhis
nameserver 10.75.2.2 # IP Werkudara
nameserver 192.168.122.1
```

ping arjuna.it23.com dan www.arjuna.it23.com

```ping arjuna.it23.com -c 5```
![ping arjuna it23 com](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/eb3d2857-6d10-4629-b1ab-ee66fc881704)

```ping www.arjuna.it23.com -c 5```
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
	file "/etc/bind/it23/arjuna.it23.com";
};

zone "abimanyu.it23.com" {
	type master;
	file "/etc/bind/jarkom/it23/abimanyu.it23.com";
};
```

Copy file db.local ke folder arjuna.it23.com :
```cp /etc/bind/db.local /etc/bind/it23/abimanyu.it23.com```

Buka file abimanyu.it23.com :
```nano /etc/bind/it23/abimanyu.it23.com```

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
@           IN      A       10.75.2.4 ; IP Abimanyu
www         IN      CNAME   abimanyu.it23.com.
@           IN      AAAA    ::1' > /etc/bind/it23/abimanyu.it23.com


```

Restart bind :
```service bind9 restart```

Di Sadewa Client :
ping arjuna.it23.com dan www.arjuna.it23.com

```ping abimanyu.it23.com -c 5```
![ping abimanyu it23 com](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/a9d25198-c6f3-4d21-b2ad-300f5aa405a9)

```ping www.abimanyu.it23.com -c 5```
![ping www abimanyu it23 com](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/1acb66db-81d1-4b2b-a998-6bd55ae71348)


### Soal 4
#### Description :
Buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu

#### Pengerjaan :
Buka file abimanyu.it23.com :
```nano /etc/bind/it23/abimanyu.it23.com```

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
@           IN      A       10.75.2.4 ; IP Abimanyu
www         IN      CNAME   abimanyu.it23.com.
parikesit   IN      A       10.75.2.4 ; IP Abimanyu
@           IN      AAAA    ::1
```


Restart bind :
```service bind9 restart```

Di Sadewa Client :

```ping parikesit.abimanyu.it23.com -c 5```
![ping parikesit abimanyu it23 com](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/1654b317-d2bf-448a-866d-91a2de4fb9be)


### Soal 5
#### Description :
Buatlah reverse domain untuk domain utama, yaitu Abimanyu

#### Pengerjaan :
Membuka file di named.conf.local :
```nano /etc/bind/named.conf.local```

Code :
```bash
zone "arjuna.it23.com" {
	type master;
	file "/etc/bind/it23/arjuna.it23.com";
};

zone "abimanyu.it23.com" {
	type master;
	file "/etc/bind/it23/abimanyu.it23.com";
};

zone "2.75.10.in-addr.arpa" {
    type master;
    file "/etc/bind/it23/4.3.75.10.in-addr.arpa";
};
```

Copy file db.local ke folder abimanyu.it23.com :
```cp /etc/bind/db.local /etc/bind/jarkom/2.75.10.in-addr.arpa```

Buka file 2.75.10.in-addr.arpa :
```nano /etc/bind/it23/2.75.10.in-addr.arpa```

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
; PTR Records
2.75.10.in-addr.arpa.		IN      NS      abimanyu.it23.com.
4                          	IN      PTR     abimanyu.it23.com.
```

Restart bind :
```service bind9 restart```

Kembalikan nameserver agar tersambung dengan Abimanyu
```host -t PTR 10.75.2.4```


### Soal 6
#### Description :
Membuat DNS Slave di Werkudara sebagai cadangan jika server DNS utama di Yudhistira mengalami kegagalan

#### Pengerjaan :
Membuka file di named.conf.local :
```nano /etc/bind/named.conf.local```

Code :
```bash
zone "arjuna.it23.com" {
	type master;
    	also-notify { 10.75.2.2; }; # IP Werkudara
    	allow-transfer { 10.75.2.2; }; # IP Werkudara
	file "/etc/bind/it23/arjuna.it23.com";
};

zone "abimanyu.it23.com" {
	type master;
    	also-notify { 10.75.2.2; }; # IP Werkudara
    	allow-transfer { 10.75.2.2; }; # IP Werkudara
	file "/etc/bind/it23/abimanyu.it23.com";
};

zone "2.75.10.in-addr.arpa" {
    type master;
    file "/etc/bind/it23/4.3.75.10.in-addr.arpa";
};
```

Di Werkudara

Membuka file di named.conf.local :
```nano /etc/bind/named.conf.local```

Code :
```bash
zone "arjuna.it23.com" {
	type slave;
	masters { 10.75.3.2; }; # IP Yudhis
	file "/etc/bind/it23/arjuna.it23.com";
};

zone "abimanyu.it23.com" {
	type slave;
	masters { 10.75.3.2; }; # IP Yudhis
	file "/etc/bind/it23/abimanyu.it23.com";
};

zone "2.75.10.in-addr.arpa" {
    type master;
    file "/etc/bind/it23/4.3.75.10.in-addr.arpa";
};
```

Restart bind :
```service bind9 restart```

Di Yudhistira
```service bind9 stop ```

Di Sadewa
ping arjuna.it23.com dan abimanyu.it23.com

```ping arjuna.it23.com -c 5```
![ping www arjuna it23 com saat slave](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/29b16e58-82ee-4d1e-82db-a5369e9c099d)

```ping abimanyu.it23.com -c 5```
![ping www abimanyu it23 com saat slave](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/c6785edc-269b-454e-89c6-54907a817099)


### Soal 7
#### Description :
Buatlah subdomain khusus untuk perang, yaitu baratayuda.abimanyu.it23.com dengan alias www.baratayuda.abimanyu.it23.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda

#### Pengerjaan :
Buka file abimanyu.it23.com
```nano /etc/bind/it23/abimanyu.it23.com```

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
@           	IN      NS      abimanyu.it23.com.
@           	IN      A       10.75.2.4 ; IP Abimanyu
www         	IN      CNAME   abimanyu.it23.com.
parikesit   	IN      A       10.75.2.4 ; IP Abimanyu
ns1		IN	A	10.75.2.4 ; IP Werkudara
baratayuda	IN 	NS	ns1
@           	IN      AAAA    ::1
```

Buka file named.conf.options
```nano /etc/bind/named.conf.options```

Code :
```bash
options {
directory \"var/cache/bind\";
allow-query{any;};

auth-nxdomain no;
listen-on-v6 { any; };
};
```

Buka file named.conf.local :
```nano /etc/bind/named.conf.local```

Code :
```bash
zone "arjuna.it23.com" {
	type master;
	notify yes;
    	also-notify { 10.75.2.2; }; # IP Werkudara
    	allow-transfer { 10.75.2.2; }; # IP Werkudara
	file "/etc/bind/it23/arjuna.it23.com";
};

zone "abimanyu.it23.com" {
	type master;
	notify yes;
    	also-notify { 10.75.2.2; }; # IP Werkudara
    	allow-transfer { 10.75.2.2; }; # IP Werkudara
	file "/etc/bind/jarkom/it23/abimanyu.it23.com";
};

zone "2.75.10.in-addr.arpa" {
    type master;
    file "/etc/bind/it23/4.3.75.10.in-addr.arpa";
};
```

Restart bind :
```service bind9 restart```

Di Sadewa Client :

```ping baratayuda.abimanyu.it23.com -c 5```
![ping baratayuda abimanyu it23 com](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/f0646b3e-6c5c-4845-9a06-0a5d20a938d0)

```ping www.baratayuda.abimanyu.it23.com -c 5```
![ping www baratayuda abimanyu it23 com](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/8c524eeb-0faf-416b-b335-d749be503b7d)


### Soal 8
#### Description :
Buatlah subdomain melalui Werkudara dengan akses rjp.baratayuda.abimanyu.yyy.com dengan alias www.rjp.baratayuda.abimanyu.yyy.com yang mengarah ke Abimanyu.

#### Pengerjaan :

Di Sadewa Client :

```ping rjp.baratayuda.abimanyu.it23.com -c 5```
![ping rjp baratayuda abimanyu it23 com](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/b5183c51-9c13-47c0-bd5a-062c58dc7ace)

```ping www.rjp.baratayuda.abimanyu.it23.com -c 5```
![ping www rjp baratayuda abimanyu it23 com](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/59fe1d23-cd65-4ade-a01c-995ddef6e107)


### Soal 9
#### Description :
Lakukan deployment pada masing-masing worker. Dengan Arjuna merupakan suatu Load Balancer Nginx dengan tiga worker yaitu Prabakusuma, Abimanyu, dan Wisanggeni.

#### Pengerjaan :
#### Prabukusuma
Buka file /var/www/jarkom_it23/index.php
```nano /etc/bind/named.conf.options``` 

Code :
```bash
<?php
echo "Ini Prabukusuma";
?>
```

Masukkan config ke /etc/nginx/sites-available/jarkom_it23 :
```bash
server {
    listen 8001;
    root /var/www/jarkom_it23;
    index index.php index.html index.htm;
    server_name _;
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
    }
    location ~ /\.ht {
        deny all;
    }
    error_log /var/log/nginx/jarkom_it23_error.log;
    access_log /var/log/nginx/jarkom_it23_access.log;
}
```

Run command :
```
ln -s /etc/nginx/sites-available/jarkom_it23 /etc/nginx/sites-enabled/jarkom_it23

rm /etc/nginx/sites-enabled/default

service nginx restart

service php7.2-fpm start

service php7.2-fpm status
```

Akses ke :
```lynx 10.75.2.5:8001```
![9Prabukusuma](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/f009e5c3-2410-457f-b2b2-cb0d76b8b41f)


#### Wisanggeni
Buka file /var/www/jarkom_it23/index.php
```nano /etc/bind/named.conf.options``` 

Code :
```bash
<?php
echo "Ini Wisanggeni";
?>
```

Masukkan config ke /etc/nginx/sites-available/jarkom_it23 :
```bash
server {
    listen 8002;
    root /var/www/jarkom_it23;
    index index.php index.html index.htm;
    server_name _;
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
    }
    location ~ /\.ht {
        deny all;
    }
    error_log /var/log/nginx/jarkom_it23_error.log;
    access_log /var/log/nginx/jarkom_it23_access.log;
}
```

Run command :
```
ln -s /etc/nginx/sites-available/jarkom_it23 /etc/nginx/sites-enabled/jarkom_it23

rm /etc/nginx/sites-enabled/default

service nginx restart

service php7.2-fpm start

service php7.2-fpm status
```

Akses ke :
```lynx 10.75.2.6:8002```
![9Wisanggeni](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/18fd7d66-b731-4588-89b1-f1597b582d1f)


#### Abimanyu
Buka file /var/www/jarkom_it23/index.php
```nano /etc/bind/named.conf.options``` 

Code :
```bash
<?php
echo "Ini Abimanyu";
?>
```

Masukkan config ke /etc/nginx/sites-available/jarkom_it23 :
```bash
server {
    listen 8003;
    root /var/www/jarkom_it23;
    index index.php index.html index.htm;
    server_name _;
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
    }
    location ~ /\.ht {
        deny all;
    }
    error_log /var/log/nginx/jarkom_it23_error.log;
    access_log /var/log/nginx/jarkom_it23_access.log;
}
```

Run command :
```
ln -s /etc/nginx/sites-available/jarkom_it23 /etc/nginx/sites-enabled/jarkom_it23

rm /etc/nginx/sites-enabled/default

service nginx restart

service php7.2-fpm start

service php7.2-fpm status
```

Akses ke :
```lynx 10.75.2.4:8003```
![9Abimanyu](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/33053b3d-e5c6-4679-ae5a-851167ea0f15)



### Soal 10
#### Description :
Gunakan algoritma Round Robin untuk Load Balancer pada Arjuna. Gunakan server_name pada soal nomor 1. Untuk melakukan pengecekan akses alamat web tersebut kemudian pastikan worker yang digunakan untuk menangani permintaan akan berganti ganti secara acak. Untuk webserver di masing-masing worker wajib berjalan di port 8001-8003. Contoh
    - Prabakusuma:8001
    - Abimanyu:8002
    - Wisanggeni:8003

#### Pengerjaan :
Masukkan config ke Arjuna Load Balancer di /etc/nginx/sites-available/load-balancer
```bash
# Mengonfigurasi Nginx dengan load balancing (Round Robin)
upstream webserver {
    server 10.75.2.5:8001; # IP Prabukusuma
    server 10.75.2.4:8002; # IP Abimanyu
    server 10.75.2.6:8003; # IP Wisanggeni
}
server {
    listen 80;
    server_name arjuna.it23.com www.arjuna.it23.com;
    location / {
        proxy_pass http://webserver;
    }
}
```

Run command :
```
ln -s /etc/nginx/sites-available/load-balancer /etc/nginx/sites-enabled/load-balancer

service nginx restart
```

Di Nakula Client
Akses ke :
``` lynx http://www.arjuna.it23.com ```
Run lynx yang sama 3 kali :
![hi prabukusuma](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/9d9909f4-cf96-4e68-960a-dbf5aea815d9)
![hi Abimanyu](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/9db80917-864b-4e31-a083-b24764afe54a)
![hi wisanggeni](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/d035dac7-9f6f-4ad2-8a28-881779bb9918)



### Soal 11
#### Description :
Lakukan konfigurasi Apache Web Server pada worker Abimanyu dengan web server www.abimanyu.yyy.com. Pertama dibutuhkan web server dengan DocumentRoot pada /var/www/abimanyu.yyy


### Pengerjaan :
![11Abimanyu](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/8fb2a4c6-73a1-4658-a600-1d617efaadf2)


### Soal 12
#### Description :


### Pengerjaan :
![12Abimanyu](https://github.com/dheaarfryza/Jarkom-Modul-2-IT23-2023/assets/89828723/20417717-2c10-4786-a07b-3d6b0189cd69)


### Soal 13
#### Description :


### Pengerjaan :
