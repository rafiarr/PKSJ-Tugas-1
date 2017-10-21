# Perancangan Keamanan Sistem Jaringan (PKSJ)- Tugas 1

> Tugas 1 pada Mata Kuliah PKSJ ini adalah melakukan pen test [Penetration Testing](https://en.wikipedia.org/wiki/Penetration_test) pada sebuah sistem.
>
> Sistem yang diserang adalah sebuah Ubuntu Server.
>
> Aplikasi yang terlibat: [Hydra](https://github.com/opennota/hydra), [Medusa](http://h.foofus.net/?cat=9), dan [NCrack](https://nmap.org/)
>
> *Semoga bermanfaat!*

##Daftar Isi

- [Dasar Teori](#dasar-teori)
- [Instalasi Aplikasi](#instalasi-aplikasi)
    -[Ubuntu Server](#ubuntu-server)
    -[]
- [Eksperimen]()


## TUGAS 1

### Pendahuluan


### Dasar Teori

1. 

###


## A. Instalasi Ubuntu Server
* Download [Ubuntu Server](https://"linkubuntuserver"). Pada percobaan kami, kami mengguanakan ubuntu server 16.04.
* Persiapkan Bootable USB untuk melakukan instalasi. Pada percobaan kami, kami menggunakan [Rufus](https://"linkrufus").
* Pada saat komputer melakukan booting pilih media USB dimana OS Ubuntu Server diletakkan. Pilih bahasa dan Enter.
* Selanjutnya pilih **Install Ubuntu Server**.
* Pilih bahasa yang hendak digunakan pada saat proses instalasi dan bahasa yang akan digunakan sebagai bahasa default OS.
* Pilih **Continent**, lalu **Country** yang sesuai dengan lokasi Anda saat ini.



## B. Instalasi OS Penetrator
* Download file instalasi [Kali Linux](https://"linkkali"). Pada percobaan kami, kami mengguanakan kali sebagai OS untuk penetrasi.
* Persiapkan bootable USB. Pada percobaan kami, kami menggunakan [Rufus](https://"linkrufus").
* Tahapan2 instalasi

## C. Instalasi SSH Server



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



## D. Uji Penetrasi


