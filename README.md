# Jarkom_Modul3_Lapres_T19
Penyelesaian Soal Shift 1 Komunikasi Data, dan Jaringan Data 2020\
Kelompok T19
  * Made Krisnanda Utama (05311840000033)
  * Muhammad Irsyad Ali (05311840000041)


---
## Table of Contents
* [Soal 1](#soal-1)
* [Soal 2](#soal-2)
* [Soal 3](#soal-3)
* [Soal 4](#soal-4)
* [Soal 5](#soal-5)
* [Soal 6](#soal-6)
* [Soal 7](#soal-7)
* [Soal 8](#soal-8)
* [Soal 9](#soal-9)
* [Soal 10](#soal-10)
* [Soal 11](#soal-11)
* [Soal 12](#soal-12)
---

``` 
Teknis Pengerjaan
    1. Default memori UML adalah 64M, kecuali :
      a. SURABAYA : 256M
      b. MALANG : 160M
      c. MOJOKERTO : 128M
      d. TUBAN : 128M
    2. Menghitung dan menggunakan IP sesuai dengan NID Tuntap dan NID DMZ masing-masing kelompok
    3. IP Tuntap : NID_tuntap_tiap_kelompok + 1
    4. IP Interface Router SURABAYA :
      a. eth0 : NID_tuntap_tiap_kelompok + 2
      b. eth3 : NID_DMZ_tiap_kelompok + 1 
      c. eth1 : 192.168.0.1
      d. eth2 : 192.168.1.1
    5. IP Server (SUBNET 2) :
      MALANG    :  NID_DMZ_tiap_kelompok + 2
      MOJOKERTO : NID_DMZ_tiap_kelompok + 3
      TUBAN     : NID_DMZ_tiap_kelompok + 4
```

## Soal 1
 **PERINTAH**\
 Membuat topologi jaringan, *SURABAYA* sebagai router, *MALANG* sebagai DNS server, *TUBAN* sebagai DHCP server, serta *MOJOKERTO* sebagai proxy server, dan *UML* lainnya sebagai client.
 
 **PENJELASAN**\
 Pertama-tama setting awal pembuatan UML. Sintaks dari gambar topologi yang di soal sebegai berikut;
 ![1_1](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomer1_setting%20mojokerto.jpg)
 ```
 # Switch
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.76.89 eth1=daemon,,,switch2 eth2=daemon,,,switch3 eth3=daemon,,,switch2 mem256M &

# Server
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch2 mem=160M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch2 mem=128M &
xterm -T TUBAN -e linux ubd0=TUBAN,jarkom umid=TUBAN eth0=daemon,,,switch2 mem=128M &

# Klien
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch1 mem=64M &
xterm -T GRESIK -e linux ubd0=GRESIK,jarkom umid=GRESIK eth0=daemon,,,switch1 mem=64M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch3 mem=64M &
xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI umid-BANYUWANGI eth0=daemon,,,switch3 mem=64M &
```

* Kemudian lakukan konfigurasi interface pada tiap UML supaya bisa mendapatkan layanan dari DHCP. Setelah itu buka ```/etc/network/interfaces``` pada tiap client.

```
nano /etc/network/interfaces
```

* Lakukan pada *SURABAYA* tambahkan seperti pada gambar dibawah ini.
![1_2](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomer1_setting%20surabaya.jpg)

* Lakukan pada *MALANG* tambahkan seperti pada gambar dibawah ini.
![1_3](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor1_settingan%20malang.jpg)

* Lakukan pada *TUBAN* tambahkan seperti pada gambar dibawah ini.
![1_4](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomer1_setting%20tuban.jpg)

* Lakukan pada *MOJOKERTO* tambahkan seperti pada gambar dibawah ini.
![1_5](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomer1_setting%20mojokerto.jpg)

* Lakukan pada *BANYUWANGI* tambahkan seperti pada gambar dibawah ini.
![1_6](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20banyuwangi_step1.png)

* Lakukan pada *SIDOARJO* tambahkan seperti pada gambar dibawah ini.
![1_7](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20sidoarjo_step1.png)

* Lakukan pada *MADIUN* tambahkan seperti pada gambar dibawah ini.
![1_8](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20madiun_step1.png)

* Lakukan pada *GRESIK* tambahkan seperti pada gambar dibawah ini.
![1_9](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20gresik_step2.png)

* Dan gambar berikut merupakan hasil UML setelah kita lakukan konfigurasi.
![1_10](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor1_semua.jpg)

## Soal 2
 **PERINTAH**\
  SURABAYA ditunjuk sebagai perantara (DHCP Relay) antara DHCP Server dan client.

 **PENJELASAN**\
  Setelah itu lakukan instalasi ISC-DHCP pada TUBAN. Lakukan package list pada TUBAN dengan command.

```
apt-get update
```
* Install ISC-DHCP dengan command.
```
apt-get install isc-dhcp-server
```

![2_1](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/persiapan_install%20dhcpserver_tuban%20_eror.png)

* Setelah itu lakukan konfigurasi interface DHCP pada TUBAN. Setelah itu buka konfigurasi interface dengan perintah.

```
nano /etc/default/isc-dhcp-server
```

* Kemudian tentukan interfaces ``eth0`` untuk diberikan layanan DHCP.

```
INTERFACE=eth0
```

![2_2](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/persiapan_install%20dhcp%20server_tuban%20_step%201.png)

* Setelah itu lakukan konfigurasi DHCP pada TUBAN dengan command.

```
nano /etc/dhcp/dhcpd.conf
```

* Dan tambahkan script seperti pada gambar dibawah ini. Dan setelah itu lakukan restart servvice dengan perintah ``service isc-dhcp-server restart``

![2_3](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20di%20tuban_step1.png)

* Kemudian lakukan penginstallan relay pada SURABAYA dengan command berikut.

```
apt-get install isc-dhcp-relay
```

* Setelah melakukan perintah tersebut akan muncul windows seperti dibawah ini. Dan masukkan ip TUBAN yaitu ``10.151.77.180``.

* Setelah memasukkan ip TUBAN, akan diminta untuk memasukkan konfigurasi interface seperti gambar dibawah ini.

* Setelah itu proses instalasi isc-dhcp-relay pada surabaya telah berhasil seperti pada gambar dibawah ini.

![2_4](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%202_install%20relay%20selesai_surabaya.png)

## Soal 3
 **PERINTAH**\
  Client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan 192.168.0.110 sampai 192.168.0.200.
  
 **PENJELASAN**\
  Pertama-tama konfigurasi subnet TUBAN untuk client GRESIK dan SIDOARJO dengan cara melakukan perintah.

```
nano /etc/dhcp/dhcpd.conf
```

* Tambahkan script berikut dan sesuai dengan gambar dibawah.

```
subnet 192.168.0.0 netmask 255.255.255.0 {
    range 192.168.0.10 192.168.0.100;
    range 192.168.0.110 192.168.0.200;
    option routers 192.168.0.1;
    option broadcast-address 192.168.0.255;
    option domain-name-servers 10.151.77.176 202.46.129.2;
    default-lease-time 300;
}
```
![3_1](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20di%20tuban_step3_berhasil%20restart.png)

* Dan lakukan service restart dengan perintah.

```
service isc-dhcp-server restart
```

* Kemudian lakukan konfigurasi pada interface client GRESIK dan SIDOARJO dengan perintah.

```
nano /etc/network/interfaces
```

* Dan isi konfigurasi sesuai pada gambar dibawah ini.

![3_2](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20gresik_step2.png)
![3_3](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20sidoarjo_step1.png)

* Setelah itu lakukan testing dengan perintah. 
```
cat /etc/resolv.conf
```
* Dan Berikut merupakan hasil dari kedua client yang telah dikonfigurasikan.

![3_4](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20gresik_step4.png)
![3_5](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20sidoarjo_step3.png)

## Soal 4
 **PERINTAH**\
  Client pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70.
 
 **PENJELASAN**
  * Lakukan konfigurasi subnet TUBAN untuk client BANYUWANGI dan MADIUN dengan cara melakukan perintah.

```
nano /etc/dhcp/dhcpd.conf
```

* Tambahkan script berikut dan sesuai dengan gambar dibawah.

```
subnet 192.168.0.0 netmask 255.255.255.0 {
    range 192.168.1.50 192.168.1.70;
    option routers 192.168.1.1;
    option broadcast-address 192.168.1.255;
    option domain-name-servers 10.151.77.176 202.46.129.2;
    default-lease-time 600;
    max-lease-time 7200;
}
```

![4_1](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20di%20tuban_step1.png)

* Dan lakukan service restart dengan perintah.

```
service isc-dhcp-server restart
```

* Kemudian lakukan konfigurasi pada interface client BANYUWANGI dan MADIUN dengan perintah.

```
nano /etc/network/interfaces
```

* Dan isi konfigurasi sesuai pada gambar dibawah ini.

![4_2](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20banyuwangi_step1.png)
![4_3](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20madiun_step1.png)

* Setelah itu lakukan testing dengan perintah. 

```
cat /etc/resolv.conf
```

* Dan Berikut merupakan hasil dari kedua client yang telah dikonfigurasikan.

![4_4](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20banyuwangi_step3.png)
![4_5](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20madiun_step3.png)

## Soal 5
 **PERINTAH**\
  Client mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP
  
 **PENJELASAN**
 * Lakukan konfigurasi DHCP Server pada TUBAN dengan perintah

```
nano /etc/dhcp/dhcpd.conf
````

* Dan lakukan konfigurasi sperti dibawah ini.

![5_1](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20di%20tuban_step1.png)

* Dan berikut merupak hasil dns dari SIDOARJO, GRESIK, dan BANYUWANGI.

![5_2](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20sidoarjo_step3.png)
![5_3](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20gresik_step4.png)
![5_4](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20banyuwangi_step2.png)

## Soal 6
 **PERINTAH**\
  Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan client pada subnet 3 mendapatkan peminjaman IP selama 10 menit.
 
 **PENJELASAN**
 * Lakukan konfigurasi pada ``/etc/dhcp/dhcpd.conf`` dengan perintah.

```
nano /etc/dhcp.dhcpd.conf
```

* Dan lakukan konfigurasi seperti pada gambar dibawah ini.

![6_1](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20di%20tuban_step1.png)

## Soal 7
 **PERINTAH**\
  User autentikasi milik Anri memiliki format sebagai:
  * User     :userta_yyy
  * Password :inipassw0rdta_yyy
 
 **PENJELASAN**
 
## Soal 8

## Soal 9

## Soal 10

## Soal 11

## Soal 12
