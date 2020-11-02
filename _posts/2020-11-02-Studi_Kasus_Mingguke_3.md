---
layout: post
title:  "Aplikasi Data Kontak - Menggunakan Java Netbeans & MYSQL || Studi Kasus Minggu Ketiga"
author: Mapriyatna
categories: [ Studi Kasus ]
image: assets/images/1.jpg
---

#### *Membuat Aplikasi Data Kontak dengan database MySQL || Studi Kasus pertemuan minggu ke 3*
##### *Muhamad Apriyatna 181011401125*

Pada pertemuan ini, saya akan membagikan sedikit tutorial bagaimana cara membuat aplikasi Database input data yang terdiri dari ID Kontak, Nama Kontak, No. Kontak, Alamat, Status dan Tabel Kontak.

Simak baik-baik pembahasan tutorial kali ini baik-baik ;)

Untuk membangun aplikasi sederhana ini, tentunya dibutuhkan aplikasi IDE Netbeans dan XAMPP.
Jika kalian belum mempunyai aplikasi XAMPP bisa mendownload terlebih dahulu [DI SINI](https://www.apachefriends.org/download.html).

Pertama jalankan XAMPP terlebih dahulu, lalu aktifkan Apache dan MySQL.
![](/assets/images/p3_d.png)

Buka Web browser, lalu ketik di kolom url "**localhost/phpmyadmin**".
Setelah itu create database dengan nama *database_kontak*, lalu buat database tabel dengan 5 kolom dengan index pada kolom pertama "**id_kontak sebagai primary key**". [](/assets/images/p3_3.png)

Kita beralih ke Netbeans IDE, buat project baru dengan cara File → New Project → Java Application → Next. lalu nama project "PertemuanMingguke3" dan "Finish".

Dalam Source Package kita buat baru *jFrame From...* dengan nama (disini saya isikan) **"MuhamadApriyatna_Mingguke3"**, lalu Finish.
![](/assets/images/p3_f.png)

Sebelum kita mengisi jFrame, jangan lupa untuk menambahkan **MySQL JDBC Driver** didalam Libraries untuk mengatur koneksi ke database MySQL.
![](/assets/images/p3_2.png)

Pada *jFrame* "input_data_kontak" kita buat desain seperti ini.

Dengan 6 Label, 4 TextField, 1 ComboBox, 1 Button, dan 1 Table yang ada pada Swing Controls, dan jangan lupa atur properties dan nama variable nya ;).
![](/assets/images/p3_g.png)

Pada ComboBox, kita atur seperti ini, dan jangan lupa pada *SelectedIndex "-1"* :
![](/assets/images/p3_9.png).

**Selanjutnya** ***Tahap selanjutnya, Kita akan memulai dengan mengetikkan coding.***

Untuk mempersingkat waktu, silahkan kalian download source code beserta format desainnya [DI SINI](https://app.box.com/s/1rphz9nji85k6jza2mr3yikhk029ya9i).

Dan paste di project Netbeans kalian.

---
***Saya harap kalian cukup paham dengan source code nya***
---

Setelah semuanya selesai,
Langkah terakhir yaitu kita coba jalankan aplikasinya dengan cara pilih atau klik tombol "Run" juga bisa dengan 'Shift + F6', tunggu beberapa detik dan muncul lah hasil program aplikasi yang kita buat.

Pada jFrame "input_data_kontak", kita bisa isikan nama dan pesan kita, dan klik "Submit". dan jFrame "Data_Kkontak" untuk melihat hasil datanya
![](/assets/images/p3_h.png).


Dan Kita lihat di localhost databasenya
![](/assets/images/p3_i.png).

Selamat kamu berhasil membuat program Aplikasi Database Data Kontak dengan Java Netbeans & MySQL.

Terimakasih,


Selamat Mencoba ;)