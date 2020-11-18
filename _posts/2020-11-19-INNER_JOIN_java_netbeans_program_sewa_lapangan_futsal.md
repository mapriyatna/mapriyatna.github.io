---
layout: post
title:  "INNER JOIN - Java Netbeans & MYSQL || Lanjutan Program Penyewaan Lapangan Futsal"
author: Mapriyatna
categories: [ Tutorial ]
image: assets/images/nx.png
---

##### **Ini adalah lanjutan dari aplikasi penyewaan lapangan futsal dan dikembangkan dengan tambahan form session login menggunakan INNER JOIN**.

###### *Muhamad Apriyatna 181011401125*

INNER JOIN adalah Bentuk kondisi join dimana di antara 2 atau lebih tabel yang ingin di join memiliki hubungan sehingga semua isi tabel yang di pilih bisa di tampilkan.

Pada kesempatan kali ini saya akan menambahkan 2 tabel database dan form login ke dalam aplikasi sebelumnya, yaitu [Program Penyewaan Lapangan Futsal Menggunakan Java Netbeans & MYSQL](https://mapriyatna.github.io/Program_penyewaan_lapangan_Futsal/).

Simak baik-baik pembahasan tutorial kali ini ;)

Buka Web browser, lalu ketik di kolom url "**localhost/phpmyadmin**".
kemudian buka __"database_futsal"__, lalu buat tabel baru dengan nama **"data_user"**. Dengan "id_user sebagai primary key".
![](/assets/images/p5_1.png)

lalu buat tabel ke 2 dengan nama **"session"** dengan "**user_session sebagai primary key**". ![](/assets/images/p5_2.png)

Berikan Tambahan data pada tabel *"session"*
![](/assets/images/p5_3.png).

Selanjutnya, pada tabel **"data_user"**, buat **Foreign Key** kepada **"user_session"**
![](/assets/images/p5_4.png).

Lalu, isikan data seperti ini.
![](/assets/images/p5_5.png)

---
**Note** "Dari hasil pembuatan database tersebut saya membuat data_user ***"admin"*** sebagai pengguna yang full akses, dan ***"user"*** sebagai pengguna operator yang hanya bisa menyimpan data tetapi tidak bisa mengedit dan menghapus data".


---

**Kita beralih ke Netbeans IDE**, buat jFrame Form baru pada Source Package project sebelumnya. Dengan cara Klik Kanan → New → New jFrame Form → OK. lalu beri nama "HalamanLogin" dan "Finish".
![](/assets/images/p5_6.png)


Pada *jFrame* "HalamanLogin" kita buat desain seperti ini.
![](/assets/images/p5_7.png).

---

**Tahap Selanjutnya,** ***Kita akan memulai dengan memasukkan source code.***

*Perhatikan baik-baik*

Pada Package instansi masukkan code berikut :

```ruby
import java.sql.*;
import java.awt.*;
import javax.swing.JOptionPane;
```
---
Pada ***"public class HalamanLogin extends javax.swing.JFrame"*** masukkan coding dibawah ini.
```java
private Connection con;
private Statement stat;
private ResultSet res;
```
---
Pada methode constructor *public HalamanLogin()* terdapat satu code dengan *`initComponents();`*.
dibawahnya, masukkan coding berikut :
```ruby
koneksi();
kosongkan();
status();

    //rata kiri dan kanan
    Dimension screenSize = Toolkit.getDefaultToolkit().getScreenSize();
    Dimension frameSize = getSize();
    setLocation (
        (screenSize.width - frameSize.width) / 3,
        (screenSize.height - frameSize.height) / 4);
```
---
Lalu, buat ***"method konstuktor Koneksi"***, dengan cara masukkan kode dibawah ini.

```ruby
private void koneksi() {
	try {
		Class.forName ("com.mysql.jdbc.Driver");
		con=DriverManager.getConnection("jdbc:mysql://127.0.0.1/database_futsal", "root", "");
		stat=con.createStatement();
	} catch (Exception e) {
    	JOptionPane.showMessageDialog(null, e);
	}
}
```
---

***Sekarang kita setting bagian perintah button***

*Masukkan source code pada bagian button Masuk.*
```ruby
String access="";
try{
	res=stat.executeQuery("select dl.username, dl.password, dss.user_access "
    + "FROM data_user dl "
    + "INNER JOIN session dss "
    + "ON dl.user_session=dss.user_session "
    + "where "+ "dl.username='" +username_MuhamadApriyatna.getText()+"'"+ ""
    + "AND dl.password='"+password_MuhamadApriyatna.getText()+"'" );

    while(res.next()) {
    	access=res.getString(3);
    }
    if(access.equals("")) {
    	JOptionPane.showMessageDialog(null, "Username atau Password Salah !!!");
    } else {
    	if(access.equals("Admin")){
    		UTS_Mapriyatna_181011401125 mnu= new UTS_Mapriyatna_181011401125(); 
            mnu.HakaksesAdmin();
            mnu.setVisible(true);
            dispose();
        } else if(access.equals("Operator")) {
        	UTS_Mapriyatna_181011401125 mnu=new UTS_Mapriyatna_181011401125();
        	mnu.HakaksesOperator();
            mnu.setVisible(true);
            dispose();
        } else {
        	JOptionPane.showMessageDialog(null, "Login Gagal...!!!!");
        }
    }
```

---
*Masukkan source code pada bagian button Cancel.*
```ruby
System.exit(0);
```

---
**Note :** ***"Buka kembali project .java jFrame Form sebelumnya"***

**Pada .java jFrame Form ["UTS_Mapriyatna_181011401125"](https://mapriyatna.github.io/Program_penyewaan_lapangan_Futsal/), buat method contructor **HakaksesAdmin** dan **HakaksesOperator**.

*Masukan kode method di bawah ini*
```ruby
public void HakaksesAdmin(){

}

public void HakaksesOperator(){
	HapusData_MuhamadApriyatna.setEnabled(false);
    EditData_MuhamadApriyatna.setEnabled(false);
}
```

---
**Semua langkah hampir selesai,**.

Pada *"Source Package"*, Klik Kanan → Properties → pilih Run → "ubah main class dengan" *HalamanLogin* →. dan "Select Main Class", lalu "OK"
![](/assets/images/p5_8.png)

---
Setelah semuanya selesai.
Langkah terakhir yaitu kita coba jalankan aplikasinya dengan cara pilih atau klik tombol "Run" juga bisa dengan 'Shift + F6', tunggu beberapa detik dan muncul lah hasil program aplikasi yang kita buat.

Ujicoba  *"Sebagai Admin"*
![](/assets/images/p5_9.png).

Ujicoba *"Sebagai Operator"*
![](/assets/images/p5_10.png).

---
---

Untuk source code beserta database nya, kalian bisa [DOWNLOAD DI SINI](https://bit.ly/BookingFutsal-INNER_JOIN).


Dan untuk demo aplikasinya, silahkan lihat video dibawah ini :
[![Program Penyewaan Lapangan Futsal dengan Form Login - menggunakan INNER JOIN](https://res.cloudinary.com/marcomontalbano/image/upload/v1605702252/video_to_markdown/images/youtube--K31gYbVvqJ8-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/K31gYbVvqJ8 "INNER JOIN Java Netbeans & MySQL - Program Penyewaan Lapangan Futsal dengan Form Login")

**Selesai**.


Terimakasih,
Selamat Mencoba ;)