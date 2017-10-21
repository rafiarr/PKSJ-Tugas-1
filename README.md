# Perancangan Keamanan Sistem Jaringan (PKSJ)- Tugas 1

> Tugas 1 pada Mata Kuliah PKSJ ini adalah melakukan pen test [Penetration Testing](https://en.wikipedia.org/wiki/Penetration_test) pada sebuah sistem.
>
> Sistem yang diserang adalah sebuah Ubuntu Server.
>
> Aplikasi yang terlibat: [Hydra](https://github.com/opennota/hydra), [Medusa](http://h.foofus.net/?cat=9), dan [NCrack](https://nmap.org/)
>
> *Semoga bermanfaat!*

## Daftar Isi

- [Dasar Teori](#dasar-teori)
- [Instalasi Aplikasi](#instalasi-aplikasi)
    - [Server](#instalasi-server)
    - [Penetrator](#instalasi-penetrator)
    - [SSH Server](#instalasi-ssh-sever)
- [Eksperimen](#uji-penetrasi)


### Pendahuluan


### Dasar Teori


#### Computer Security

Computer Security, yang biasa dikenal juga sebagai Cyber Security dan/atau IT Security, adalah perlindungan pada sebuah sistem komputer dari pencurian atau kerusakan pada hardware, software, maupun informasi yang dimiliki, serta menghindari adanya gangguan ataupun alih-fungsi pada service yang tersedia.


#### Penetration Testing

Penetration Testing adalah metode untuk mengevaluasi keamanan sistem komputer atau jaringan dengan mensimulasikan serangan dari sumber yang berbahaya. Proses ini melibatkan analisis aktif terhadap sistem untuk setiap kerentanan potensial yang diakibatkan oleh sistem yang lemah atau konfigurasi sistem yang tidak benar atau kelemahan operasional dalam proses teknis. Masalah keamanan yang ditemukan akan disampaikan kepada pemilik sistem bersama dengan penilaian dampak dan mitigasi (solusi teknis) dari setiap kerentanan yang ditemukan.
Tujuan Penetration Testing diantaranya adalah untuk menentukan dan mengetahui serangan-serangan yang bisa terjadi terhadap kerentanan yang ada pada sistem, mengetahui dampak bisnis yang diakibatkan dari hasil ekpoitasi yang dilakukan oleh penyerang. Penetration Testing adalah salah satu komponen penting dari *Security Measures*.


### Vulnerabilities

Proses dari Penetration Testing dibagi menjadi 2:
1. Vulnerabilites Discovery - Operasi-operasi yang seharusnya berjalan normal, yang mana tester dapat melakukan uji coba melakukan kegiatan yang dianggap tidak sesuai.
2. Vulnerabilities Exploitation - Operasi-operasi ilegal yang dilakukan dan berjalan lancar akan dijadikan sasaran penyerangan


##Instalasi Aplikasi

Di bawah ini akan dijelaskan bagaimana melakukan eksperimen dengan pertama-tama melakukan instalasi aplikasi yang dibutuhkan.

### Instalasi Server
* Pada eksperimen kali ini kita menggunakan [Ubuntu Server](https://www.ubuntu.com/download/server?).
* Download Ubuntu Server. Pada percobaan kami, kami memilih Ubuntu Server 16.04.
* Persiapkan Bootable USB untuk melakukan instalasi. Pada percobaan kami, kami menggunakan [Rufus](https://"linkrufus").
* Pada saat komputer melakukan booting pilih media USB dimana OS Ubuntu Server diletakkan. Pilih bahasa dan Enter.
* Selanjutnya pilih **Install Ubuntu Server**.
* Pilih bahasa yang hendak digunakan pada saat proses instalasi dan bahasa yang akan digunakan sebagai bahasa default OS.
* Pilih **Continent**, lalu **Country** yang sesuai dengan lokasi Anda saat ini.




### Instalasi Penetrator
* Download file instalasi [Kali Linux](https://"linkkali"). Pada percobaan kami, kami mengguanakan kali sebagai OS untuk penetrasi.
* Persiapkan bootable USB. Pada percobaan kami, kami menggunakan [Rufus](https://"linkrufus").
* [Tahapan Instalasi OS Kali Linux]

Selanjutnya akan dijelaskan langkah-langkah menginstall aplikasi yang digunakan untuk Penetration Testing.

#### Instalasi Hydra

Untuk melakukan instalasi Hydra, cukup download file tar.gz yang dibutuhkan dan lakukan ekstraksi seperti biasa.

```bash
wget https://nmap.org/ncrack/dist/ncrack-0.5.tar.gz
./configure
make
make install
```

#### Instalasi NCrack

Untuk melakukan instalasi NCrack, cukup download file tar.gz yang dibutuhkan dan lakukan ekstraksi seperti biasa.

```bash
wget http://freeworld.thc.org/releases/hydra-6.3-src.tar.gz
./configure
make
make install
```

#### Instalasi Medusa

Untuk melakukan instalasi Medusa, cukup download file tar.gz yang dibutuhkan dan lakukan ekstraksi seperti biasa.

```bash
wget http://www.foofus.net/jmk/tools/medusa-2.0.tar.gz
./configure
make
make install
```

### Instalasi SSH Server

+ Untuk menginstall aplikasi OpenSSH server dan aplikasi yang terkait, jalankan kode:

```bash
sudo apt install openssh-server
```

+ Untuk mengonfigurasi OpenSSH, kita dapat melakukan modifikasi melalui file ` /etc/ssh/sshd_config`. Untuk informasi lebih detail mengenai apa saja yang bisa diedit dari file konfigurasi ini, bisa melihat petunjuk pada file tersebut, dengan menjalankan,


```bash
man sshd_config
```

Dibawah ini adalah contoh konfigurasi yang bisa dimodifikasi sesuai kebutuhan.

* Untuk mengatur supaya OpenSSH menggunakan Port 2222 sebagai ganti dari default TCP Port 22, cari baris konfigurasi berikut ini

```bash
Port 2222
```

dan ganti ke

```bash
Port 22
```



### Uji Penetrasi

Uji Penetrasi kali ini dibagi menjadi 3, yaitu menggunakan Hydra, NCrack, dan Medusa.

Untuk melakukan Penetration Test menggunakan *Automated Tools* dibawah ini, beberapa bisa melakukan attempt untuk 1 password, namun kali ini kami menggunakan password list yang tersimpan pada file `.txt`.

File yang kami gunakan ada 2:

* File yang berisi 10 baris ditambah dengan password asli. Bisa dilihat [disini](https://github.com/rafiarr/PKSJ-Tugas-1/blob/master/wordlist10.txt).
* File yang berisi 1000 baris ditambah dengan password asli. Bisa dilihat [disini](https://github.com/rafiarr/PKSJ-Tugas-1/blob/master/wordlist.txt).

#### Uji Penetrasi Menggunkan Hydra
#### Uji Penetrasi Menggunkan NCrack
#### Uji Penetrasi Menggunkan Medusa




