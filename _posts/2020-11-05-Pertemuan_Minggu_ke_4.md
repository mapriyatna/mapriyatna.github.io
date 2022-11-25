---
layout: post
title:  "Program Penyewaan Lapangan Futsal Menggunakan Java Netbeans & MYSQL || UTS Pemrograman 2"
author: Mapriyatna
categories: [ Tutorial ]
image: assets/images/nx.png
---

#### *Muhamad Apriyatna 181011401125*

Pada pertemuan ini, saya akan membagikan sedikit tutorial bagaimana cara membuat program penyewaan lapangan futsal yang terdiri dari : 
- Simpan hasil booking
- Edit hasil booking
- Hapus hasil booking
- Pencarian hasil booking

Simak baik-baik pembahasan tutorial kali ini baik-baik ;)

Untuk membangun aplikasi sederhana ini, tentunya dibutuhkan aplikasi IDE Netbeans dan XAMPP.
Jika kalian belum mempunyai aplikasi XAMPP bisa mendownload terlebih dahulu [DI SINI](https://www.apachefriends.org/download.html).

Pertama jalankan XAMPP terlebih dahulu, lalu aktifkan Apache dan MySQL.
![](/assets/images/p3_d.png)

Buka Web browser, lalu ketik di kolom url "**localhost/phpmyadmin**".
Setelah itu create database dengan nama *database_futsal*, lalu buat tabel dengan nama *"data_sewa"* ditambah dengan 9 kolom dengan index pada kolom pertama "**hsl_kode_booking sebagai primary key**". [](/assets/images/uts1.png).

**Kita beralih ke Netbeans IDE**, buat project baru dengan cara File → New Project → Java Application → Next. lalu nama project "UTS" dan "Finish".

Dalam Source Package kita buat baru *jFrame From...* dengan nama (disini saya isikan) **"UTS_Mapriyatna_181011401125"**, lalu Finish.

Sebelum kita mengisi jFrame, jangan lupa untuk menambahkan **MySQL JDBC Driver** didalam Libraries untuk mengatur koneksi ke database MySQL.
![](/assets/images/uts.png)

Pada *jFrame* "UTS_Mapriyatna_181011401125" kita buat desain seperti ini.
![](/assets/images/uts2.png).

**Note** *Perhatikan , dan jangan lupa atur properties dan nama variable nya ;)*.

Pada ComboBox, kita atur seperti ini, dan jangan lupa pada *SelectedIndex "-1"* :
![](/assets/images/p3_9.png).

---

**Tahap Selanjutnya,** ***Kita akan memulai dengan memasukkan source code.***

*Perhatikan baik-baik*

Pada Package instansi masukkan code berikut :

```ruby
import java.sql.*;
import java.awt.Dimension;
import java.awt.Toolkit;
import java.sql.DriverManager;
import java.sql.ResultSet;
import javax.swing.JOptionPane;
import javax.swing.table.DefaultTableModel;
```
---
Pada ***"public class MuhamadApriyatna_Mingguke4 extends javax.swing.JFrame"*** masukkan coding dibawah ini.
```java
private Connection con;
private Statement stat;
private ResultSet res;
```
---
Pada methode constructor *public MuhamadApriyatna_Mingguke4()* terdapat satu code dengan *`initComponents();`*.
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
Lalu, buat ***"konstuktor Koneksi, Status, Tabel, dan Lihat"***, dengan cara masukkan masing-masing konstuktor dibawah ini.

