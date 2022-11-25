---
layout: post
title:  "Tutorial - Booking Hotel sederhana dengan Java Netbeans || Minggu Kedua"
author: Mapriyatna
categories: [ Tutorial ]
image: assets/images/1.jpg
---

#### *Menggabungkan Studi kasus dari pertemuan minggu ke 2*

Pada pertemuan ini, saya akan membagikan sedikit tutorial bagaimana cara membuat aplikasi GUI Booking Hotel (gabungan dari pembahasan materi studi kasus pertemuan minggu ke 2) dengan Java Netbeans.

Simak baik-baik pembahasan tutorial kali ini baik-baik ;)

Sebelum kita membuat program java dengan netbeans, hal yang paling penting tentunya kalian sudah menginstall aplikasi netbeans.

Selanjutnya buat project dengan netbeans.
Pada tahap ini kalian pilih project java lalu Java Application dan pilih "Next".
![Contoh gambar](/assets/images/project.png)

Selanjutnya buat nama project sesuai dengan nama kalian masing-masing, disini saya isikan "PertemuanMinggu2" lalu pilih "Finish".
Lalu, dalam "Source Package", klik kanan pilih "New" lalu pilih "Java Package" dan isi dengan nama "LatihanMinggu2".
Klik kanan lagi pada "Source Package", pilih "New" lalu pilih "jFrame From...".
![atau seperti gambar di bawah ini :](/assets/images/m1.png)

Tahap selanjutnya, Kita akan mencoba buat desain aplikasi cetak kata seperti gambar di bawah ini.
![](/assets/images/m22.png)

Pertama kita susun terlebih dahulu desainnya seperti ini :
![](/assets/images/m2.png)

**Note:** Untuk "jLabel", ubah sesuai dengan keperluan kalian masing-masing.

> Perlu diperhatikan, disini kita ganti nama variable dibawah ini dengan ketentuan :
   - jTextField1 ganti variable menjadi nik
   - jTextField2 ganti variable menjadi nama
   - jTextField3 ganti variable menjadi JKLabel
   - jTextField4 ganti variable menjadi Tgl
   - jTextField5 ganti variable menjadi Hari
   - jTextField6 ganti variable menjadi Hargatxt
   - jTextField7 ganti variable menjadi Bayartxt
   - jCheckBox1 ganti variable menjadi Laki
   - jCheckBox2 ganti variable menjadi Cewe
   - jComboBox1 ganti variable menjadi JPComboBox
   - jButton1 ganti variable menjadi Button
   - jTextPane1 ganti variable menjadi BuktiPembayarantxt.


Sebelum melanjutkan ke step berikutnya, masukkan script atau kode dibawah ini.
```ruby
    public String JenisKamar;
    public String HargaBayar;
    public String JK ="";
    public int kembali;
```

**Note:**
*String JenisKamar dan String HargaBayar untuk menghitung dan menampilkan harga jenis kamar yang akan dipilih,*
*String JK untuk menampilkan hasil jenis kelamin yang dipilih,*
*dan int kembali untuk menghitung hasil kembalian ketika melakukan pembayaran atau pemesanan*.


Selanjutnya, kita atur terlebih dahulu variable checkbox "Laki-laki dan Perempuan" dengan mengklik kanan, pilih Events, Action, lalu pilih ActionPerformed.
Lalu masukkan script atau kode dibawah ini.

variable CheckBox Laki-laki :
```ruby
        JK="Laki-laki";
        Cewe.setSelected(false);

        JKLabel.setText(JK);
```
variable CheckBox Perempuan :
```ruby
        JK = "Perempuan";
        Laki.setSelected(false);

        JKLabel.setText(JK);
```

Berikutnya kita setting variable jComboBox yang sudah di ganti sebelumnya menjadi "JPComboBox".
Pertama, Klik kanan pilih "Properties" pilih tanda "..." (titik), lalu edit seperti yang ini.
![](/assets/images/m4.png)

**catatan:** *pada SelectedIndex ubah dengan -1, karena list item dimulai dari index 0 atau urutan item yang kita edit seperti gambar di atas*

Lalu, tambahkan script code untuk menjalankan list item yang dimulai dari -1.

Masukkan script code `JPComboBox.setSelectedIndex(-1);` tepat pada ***method constructor***.
![atau seperti gambar dibawah ini.](/assets/images/m5.png)

Sekarang kita setting action klik-nya.
Langkah selanjutnya, pada JPComboBox klik kanan, pilih Events, Action, lalu pilih ActionPerformed. Lalu masukkan script code dibawah ini
```ruby
JenisKamar = (String) JPComboBox.getSelectedItem();
	if (JenisKamar == "Standard Room") {
		HargaBayar = "350000";
		} else if (JenisKamar == "Suite Room") {
			HargaBayar = "500000";
		} else if (JenisKamar == "Deluxe Room") {
			HargaBayar = "1500000";
		} else if (JenisKamar == "Superior Room") {
			HargaBayar = "2300000";
	}
Hargatxt.setText(String.valueOf(HargaBayar));
```
Berikutnya, kita setting tombol "Button", dalam langkah ini klik kanan paca variable Button, pilih event, Action, lalu pilih ActionPerformed.
lalu, isi source code ini ke dalamnya.
```ruby
        int a = Integer.parseInt(Bayartxt.getText());
        int b = Integer.parseInt(Hargatxt.getText());
        int c = Integer.parseInt(Hari.getText());
        kembali = a - b * c;

        BuktiPembayarantxt.setText	("\n\t SELAMAT, \n PESANAN ANDA SUDAH TERVERIFIKASI"
                                        +"\n ------------------------------------------------------ "
                                        +"\n NIK / No. KTP \t: "+nik.getText()
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
```


Langkah terakhir yaitu kita coba jalankan aplikasinya dengan cara pilih atau klik tombol "Run" juga bisa dengan 'Shift + F6', tunggu beberapa detik dan muncul lah hasil program aplikasi yang kita buat.

Di dalamnya, kita bisa isikan nama dan pesan kita, dan klik "Submit".
![](/assets/images/m3.png)

Taraaa... selamat kamu berhasil membuat program Booking Hotel dengan Java Netbeans.

Terimakasih,


Selamat Mencoba ;)