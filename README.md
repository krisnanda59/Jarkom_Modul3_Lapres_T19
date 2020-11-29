# Jarkom_Modul3_Lapres_T19
Penyelesaian Soal Shift 3 Komunikasi Data, dan Jaringan Data 2020\
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
 Pertama-tama kami membuat topologi UML. sesuai yang ada di soal shift, sebagai berikut
 ![1_1](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor1_sintaks%20topologi.jpg)
 ```
 # Switch
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.70.65 eth1=daemon,,,switch2 eth2=daemon,,,switch3 eth3=daemon,,,switch2 mem256M &

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

* Kemudian kami melakukan konfigurasi interface pada setiap UML supaya bisa mendapatkan layanan dari DHCP. dengan menggunakan sintax ```/etc/network/interfaces``` pada setiap client.

```
nano /etc/network/interfaces
```

* Interface yang sudah di setting pada *SURABAYA*.
![1_2](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomer1_setting%20surabaya.jpg)

* Interface yang sudah di setting pada *MALANG*.
![1_3](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor1_settingan%20malang.jpg)

* Interface yang sudah di setting pada *TUBAN*.
![1_4](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomer1_setting%20tuban.jpg)

* Interface yang sudah di setting pada *MOJOKERTO* .
![1_5](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomer1_setting%20mojokerto.jpg)

* Interface yang sudah di setting pada *BANYUWANGI*.
![1_6](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20banyuwangi_step1.png)

* Interface yang sudah di setting pada *SIDOARJO*.
![1_7](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20sidoarjo_step1.png)

* Interface yang sudah di setting pada  *MADIUN* .
![1_8](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20madiun_step1.png)

* Interface yang sudah di setting pada  *GRESIK*.
![1_9](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20gresik_step2.png)

* Dan gambar berikut merupakan hasil UML setelah kita lakukan konfigurasi.
![1_10](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor1_semua.jpg)

## Soal 2
 **PERINTAH**\
  *SURABAYA* ditunjuk sebagai perantara (DHCP Relay) antara DHCP Server dan client.

 **PENJELASAN**\
  *  Karena surabaya ditunjuk sebagai relay, maka kami melakukan install relay di *SURABAYA* dengan menggunakan command dibawah, setelah melakukan ```apt-get update```  
  ``` 
  apt-get install isc-dhcp-relay
  ```
  *  disini terdapat 3 prompt yang dapat diisi, pada prompt pertama kami mengisikan IP Tuban yaitu ```10.151.71.132```, prompt kedua kami isi dengan ``` eth1 eth2 eth3 ```  
  
  *  Kemudian barulah kami menginstall DHCP server pada *TUBAN* menggunakan command dibawah, setelah melakukan ```apt-get update```
```
apt-get install isc-dhcp-server
```  
  *  Proses instalasi isc-dhcp-relay pada *SURABAYA* setelah berhasil.
![2_4](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%202_install%20relay%20selesai_surabaya.png)

  * Proses instalasi isc-dhcp-server pada *TUBAN* setelah berhasil.  
![2_1](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/persiapan_install%20dhcpserver_tuban%20_eror.png)

  * Setelah itu kami melakukan konfigurasi pada *TUBAN* dengan menggunakan command ``` nano /etc/default/isc-dhcp-server ```

  * Kami menambahkan ``eth0`` pada  interfaces agar dapat diberikan layanan DHCP.

```
INTERFACE=eth0
```

![2_2](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/persiapan_install%20dhcp%20server_tuban%20_step%201.png)

  * Setelah itu lakukan konfigurasi DHCP pada *TUBAN* dengan command.

```
nano /etc/dhcp/dhcpd.conf
```

  * Disini kami membuat satu subnet ``` subnet 10.151.71.128 netmask 255.255.255.248``` dimana subnet tersebut adalah dari DMZ kelompok kami. 
  * Dan setelah itu lakukan restart servvice dengan perintah ``service isc-dhcp-server restart``

![2_3](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20di%20tuban_step1.png)


## Soal 3
 **PERINTAH**\
  Client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan 192.168.0.110 sampai 192.168.0.200.
  
 **PENJELASAN**\
  * Pertama-tama konfigurasi subnet *TUBAN* untuk client *GRESIK* dan *SIDOARJO* dengan menggunakan ``` nano /etc/dhcp/dhcpd.conf ```
  * Disini kami membuat beberapa konfigurasi, yang pertama ada pada *subnet1* dengan command:   
  ```
   range 192.168.0.10 192.168.0.11
   range 192.168.0.110 192.168.0.100
  ```  
  * yang kedua berada di subnet 2 dengan command :
  ```
  range 192.168.1.50 192.168.1.7
  ```
![3_1](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20di%20tuban_step1.png)


  * Lalu lakukan service restart dengan perintah.

```
service isc-dhcp-server restart
```
![3_2](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20di%20tuban_step3_berhasil%20restart.png)

* Kemudian lakukan konfigurasi pada interface client *GRESIK* dan *SIDOARJO* dengan perintah:

```
nano /etc/network/interfaces
```

* Dan isi konfigurasi sesuai pada gambar dibawah ini.

![3_3](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20gresik_step2.png)
![3_4](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20sidoarjo_step1.png)

* Setelah itu lakukan testing dengan perintah. 
```
cat /etc/resolv.conf
```
* Dan Berikut merupakan hasil dari kedua client yang telah dikonfigurasikan.

![3_5](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20gresik_step4.png)
![3_6](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20sidoarjo_step3.png)

## Soal 4
 **PERINTAH**\
  Client pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70.
 
 **PENJELASAN**
  * Pertama konfigurasikan subnet TUBAN untuk client BANYUWANGI dan MADIUN dengan cara melakukan perintah:

```
nano /etc/dhcp/dhcpd.conf
```

* Tambahkan script berikut dan sesuai dengan gambar dibawah.

```
subnet 192.168.0.0 netmask 255.255.255.0 {
    range 192.168.1.50 192.168.1.70;
    option routers 192.168.0.1;
    option broadcast-address 192.168.0.255;
    option domain-name-servers 10.151.71.130 202.46.129.2;
    default-lease-time 300;
    max-lease-time 7200;
}
```

![4_1](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20di%20tuban_step1.png)

* Dan lakukan service restart dengan perintah:

```
service isc-dhcp-server restart
```

* Kemudian lakukan konfigurasi pada interface client *BANYUWANGI* dan *MADIUN* dengan perintah:

```
nano /etc/network/interfaces
```

* Dan isi konfigurasi sesuai pada gambar dibawah ini.

![4_2](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20banyuwangi_step1.png)
![4_3](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20madiun_step1.png)

* Setelah itu testing dengan perintah. 

```
cat /etc/resolv.conf
```

* Dan Berikut merupakan hasil dari kedua client yang telah dikonfigurasikan.

![4_4](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20banyuwangi_step3.png)
![4_5](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20madiun_step3.png)

## Soal 5
 **PERINTAH**\
  Client mendapatkan DNS *Malang* dan DNS 202.46.129.2 dari DHCP
  
 **PENJELASAN**
 * Pertama kami mengkonfigurasi DHCP Server pada *TUBAN* dengan perintah:

```
nano /etc/dhcp/dhcpd.conf
````

