---
layout: post
title:  "Aplikasi Database dengan Java Netbeans & MYSQL || Minggu Ketiga"
author: Mapriyatna
categories: [ Tutorial ]
image: assets/images/1.jpg
---

#### *Tugas aplikasi database input data dengan java & Mysql || pertemuan minggu ke 3*
##### *Muhamad Apriyatna 181011401125*

Pada pertemuan ini, saya akan membagikan sedikit tutorial bagaimana cara membuat aplikasi Database input data yang terdiri dari ID Kontak, Nama Kontak, No. Kontak, Alamat, dan Status.

**Note:** *Dengan tampilan 2 class yang berbeda atau 2 jFrame*.
*Satu jFrame class untuk input data, dan jFrame class yang lain untuk melihat data*.

Simak baik-baik pembahasan tutorial kali ini baik-baik ;)

Untuk membangun aplikasi sederhana ini, tentunya dibutuhkan aplikasi IDE Netbeans dan XAMPP.
Jika kalian belum mempunyai aplikasi XAMPP bisa mendownload terlebih dahulu [DI SINI](https://www.apachefriends.org/download.html).

Pertama jalankan XAMPP terlebih dahulu, lalu aktifkan Apache dan MySQL.
![](/assets/images/p3_d.png)

Buka Web browser, lalu ketik di kolom url "**localhost/phpmyadmin**".
Setelah itu create database dengan nama *database_kontak*, lalu buat database tabel dengan 5 kolom dengan index pada kolom pertama "**id_kontak sebagai primary key**". [](/assets/images/p3_3.png)

Kita beralih ke Netbeans IDE, buat project baru dengan cara File → New Project → Java Application → Next. lalu nama project "PertemuanMingguke3" dan "Finish".

Dalam Source Package kita buat baru *jFrame From...* dengan nama **"input_data_kontak" dan "Data_Kontak"**, lalu Finish.
![](/assets/images/p3_5.png)

Sebelum kita mengisi jFrame, jangan lupa untuk menambahkan **MySQL JDBC Driver** didalam Libraries untuk mengatur koneksi ke database MySQL.
![](/assets/images/p3_2.png)

Pada *jFrame* "input_data_kontak" kita buat desain seperti ini.

Dengan 6 Label, 4 TextField, 1 ComboBox, dan 1 Button yang ada pada Swing Controls, dan jangan lupa atur properties dan nama variable nya ;).
![](/assets/images/p3_8.png)

Pada ComboBox, kita atur seperti ini, dan jangan lupa pada *SelectedIndex "-1"* :
![](/assets/images/p3_9.png)

Selanjutnya, pada *jFrame* "Data_Kontak" buat 1 jTable seperti ini :
![](/assets/images/p3_a.png)


Tahap selanjutnya, Kita akan memulai dengan mengetikkan coding pada masing-masing jFrame class.

**Pertama kita atur terlebih dahulu jFrame "input_data_kontak"**.

Pada Package instansi masukkan code berikut :

```java
import java.sql.*;
import java.awt.Dimension;
import java.awt.Toolkit;
import java.sql.DriverManager;
import java.sql.ResultSet;
import javax.swing.JOptionPane;
```

Pada *"public class input_data_kontak extends javax.swing.JFrame"* masukkan coding dibawah ini.
```java
private Connection con;
private Statement stat;
private ResultSet res;
```