*Buat konstruktor koneksi* :
```ruby
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
---
*Buat konstruktor status* :
```ruby
private void status() { 
    statusComboBox.setSelectedIndex(-1); 
}
```
---
*Buat konstruktor tabel* :
```ruby
private void tabel() { 
    DefaultTableModel t= new DefaultTableModel();
    t.addColumn("ID"); 
    t.addColumn("Nama"); 
    t.addColumn("No Kontak");
    t.addColumn("Alamat"); 
    t.addColumn("Status"); 
    Table.setModel(t); 
    try { 
        koneksi();
        res=stat.executeQuery("select * from data_kontak"); 
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
---
*Buat konstruksi Lihat* :
```ruby
private DefaultTableModel dtm;
```

---
**Pertama, kita setting event action dari "id_kontak"**

**Pada bagian *"ID Kontak TextField"***, klik kanan, pilih Events, Action, lalu pilih ActionPerformed, lalu masukkan source code berikut.
```ruby
try { 
	res=stat.executeQuery("select * from data_Kontak where "+ "id_Kontak='" +id_KontakTextField.getText()
	+"'" ); while (res.next()) { 
	nama_KontakTextField.setText(res.getString("nama_kontak")); 
	no_KontakTextField.setText(res.getString("no_kontak")); 
	alamat_KontakTextField.setText(res.getString("alamat"));
	statusComboBox.setSelectedItem(res.getString("Status"));
	}
} catch (Exception e) {
	JOptionPane.showMessageDialog(rootPane, e); 
}
```

---
**Kedua, setting event mouse click pada tabel**

Klik kanan pada tabel, pilih Events, Mouse, lalu pilih mouseClicked. lalu masukkan source code berikut.
```ruby
int i = Table.getSelectedRow();
if(i==-1) {
	return;
}
String code = (String)Table.getValueAt(i,0);
String code1 = (String)Table.getValueAt(i,1);
String code2 = (String)Table.getValueAt(i,2);
String code3 = (String)Table.getValueAt(i,3);
String code4 = (String)Table.getValueAt(i,4);
id_KontakTextField.setText(code);
nama_KontakTextField.setText(code1);
no_KontakTextField.setText(code2);
alamat_KontakTextField.setText(code3);
statusComboBox.setSelectedItem(code4);
```

---
***Sekarang kita setting bagian perintah button***

*Masukkan source code pada bagian button Simpan.*
```ruby
try {
    stat.executeUpdate("insert into data_kontak values (" 
	+ "'" + id_KontakTextField.getText()+"'," 
	+ "'" + nama_KontakTextField.getText()+"'," 
	+ "'" + no_KontakTextField.getText()+"'," 
	+ "'" + alamat_KontakTextField.getText()+"',"
	+ "'" + statusComboBox.getSelectedItem()+ "')");
	con.close();
	tabel();

	JOptionPane.showMessageDialog(null, "Berhasil Menyimpan Data"); 
} catch (Exception e) {
    JOptionPane.showMessageDialog(null, "Perintah Salah : "+e);
}
```
---
*Masukkan source code pada bagian button Refresh.*
```ruby
id_KontakTextField.setText("");
nama_KontakTextField.setText("");
no_KontakTextField.setText("");
alamat_KontakTextField.setText("");
id_KontakTextField.requestFocus();
statusComboBox.setSelectedIndex(-1);
```
---
*Masukkan source code pada bagian button Hapus.*
```ruby
int ok=JOptionPane.showConfirmDialog(null,"Apakah Yakin Mendelete record ini???", "Confirmation",JOptionPane.YES_NO_CANCEL_OPTION);
if (ok==0) {
    try { 
		String sql="delete from data_kontak where id_kontak='"+id_KontakTextField.getText()+"'";
        PreparedStatement st=con.prepareStatement(sql);
        st.executeUpdate();
        JOptionPane.showMessageDialog(null, "Delete Data Sukses");
    } catch (Exception e){
        JOptionPane.showMessageDialog(null, "Delete Data Gagal");
    }
}
```
---
*Masukkan source code pada bagian button Lihat.*
```ruby
try {
    Object [] rows={"ID","Nama ","No Kontak","Alamat","Status"};
    dtm=new DefaultTableModel(null,rows);
    Table.setModel(dtm);
    Table.setBorder(null);
    jScrollPane1.setVisible(true);
    jScrollPane1.setViewportView(Table);
    int no = 1;
    String id_kontak="",nama_kontak="",no_kontak="",alamat="",status="";
    try {
        String sql="select * from data_kontak";
        Statement stat=con.createStatement();
        ResultSet res=stat.executeQuery(sql);
        while(res.next()) {
            id_kontak=res.getString("id_kontak");
            nama_kontak=res.getString("nama_kontak");
            no_kontak=res.getString("no_kontak");
            alamat=res.getString("Alamat");
            status=res.getString("status");
            String [] tampil={""+id_kontak,nama_kontak,no_kontak,alamat,status};dtm.addRow(tampil);
    	}
    } catch(SQLException e) {
        e.printStackTrace();
        JOptionPane.showMessageDialog(null,"Query Salah "+e);
    }
} catch(Exception e) {
    e.printStackTrace();
}
```
---
*Masukkan source code pada bagian button Search.*
```ruby
try {
    res=stat.executeQuery("select * from data_kontak where "+ "id_kontak='" +id_KontakTextField.getText()+"'" ); 
    while (res.next()) { 
    nama_KontakTextField.setText(res.getString("nama_kontak")); 
    no_KontakTextField.setText(res.getString("no_kontak")); 
    alamat_KontakTextField.setText(res.getString("alamat")); 
    statusComboBox.setSelectedItem(res.getString("status")); 
    } 
} catch (Exception e) { 
    JOptionPane.showMessageDialog(rootPane, e); 
}
```
---
*Masukkan source code ini pada bagian button Edit Data.*
```ruby
int ok=JOptionPane.showConfirmDialog(null,"Apakah Yakin Untuk Update Record ini???","Confirmation",JOptionPane.YES_NO_OPTION);
try {
    String sql="update data_kontak set id_kontak=?,nama_kontak=?,no_kontak=?,Alamat=?,status=? where id_kontak='"+id_KontakTextField.getText()+"'";
    PreparedStatement st=con.prepareStatement(sql);
    if(ok==0) {
        try {
            st.setString(1,id_KontakTextField.getText());
            st.setString(2,nama_KontakTextField.getText());
            st.setString(3,no_KontakTextField.getText());
            st.setString(4,alamat_KontakTextField.getText());
            st.setString(5, (String) statusComboBox.getSelectedItem());
            st.executeUpdate();
            JOptionPane.showMessageDialog(null,"Update Data Sukses");
        } catch (Exception e) {
            JOptionPane.showMessageDialog(null, "Update Data Gagal");
        }
    }
} catch (Exception e) {
}
```
---
*Masukkan source code pada bagian button Clear.*
```ruby
id_KontakTextField.setText("");
nama_KontakTextField.setText("");
no_KontakTextField.setText("");
alamat_KontakTextField.setText("");
id_KontakTextField.requestFocus();
statusComboBox.setSelectedIndex(-1);
```
---
*Masukkan source code pada bagian button Exit.*
```ruby
JOptionPane.showMessageDialog(null, "Anda telah keluar");
System.exit(0);
```

Setelah semuanya selesai.
Langkah terakhir yaitu kita coba jalankan aplikasinya dengan cara pilih atau klik tombol "Run" juga bisa dengan 'Shift + F6', tunggu beberapa detik dan muncul lah hasil program aplikasi yang kita buat.

Ujicoba Button *"Search"*
![](/assets/images/p4_8.png).

Ujicoba Button *"Submit"*
![](/assets/images/p4_3.png).

Ujicoba Button *"Edit Data"*
![](/assets/images/p4_4.png).

Ujicoba Button *"Lihat"*
![](/assets/images/p4_5.png).

Ujicoba Button *"Hapus"*
![](/assets/images/p4_6.png).

Ujicoba Button *"Clear dan Refresh"*
![](/assets/images/p4_7.png).

**Selesai**.

*Selamat kamu berhasil membuat Program Aplikasi Database dengan Java Netbeans & MySQL.*

Terimakasih,
Selamat Mencoba ;)