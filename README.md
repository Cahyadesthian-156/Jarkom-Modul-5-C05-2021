# Jarkom-Modul-5-C05-2021
Pengerjaan Soal Shift Modul 5 Jaringan Komputer 2021/2022     
.                                                           
Ghifari Astaudi U. (05111940000012)                             
Ricky Supriyanto (05111940000036)                                       
Cahyadesthian R. W. (05111940000156)                                   
.                                                               
# Praktikum Modul 5
### 📅 5 - 7 Desember 2021 

### Konfigurasi IP dengan VLSM (Variable Length Subnet Masking) :
<img width="793" alt="kofigurasi-IP-docx-ricky" src="https://user-images.githubusercontent.com/90148155/144958734-f69ac9e8-1ba3-458d-8570-32a69f6268c1.png">

### Tree :
![tree-docx-ricky](https://user-images.githubusercontent.com/90148155/144958765-ee5deacc-99c7-4d79-950f-77f1f6af520f.png)

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

### Routing
route add -net 192.186.1.0 netmask 255.255.255.0 gw 192.186.0.6                                     
route add -net 192.186.2.0 netmask 255.255.254.0 gw 192.186.0.6                                   
route add -net 192.186.0.24 netmask 255.255.255.248 gw 192.186.0.6                                    
route add -net 192.186.4.0 netmask 255.255.252.0 gw 192.186.0.2                                         
route add -net 192.186.0.128 netmask 255.255.255.128 gw 192.186.0.2                                 
route add -net 192.186.0.16 netmask 255.255.255.248 gw 192.186.0.2                                  