Pada methode constructor public input_data_kontak() terdapat satu code dengan "initComponents();"
dibawahnya, masukkan coding berikut :
```java
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

Lalu, buat *"konstuktor koneksi, kosongkan, dan status"*, dengan cara masukkan masing-masing konstuktor dibawah ini.

*buat konstruktor koneksi* :
```java
private void koneksi() {
	try {
		Class.forName ("com.mysql.jdbc.Driver");
		con=DriverManager.getConnection("jdbc:mysql://127.0.0.1/database_kontak", "root", "");
		stat=con.createStatement();
	} catch (Exception e) {
    	JOptionPane.showMessageDialog(null, e);
	}
}
```

*buat konstruktor kosongkan* :
```java
private void kosongkan() {
	id_KontakTextField.setText("");
	nama_KontakTextField.setText("");
	no_KontakTextField.setText("");
	alamat_KontakTextField.setText("");
	id_KontakTextField.requestFocus();
	statusComboBox.setSelectedIndex(-1);
}
```

*buat konstruktor status* :
```java
private void status() { 
    statusComboBox.setSelectedIndex(-1); 
}
```

Pada tombol **"ID Kontak"** klik kanan, pilih Events, Action, lalu pilih ActionPerformed. Lalu masukkan script code dibawah ini
```ruby
try {
    res=stat.executeQuery("select * from data_Kontak where "+ "id_Kontak='" +id_KontakTextField.getText()+"'" );
    while (res.next()) {
    	nama_KontakTextField.setText(res.getString("nama_kontak")); 
    	no_KontakTextField.setText(res.getString("no_kontak")); 
    	alamat_KontakTextField.setText(res.getString("alamat"));
    	statusComboBox.setSelectedItem(res.getString("Status"));
	}
} catch (Exception e) {
	JOptionPane.showMessageDialog(rootPane, e);
}
```


Selanjutnya, Pada tombol "Simpan" klik kanan, pilih Events, Action, lalu pilih ActionPerformed. Lalu masukkan script code dibawah ini
```ruby
try {
    stat.executeUpdate("insert into data_kontak values (" 
    + "'" + id_KontakTextField.getText()+"'," 
    + "'" + nama_KontakTextField.getText()+"'," 
    + "'" + no_KontakTextField.getText()+"'," 
    + "'" + alamat_KontakTextField.getText()+"',"
    + "'" + statusComboBox.getSelectedItem()+ "')");
    con.close();
    JOptionPane.showMessageDialog(null, "Berhasil Menyimpan Data"); 
} catch (Exception e) {
	JOptionPane.showMessageDialog(null, "Perintah Salah : "+e);
}
```

**Kedua, kita atur jFrame "Data_Kontak"**.

Pada *"public class input_data_kontak extends javax.swing.JFrame"* masukkan coding dibawah ini.
```java
private Connection con;
private Statement stat;
private ResultSet res;
```

Pada methode constructor Data_Kontak() terdapat satu code dengan "initComponents();"
dibawahnya, masukkan coding berikut :
```java
koneksi();
kosongkan();
status();

    //rata kiri dan kanan
    Dimension screenSize = Toolkit.getDefaultToolkit().getScreenSize();
    Dimension frameSize = getSize();
    setLocation (
        (screenSize.width - frameSize.width) / 2,
        (screenSize.height - frameSize.height) / 3);
```

Lalu, buat *"konstuktor koneksi, dan tabel"*, dengan cara masukkan masing-masing coding dibawah ini.

*buat konstruktor koneksi* :
```java
private void koneksi() {
	try {
		Class.forName ("com.mysql.jdbc.Driver");
		con=DriverManager.getConnection("jdbc:mysql://127.0.0.1/database_kontak", "root", "");
		stat=con.createStatement();
	} catch (Exception e) {
    	JOptionPane.showMessageDialog(null, e);
	}
}
```

*buat konstruktor tabel* :
```java
private void tabel() { 
        DefaultTableModel t= new DefaultTableModel();
        t.addColumn("Id"); 
        t.addColumn("Nama"); 
        t.addColumn("No Kontak");
        t.addColumn("Alamat"); 
        t.addColumn("Status"); 
        Table.setModel(t); 
        try { res=stat.executeQuery("select * from data_kontak"); 
            while (res.next()) { 
                t.addRow(new Object[] { 
                res.getString("id_kontak"),
                res.getString("nama_kontak"), 
                res.getString("no_kontak"), 
                res.getString("alamat"), 
                res.getString("status") }); 
            }
        } catch (Exception e) { 
        JOptionPane.showMessageDialog(rootPane, e); 
        } 
    }
```

Setelah semuanya selesai,
Langkah terakhir yaitu kita coba jalankan aplikasinya dengan cara pilih atau klik tombol "Run" juga bisa dengan 'Shift + F6', tunggu beberapa detik dan muncul lah hasil program aplikasi yang kita buat.

Pada jFrame "input_data_kontak", kita bisa isikan nama dan pesan kita, dan klik "Submit". dan jFrame "Data_Kkontak" untuk melihat hasil datanya
![](/assets/images/p3_b.png).
![](/assets/images/p3_c.png).


Dan Kita lihat di localhost databasenya
![](/assets/images/p3_e.png).

Selamat kamu berhasil membuat program Aplikasi Database Input Data dengan Java Netbeans & MySQL.

Terimakasih,


Selamat Mencoba ;)