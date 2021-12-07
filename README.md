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

- SETTING INTERFACE PADA GNS3
**Foosha**
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
        address 192.186.0.1
        netmask 255.255.255.252

auto eth2
iface eth2 inet static
         address 192.186.0.5
         netmask 255.255.255.252
```
**Water7**
```
auto eth0
iface eth0 inet static
        address 192.186.0.2
        netmask 255.255.255.252
        gateway 192.186.0.1

auto eth1
iface eth1 inet static
        address 192.186.0.17
        netmask 255.255.255.248

auto eth2
iface eth2 inet static
         address 192.186.0.129
         netmask 255.255.255.128

auto eth3
iface eth3 inet static
         address 192.186.4.1
         netmask 255.255.252.0
```
**GUANHAO**
```
auto eth0
iface eth0 inet static
          address 192.186.0.6
          netmask 255.255.255.252
          gateway 192.186.0.5

auto eth1
iface eth1 inet static
          address 192.186.0.25
          netmask 255.255.255.248

auto eth2
iface eth2 inet static
          address 192.186.1.1
          netmask 255.255.255.0

auto eth3
iface eth3 inet static
           address 192.186.2.1
          netmask 255.255.254.0
```
**Blueno**
```
auto eth0
iface eth0 inet static
      address 192.186.0.130
      netmask 255.255.255.128
      gateway 192.186.0.129
```
**Chiper**
```
auto eth0
iface eth0 inet static
       address 192.186.4.2
      netmask 255.255.252.0
       gateway 192.186.4.1
```
**ELENA**
```
auto eth0
iface eth0 inet static
       address 192.186.2.2
       netmask 255.255.254.0
       gateway 192.186.2.1
```
**fukurou**
```
auto eth0
iface eth0 inet static
       address 192.186.1.2
       netmask 255.255.255.0
       gateway 192.186.1.1
```
**MainGate**
```
auto eth0
iface eth0 inet static
       address 192.186.0.27
       netmask 255.255.255.248
       gateway 192.186.0.25
```
**Jorge**
```
auto eth0
iface eth0 inet static
       address 192.186.0.26
       netmask 255.255.255.248
       gateway 192.186.0.25
```
**Doriki**
```
auto eth0
iface eth0 inet static
       address 192.186.0.18
       netmask 255.255.255.248
       gateway 192.186.0.17
```
**Jipangu**
```
auto eth0
iface eth0 inet static
       address 192.186.0.19
       netmask 255.255.255.248
       gateway 192.186.0.17
```
### (C) Routing
route add -net 192.186.1.0 netmask 255.255.255.0 gw 192.186.0.6                                     
route add -net 192.186.2.0 netmask 255.255.254.0 gw 192.186.0.6                                   
route add -net 192.186.0.24 netmask 255.255.255.248 gw 192.186.0.6                                    
route add -net 192.186.4.0 netmask 255.255.252.0 gw 192.186.0.2                                         
route add -net 192.186.0.128 netmask 255.255.255.128 gw 192.186.0.2                                 
route add -net 192.186.0.16 netmask 255.255.255.248 gw 192.186.0.2                                  

### (D) Tugas berikutnya adalah memberikan ip pada subnet Blueno, Cipher, Fukurou, dan Elena secara dinamis menggunakan bantuan DHCP server. Kemudian kalian ingat bahwa kalian harus setting DHCP Relay pada router yang menghubungkannya.

cara:
1. Install `apt-get instal isc-dhcp-relay -y` pada foosha, water7, dan guanhao, `apt-get install isc-dhcp-server` pada Jipangu

2. Pada Router (foosha, water7 dan guanhao) Edit file `/etc/sysctl.conf` deengan command
```
net.ipv4.ip_forward=1
net.ipv4.conf.all.accept_source_route = 1
```
3. Lakukan sysctl -p
4. Buka file `/etc/default/isc-dhcp-relay` dan edit server dengan mengarahkan dchp-relay menuju Jipangu `192.186.0.19` lalu `service isc-dhcp-relay restart` pada foosha, water7, dan guanhao
```
echo '# What servers should the DHCP relay forward requests to?
SERVERS="192.186.0.19"

# On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
INTERFACES=""

# Additional options that are passed to the DHCP relay daemon?
OPTIONS="" '> /etc/default/isc-dhcp-relay
```

5. Pada Jipangu edit file `/etc/default/isc-dhcp-server` dengan menambahkan:
```
INTERFACES="eth0
```

6. Pada dhcp-server isikan data pada `/etc/dhcp/dhcpd.conf` di Jipangu, lalu lakukan `service isc-dhcp-server restart`
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

7. Buka file '/etc/network/interfaces`. Command konfigurasi lama (static) dan ubah ip Blueno, Cipher, Fukurou, dan Elena dengan command
```
auto eth0
iface eth0 inet dhcp
```

8. Lakukan restart di node yang dijadikan ip dhcp

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

**Foosha**

Command yang digunakan `iptables -t nat -A POSTROUTING -s 192.186.0.0/16 -o eth0 -j SNAT --to-s (ip eth0)` yang menyesuaikan dari eth0 tersebut

