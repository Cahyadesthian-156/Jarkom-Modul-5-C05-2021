# Jarkom-Modul-5-C05-2021
Pengerjaan Soal Shift Modul 5 Jaringan Komputer 2021/2022     
.                                                           
Ghifari Astaudi U. (05111940000012)                             
Ricky Supriyanto (05111940000036)                                       
Cahyadesthian R. W. (05111940000156)                                   
.                                                               
# Praktikum Modul 5
### 📅 5 - 7 Desember 2021 

### (A) Tugas pertama kalian yaitu membuat topologi jaringan sesuai dengan rancangan yang diberikan Luffy dibawah ini:
<img src="https://github.com/Cahyadesthian-156/Jarkom-Modul-5-C05-2021/blob/main/img/awal.png" width="800">

### (B) Konfigurasi IP dengan VLSM (Variable Length Subnet Masking) :
<img src="https://github.com/Cahyadesthian-156/Jarkom-Modul-5-C05-2021/blob/main/img/topologi.png" width="800">

### Tree :
<img src="https://github.com/Cahyadesthian-156/Jarkom-Modul-5-C05-2021/blob/main/img/tree.png" width="800">

### Pembagian IP :
| Subnet  | Jumlah IP | Netmask | subnetmask | nid |
| :---         |     :---:      |          ---: | :---:      | :---:      |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| A1 | 2 | /30 | 255.255.255.252 | 192.186.0.0 |
| A2 | 2 | /30 | 255.255.255.252 | 192.186.0.4 |
| A3 | 201 | /24 | 255.255.255.0 | 192.186.1.0 |
| A4 | 301 | /23 | 255.255.254.0 | 192.186.2.0 |
| A5 | 101 | /25 | 255.255.255.128 | 192.186.0.128 |
| A6 | 701 | /22 | 255.255.252.0 | 192.186.4.0 |
| A7 | 4 | /29 | 255.255.255.248 | 192.186.0.16 |
| A8 | 4 | /29 | 255.255.255.248 | 192.186.0.24 |
| Jumlah | 1316 | /21 | 255.255.248.0 | - |

### (C) Routing
route add -net 192.186.1.0 netmask 255.255.255.0 gw 192.186.0.6                                     
route add -net 192.186.2.0 netmask 255.255.254.0 gw 192.186.0.6                                   
route add -net 192.186.0.24 netmask 255.255.255.248 gw 192.186.0.6                                    
route add -net 192.186.4.0 netmask 255.255.252.0 gw 192.186.0.2                                         
route add -net 192.186.0.128 netmask 255.255.255.128 gw 192.186.0.2                                 
route add -net 192.186.0.16 netmask 255.255.255.248 gw 192.186.0.2                                  

### (D) Tugas berikutnya adalah memberikan ip pada subnet Blueno, Cipher, Fukurou, dan Elena secara dinamis menggunakan bantuan DHCP server. Kemudian kalian ingat bahwa kalian harus setting DHCP Relay pada router yang menghubungkannya.
cara:
1. ubah ip Blueno, Cipher, Fukurou, dan Elena dengan command
```
auto eth0
iface eth0 inet dhcp
```

2. Lalu install `bind9 -y` pada Doriki, `apt-get instal isc-dhcp-relay -y` pada foosha, water7, dan guanhao, `apt-get install isc-dhcp-server` pada Jipangu

3. Arahkan dchp-relay menuju Jipangu `192.186.0.19` lalu `service isc-dhcp-relay restart` pada foosha, water7, dan guanhao

4. Pada dhcp-server isikan data pada `/etc/dhcp/dhcpd.conf` di Jipangu, lalu lakukan `service isc-dhcp-server restart`
```
subnet 192.186.1.0 netmask 255.255.255.0 {
    range 192.186.1.2 192.186.1.254;
    option routers 192.186.1.1;
    option broadcast-address 192.186.1.255;
    option domain-name-servers 192.186.0.18;
    default-lease-time 600;
    max-lease-time 7200;
}
subnet 192.186.0.128 netmask 255.255.255.128 {
    range 192.186.0.130 192.186.0.254;
    option routers 192.186.0.129;
    option broadcast-address 192.186.0.255;
    option domain-name-servers 192.186.0.18;
    default-lease-time 600;
    max-lease-time 7200;
}
subnet 192.186.4.0 netmask 255.255.252.0 {
    range 192.186.4.2 192.186.4.254;
    option routers 192.186.4.1;
    option broadcast-address 192.186.4.255;
    option domain-name-servers 192.186.0.18;
    default-lease-time 600;
    max-lease-time 7200;
}
subnet 192.186.2.0 netmask 255.255.254.0 {
    range 192.186.2.2 192.186.2.254;
    option routers 192.186.2.1;
    option broadcast-address 192.186.2.255;
    option domain-name-servers 192.186.0.18;
    default-lease-time 600;
    max-lease-time 7200;
}
subnet 192.186.0.16 netmask 255.255.255.248{
}

```

5. Lakukan restart di node yang dijadikan ip dhcp

Berikut adalah hasilnya :

#### Blueno
<img src="https://github.com/Cahyadesthian-156/Jarkom-Modul-5-C05-2021/blob/main/img/blueno.png" width="800">

#### chiper
<img src="https://github.com/Cahyadesthian-156/Jarkom-Modul-5-C05-2021/blob/main/img/chiper.png" width="800">

#### elena
<img src="https://github.com/Cahyadesthian-156/Jarkom-Modul-5-C05-2021/blob/main/img/elena.png" width="800">

#### fukurou
<img src="https://github.com/Cahyadesthian-156/Jarkom-Modul-5-C05-2021/blob/main/img/fukurou.png" width="800">

### (1) Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Foosha menggunakan iptables, tetapi Luffy tidak ingin menggunakan MASQUERADE.

Command yang digunakan `iptables -t nat -A POSTROUTING -s 192.186.0.0/16 -o eth0 -j SNAT --to-s (ip eth0)` yang menyesuaikan dari eth0 tersebut

Pada semua router Tambahkan di `/etc/sysctl.conf`:
```
net.ipv4.ip_forward=1
net.ipv4.conf.all.accept_source_route = 1
```

Lalu, pada semua node yang terkait dilakukan `echo nameserver 192.168.122.1 > /etc/resolv.conf`

### (2) Kalian diminta untuk mendrop semua akses HTTP dari luar Topologi kalian pada server yang memiliki ip DHCP dan DNS Server demi menjaga keamanan.

### (3) Karena kelompok kalian maksimal terdiri dari 3 orang. Luffy meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.


### (4) Kemudian kalian diminta untuk membatasi akses ke Doriki yang berasal dari subnet Blueno, Cipher, Elena dan Fukuro dengan beraturan sebagai berikut :Akses dari subnet Blueno dan Cipher hanya diperbolehkan pada pukul 07.00 - 15.00 pada hari Senin sampai Kamis.


### (5) Akses dari subnet Elena dan Fukuro hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya.Selain itu di reject


### (6) Karena kita memiliki 2 Web Server, Luffy ingin Guanhao disetting sehingga setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada Jorge dan Maingate
