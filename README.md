# Jarkom_Modul3_Lapres_T19
Penyelesaian Soal Shift 1 Komunikasi Data, dan Jaringan Data 2020\
Kelompok T19
  * Made Krisnanda Utama (05311840000033)
  * Muhammad Irsyad Ali (05311840000041)


---
## Table of Contents
* [Persiapan](#persiapan-1)
* [Soal 1](#soal-2)
* [Soal 2](#soal-3)
* [Soal 3](#soal-4)
* [Soal 4](#soal-5)
* [Soal 5](#soal-6)
* [Soal 6](#soal-7)
* [Soal 7](#soal-8)
* [Soal 8](#soal-9)
* [Soal 9](#soal-10)
* [Soal 10](#soal-11)
* [Soal 11](#soal-12)
* [Soal 12](#soal-13)
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
 **PERINTAH**
 Membuat topologi jaringan, Surabaya sebagai router, Malang sebagai DNS server, Tuban sebagai DHCP server, serta Mojokerto sebagai proxy server, dan UML lainnya sebagai client.
 
 **PENJELASAN**
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
-Kemudian lakukan konfigurasi interface pada tiap UML supaya bisa mendapatkan layanan dari DHCP. Setelah itu buka ```/etc/network/interfaces``` pada tiap client.
 
## Soal 2

## Soal 3

## Soal 4

## Soal 5

## Soal 6

## Soal 7

## Soal 8

## Soal 9

## Soal 10

## Soal 11

## Soal 12