Lalu, pada semua node yang terkait dilakukan `echo nameserver 192.168.122.1 > /etc/resolv.conf`

Keterangan:
- `-t nat`: Menggunakan tabel NAT karena akan mengubah alamat asal dari paket
- `-A POSTROUTING`: Menggunakan chain POSTROUTING karena mengubah asal paket setelah routing
- `-s 192.186.0.0/16`: Mendifinisikan alamat asal dari paket yaitu semua alamat IP dari subnet 192.186.0.0/16
- `-o eth0`: Paket keluar dari eth0 Foosha
- `-j SNAT`: Menggunakan target SNAT untuk mengubah source atau alamat asal dari paket
- `--to-s (ip eth0)`: Mendefinisikan IP source, di mana digunakan eth0 Foosha dengan rentang IP `192.168.122.0` sampai`192.168.122.255`

Catatan :

-> ip eth0 akan selalu berganti ketika restart node pada foosha atau restart GNS3 dengan rentang IP yang sudah dijelaskan

-> Cara mengetahui eth0, masukan command `ip a` pada foosha

### (2) Kalian diminta untuk mendrop semua akses HTTP dari luar Topologi kalian pada server yang memiliki ip DHCP dan DNS Server demi menjaga keamanan.

**Foosha**

Command yang digunakan yaitu `iptables -A FORWARD -p tcp --dport 80 -d 192.186.0.16/29 -i eth0 -j DROP`

Keterangan:

- `-A FORWARD`: Menggunakan chain FORWARD
- `-p tcp`: Mendefinisikan protokol yang digunakan, yaitu tcp
- `--dport 80`: Mendefinisikan port yang digunakan, yaitu 80 (HTTP)
- `-d 192.186.0.16/29`: Mendefinisikan alamat tujuan dari paket (DHCP dan DNS SERVER ) berada pada subnet 192.186.0.16/29
- `-i eth0`: Paket masuk dari eth0 Foosha
- `-j DROP`: Paket di-drop

**Testing**
- Install netcat di server Jipangu dan Doriki: `apt-get install netcat`
- Pada Jipangu dan Doriki ketikkan: `nc -l -p 80`
- Pada foosha ketikkan: `nmap -p 80 192.186.0.19` atau `nmap -p 80 192.186.0.18`

**Foosha**

<img width="427" alt="di" src="https://user-images.githubusercontent.com/81076281/145001108-d99a0e60-6268-40dc-bcba-915eb23de2cf.PNG">

**Doriki**

<img width="539" alt="da" src="https://user-images.githubusercontent.com/81076281/145001433-e7eb7900-09be-43dc-8241-2e5ee5c550f7.PNG">

### (3) Karena kelompok kalian maksimal terdiri dari 3 orang. Luffy meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.

**Jipangu dan Doriki**

Diberikan komen: 
```
iptables -D INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -D INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```

Keterangan:

- `-A INPUT`: Menggunakan chain INPUT
- `-p icmp`: Mendefinisikan protokol yang digunakan, yaitu ICMP (ping)
- `-m connlimit`: Menggunakan rule connection limit
- `--connlimit-above 3`: Limit yang ditangkap paket adalah di atas 3
- `--connlimit-mask 0` : Hanya memperbolehkan 3 koneksi setiap subnet dalam satu waktu
- `-j DROP`: Paket di-drop

Lalu untuk mengecek bisa dilakukan dengan masuk ke 4 node berbeda

Lalu, ping ke arah Jipangu secara bersamaan.

**MAINGATE**

<img width="530" alt="daa" src="https://user-images.githubusercontent.com/81076281/145035194-5108ff4d-cdb9-400f-8188-4698e109306e.PNG">

**GUANHAO**

<img width="475" alt="23" src="https://user-images.githubusercontent.com/81076281/145035760-cd0efe85-5b2f-4f6a-997b-ba9b77a0a3a7.PNG">

**JORGE**

<img width="479" alt="daa" src="https://user-images.githubusercontent.com/81076281/145036528-76ac9e88-6ab1-4ba9-805d-8ecbf9c1d71b.PNG">

**ELENA**

<img width="388" alt="311" src="https://user-images.githubusercontent.com/81076281/145035992-99a24d50-2544-4b1f-8b52-e2d9c9a6919a.PNG">

### (4) Kemudian kalian diminta untuk membatasi akses ke Doriki yang berasal dari subnet Blueno, Cipher, Elena dan Fukuro dengan beraturan sebagai berikut :Akses dari subnet Blueno dan Cipher hanya diperbolehkan pada pukul 07.00 - 15.00 pada hari Senin sampai Kamis.

**Doriki**

- Untuk paket yang berasal dari Blueno menggunakan perintah:
```
iptables -A INPUT -s 192.186.0.128/25 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -s 192.186.0.128/25 -j REJECT
```
- Sedangakan paket yang berasal dari Chiper menggunakan perintah:
```
iptables -A INPUT -s 192.186.4.0/22 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -s 192.186.4.0/22 -j REJECT
```
Keterangan:

