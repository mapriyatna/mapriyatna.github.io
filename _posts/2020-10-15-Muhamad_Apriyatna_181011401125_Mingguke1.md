---
layout: post
title:  "Tutorial - Cetak Kata dengan Java Netbeans || Minggu Pertama"
author: Mapriyatna
categories: [ Tutorial ]
image: assets/images/1.jpg
code-font-size: \small
---
Pada pertemuan ini, saya akan membagikan sedikit tutorial bagaimana cara membuat aplikasi GUI Cetak Kata dengan Java Netbeans

Simak baik-baik pembahasan tutorial kali ini baik-baik ;)

Sebelum kita membuat program java dengan netbeans, hal yang paling penting tentunya kalian sudah menginstall aplikasi netbeans.

Selanjutnya buat project dengan netbeans.
Pada tahap ini kalian pilih project java lalu Java Application dan pilih "Next"
![contoh gambar](assets/images/project.png)

Selanjutnya buat nama project sesuai dengan nama kalian masing-masing, disini saya isikan "MuhamadApriyatna_181011401125_Mingguke1" lalu pilih "Finish".
![contoh gambar](assets/images/np.png)

Dalam "Source Package", klik kanan pilih New lalu pilih "Java Package" dan isi dengan nama "PertemuanMinggu1".
![atau seperti gambar di bawah ini :](assets/images/jp.png)

Tahap selanjutnya, Kita akan mencoba buat desain aplikasi cetak kata seperti gambar di bawah ini.
![](assets/images/contoh.png)

Pertama kita susun buat dahulu desainnya seperti ini
![](assets/images/ini.png)

> Perlu diperhatikan, disini kita ganti nama variable dibawah ini dengan ketentuan :
   - jLabel1  ganti  menjadi Cetak Kata
   - jLabel2 ganti  variabel menjadi Nama
   - jLabel3 ganti  variabel menjadi Pesan
   - jLabel4 ganti menjadi Pesan
   - jTextField1 ganti variable menjadi nama
   - jTextArea1 ganti variable menjadi pesan
   - jTextArea2 ganti variable menjadi cetakpesan
   - jButton1 ganti variable menjadi button.

Langkah selanjutnya, pada tombol "Submit" klik kanan, pilih Events, Action, lalu pilih ActionPerformed.
![](/assets/images/button.png)

Isi source code ini ke dalamnya

{% highlight ruby linenos %}
int a = Integer.parseInt(Bayartxt.getText());
        int b = Integer.parseInt(Hargatxt.getText());
        int c = Integer.parseInt(Hari.getText());
        kembali = a - b * c;

        BuktiPembayarantxt.setText	("\n\t SELAMAT, \n PESANAN ANDA SUDAH TERVERIFIKASI"
                                        +"\n ------------------------------------------------------ "
                                        +"\n NIK / No. KTP \t: "+nim.getText()
                                        +"\n Nama \t\t: "+nama.getText()
                                        +"\n Jenis Kelamin \t: "+JKLabel.getText()
                                        +"\n Jadwal Datang \t: "+Tgl.getText()
                                        +"\n Lama Menginap \t: "+Hari.getText()+" Hari"
                                        +"\n Jenis Kamar \t: "+JPComboBox.getSelectedItem()
                                        +"\n Harga \t\t: "+Hargatxt.getText()
                                        +"\n Membayar \t\t: "+Bayartxt.getText()
                                        +"\n ||||||||||||||||||||||||||||||||||||||||||||||||||||||||"
                                        +"\n Saldo Pengembalian \t: "+kembali
                                        +"\n ------------------------------------------------------- "
                                        +"\n ---------------------TERIMAKASIH----------------- ");
{% endhighlight %}

Langkah terakhir, pilih atau klik tombol "Run" juga bisa dengan "Shift + F6", tunggu beberapa detik dan muncul lah hasil program aplikasi yang kita buat.

Di dalamnya, kita bisa isikan nama dan pesan kita, dan klik "Submit".
![](/assets/images/hasil.png)

Taraaa... selamat kamu berhasil membuat program cetak kata dengan Java Netbeans


Selamat Mencoba ;)