* Kemudian dikonfigurasikan sperti dibawah ini.

![5_1](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20di%20tuban_step1.png)

* Dan berikut merupak hasil dns dari *SIDOARJO*, *GRESIK*, dan *BANYUWANGI*.

![5_2](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20sidoarjo_step3.png)
![5_3](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20gresik_step4.png)
![5_4](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20client%20banyuwangi_step2.png)

## Soal 6
 **PERINTAH**\
  Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan client pada subnet 3 mendapatkan peminjaman IP selama 10 menit.
 
 **PENJELASAN**
 * Pertama kami mengkonfigurasi pada ``/etc/dhcp/dhcpd.conf`` dengan menginput:

```
nano /etc/dhcp.dhcpd.conf
```

* Kemudian kami mengkonfigurasi seperti dibawah ini.

![6_1](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%203%2C4%2C5%2C6_%20konfigurasi%20di%20tuban_step1.png)

## Soal 7
 **PERINTAH**\
  User autentikasi milik Anri memiliki format sebagai:
  * User     :userta_yyy
  * Password :inipassw0rdta_yyy
 
 **PENJELASAN**
 * Pertama install ``apache2-utils`` pada UML *MOJOKERTO*. Sebelumnya kami harus melakukan ``apt-get update``, input perintah:

```
apt-get install apache2-utils
```