- `A INPUT` : Menggunakan chain INPUT 
- `s 192.186.0.128/25` : Mendifinisikan alamat asal dari paket yaitu IP dari subnet Blueno
- `s 192.186.4.0/22` : Mendifinisikan alamat asal dari paket yaitu IP dari subnet Chiper
- `m time` : Menggunakan rule time
- `-timestart 07:00` : Mendefinisikan waktu mulai yaitu 07:00
- `-timestop 15:00: : Mendefinisikan waktu berhenti yaitu 15:00
- `--weekdays Mon,Tue,Wed,Thu` : Mendefinisikan hari yaitu Senin hingga Kamis
- `-j ACCEPT` : Paket di-accept
- `-j REJECT` : Paket ditolak


**Testing**

- Blueno

<img width="500" alt="si" src="https://user-images.githubusercontent.com/81076281/145043140-32820dd7-2992-4e63-9f2a-b6eca14ae156.jpg">

- Chiper

<img width="500" alt="si" src="ttps://user-images.githubusercontent.com/81076281/145043455-965bd3f1-b73d-4c9f-aae1-6a1c50a88956.jpg">

### (5) Akses dari subnet Elena dan Fukuro hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya.Selain itu di reject

**Doriki**

- Untuk paket yang berasal dari ELENA menggunakan perintah:
```
iptables -A INPUT -s 192.186.2.0/23 -m time --timestart 07:00 --timestop 15:00 -j REJECT
```
- Untuk paket yang berasal dari FUKUROU menggunakan perintah:
```
iptables -A INPUT -s 192.186.1.0/24 -m time --timestart 07:00 --timestop 15:00 -j REJECT
```
Keterangan:

- `A INPUT` : Menggunakan chain INPUT 
- `-s 192.186.2.0/23` : Mendifinisikan alamat asal dari paket yaitu IP dari subnet Elena
- `-s 192.186.1.0/24` : Mendifinisikan alamat asal dari paket yaitu IP dari subnet Fukurou
- `m time` : Menggunakan rule time
- `-timestart 07:00` : Mendefinisikan waktu mulai yaitu 07:00
- `-timestop 15:00: : Mendefinisikan waktu berhenti yaitu 15:00
- `-j REJECT` : Paket ditolak

**Testing**

- Elena

<img width="500" alt="si" src="https://user-images.githubusercontent.com/81076281/145042747-9e99754a-3f36-40a6-a62a-a35fc872e105.jpg">

- Fukurou

<img width="500" alt="si" src="https://user-images.githubusercontent.com/81076281/145042547-884ed295-391d-494b-80d5-0753f23218f3.jpg">

### (6) Karena kita memiliki 2 Web Server, Luffy ingin Guanhao disetting sehingga setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada Jorge dan Maingate

**Doriki**
- membuat domain (DNS) yang mengarah ke IP random (dalam hal ini 192.186.8.1) pada file `/etc/bind/named.conf`
```
zone "jarkomC05.com" {
        type master;
        file "/etc/bind/jarkom/jarkomC05.com";
};
```
- Buat folder jarkom dengan command:
```
mkdir /etc/bind/jarkom
```
- Lalu copy `db.local` ke file ` /etc/bind/jarkom/jarkomC05.com`
```
cp /etc/bind/db.local /etc/bind/jarkom/jarkomC05.com
```
- Lalu edit file `/etc/bind/jarkom/jarkomC05.com`
```
$TTL    604800
@       IN      SOA     jarkomC05.com. root.jarkomC05.com. (
                        2021120705      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      jarkomC05.com.
@       IN      A       192.186.8.1
```
**Guanhao**
- Masukkan perintah:
```
iptables -A PREROUTING -t nat -p tcp -d 192.186.8.1 --dport 80 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.186.0.26:80
iptables -A PREROUTING -t nat -p tcp -d 192.186.8.1 --dport 80 -j DNAT --to-destination 192.186.0.27:80
iptables -t nat -A POSTROUTING -p tcp -d 192.186.0.26 --dport 80 -j SNAT --to-source 192.186.8.1:80
iptables -t nat -A POSTROUTING -p tcp -d 192.186.0.27 --dport 80 -j SNAT --to-source 192.186.8.1:80
```

**Testing**
- Pada Guanhao, Jorge, Maingate dan Elena install `apt-get install netcat`
- Pada Jorge ketikkan perintah: `nc -l -p 80`
- Pada Maingate ketikkan perintah: `nc -l -p 80`
- Pada client Elena ketikkan perintah: `nc 192.186.8.1 80`
- Ketikkan sembarang pada client Elena, nanti akan muncul bergantian

**Elena**

<img width="301" alt="si" src="https://user-images.githubusercontent.com/81076281/145011348-7ccc71a6-107b-4c5d-a7ef-46c48d5e8c83.PNG">

**MainGate**

<img width="221" alt="sa" src="https://user-images.githubusercontent.com/81076281/145011215-ae6fbfab-da84-432b-a2bf-dd69aca518cd.PNG">

**Jorge**

<img width="224" alt="su" src="https://user-images.githubusercontent.com/81076281/145011500-df815306-12e9-485f-bbdd-8f5b60da4bb4.PNG">