* Setelah proses instalasi selesai, kami membuat user login dengan perintah:

```
htpasswd -c /etc/squid/passwd jarkom203
```

* Setelah itu edit konfigurasi squid menjadi.

```
http_port 8080
visible_hostname mojokerto

auth_param basic program /usr/lib/squid/basic_ncsa_auth /etc/squid/passwd
auth_param basic children 5
auth_param basic realm Proxy
auth_param basic credentialsttl 2 hours
auth_param basic casesensitive on
acl USERS proxy_auth REQUIRED
http_access allow USERS
```

![7_1](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%207_mojokerto%20step1.png)

* Terus restart squid menggunakan perintah:

```
service squid restart
```
![7_2](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%207_mojokerto%20step3.png)

* Kemudian akses web (usahakan menggunakan mode incognito/private), akan muncul pop-up untuk login menggunakan username dan password yang telah kita buat.

![7_3](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%207_mojokerto%20step%20login.png)

## Soal 8
 **PERINTAH**\
  setiap hari Selasa-Rabu pukul 13.00-18.00. Bu Meguri membatasi penggunaan internet Anri hanya pada jadwal yang telah ditentukan itu saja. Maka diluar jam tersebut, Anri tidak   dapat mengakses jaringan internet dengan proxy tersebut.
  
 **PENJELASAN**
 * Pertama kami membuat file baru pada UML *MOJOKERTO* bernama acl.conf dalam folder squid

```
nano /etc/squid/acl.conf
```

* Lalu isikan seperti gambar dibawah ini.

![8_1](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%207_mojokerto%20step2.png)

* Setelah itu kami simpan filenya, kemudian buka file squid.conf menggunakan perintah

```
nano /etc/squid/squid.conf
```

* Setelah itu kami mengkonfigurasi seperti pada gambar dibawah ini.

![](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%207_mojokerto%20step1.png)

* Kemudian restart squid menggunakan perintah.

```
service squid restart
```

## Soal 9
 **PERINTAH**\
  Setiap hari Selasa-Kamis pukul 21.00 - 09.00 keesokan harinya (sampai Jumat jam 09.00). Agar Anri bisa fokus mengerjakan TA.
 
 **PENJELASAN**
 * Pertama kami mengkonfigurasi acl pada *MOJOKERTO* dengan command. 

```
nano /etc/squid/acl.conf
```

* Lalu dikonfigurasi sesuai dengan gambar dibawah ini.

![9_1](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%207_mojokerto%20set%20waktu.png)

* Kemudian kami mengkonfigurasi squid.conf dengan command.

```
nano /etc/squid/squid.conf
```

* Selanjutnya restart squid dengan perintah:

```
service squid restart
```

* Terakhir tinggal dicoba akses web http://its.ac.id (usahakan menggunakan mode incognito/private). Pasti muncul halaman error semisal mengakses diluar waktu yang telah diset.

## Soal 10
 **PERINTAH**\
  Setiap dia mengakses google.com, maka akan di redirect menuju monta.if.its.ac.id agar Anri selalu ingat untuk mengerjakan TA.
  
 **PENJELASAN**
 * Pertama-tama kami mengkonfigurasi redirect pada squid.conf menggunakan command.

```
nano /etc/suqid/squid.conf
```

* Kemudian kami mengkonfigurasi seperti dibawah ini:

![10_1](https://github.com/krisnanda59/Jarkom_Modul3_Lapres_T19/blob/main/dokumentasi%20shift%203/nomor%207_mojokerto%20step1.png)

* Hasilnya nanti pasti setiap mengakses google.com pasti akan dilempar ke monta.if.its.ac.id.

## Soal 11

## Soal 12
