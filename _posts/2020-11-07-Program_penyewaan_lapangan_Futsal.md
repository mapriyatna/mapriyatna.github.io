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
Setelah itu create database dengan nama *database_futsal*, lalu buat tabel dengan nama *"data_sewa"* ditambah dengan 9 kolom dengan index pada kolom pertama "**hsl_kode_booking sebagai primary key**". ![](/assets/images/uts1.png).

**Kita beralih ke Netbeans IDE**, buat project baru dengan cara File → New Project → Java Application → Next. lalu nama project "UTS" dan "Finish".

Dalam Source Package kita buat baru *jFrame From...* dengan nama (disini saya isikan) **"UTS_Mapriyatna_181011401125"**, lalu Finish.

Sebelum kita mengisi jFrame, jangan lupa untuk menambahkan **MySQL JDBC Driver** didalam Libraries untuk mengatur koneksi ke database MySQL.
![](/assets/images/uts.png)

Pada *jFrame* "UTS_Mapriyatna_181011401125" kita buat desain seperti ini.
![](/assets/images/uts2.png).

**Note** *Perhatikan apa saja yang digunakan pada Swing Controls untuk membuat desain seperti ini, dan jangan lupa atur properties dan nama variable nya ;)*.

---

**Tahap Selanjutnya,** ***Kita akan memulai dengan memasukkan source code.***

*Perhatikan baik-baik*

Pada Package instansi masukkan code berikut :

```java
import java.sql.*;
import java.awt.*;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;
import javax.swing.JOptionPane;
import javax.swing.table.DefaultTableModel;
```
---
Pada ***"public class UTS_Mapriyatna_181011401125 extends javax.swing.JFrame"*** masukkan coding dibawah ini.
```java
private Connection con;
private Statement stat;
private ResultSet res;
private DefaultTableModel dtm;
```
---
Pada methode constructor *public UTS_Mapriyatna_181011401125()* terdapat satu code dengan *`initComponents();`*.
dibawahnya, masukkan coding berikut :
```ruby
koneksi();
kosongkan();
tampil();

    //rata kiri dan kanan
    Dimension screenSize = Toolkit.getDefaultToolkit().getScreenSize();
    Dimension frameSize = getSize();
    setLocation (
        (screenSize.width - frameSize.width) / 3,
        (screenSize.height - frameSize.height) / 4);
```
---
Lalu, buat ***"konstuktor koneksi, kosongkan, dan tampil"***, dengan cara masukkan masing-masing konstuktor dibawah ini.

*Buat konstruktor koneksi* :
```ruby
private void koneksi () {
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
*Buat konstruktor Kosongkan* :
```ruby
private void kosongkan(){
        kd.setText("");
        tgl.setSelectedIndex(-1);
        bln.setSelectedIndex(-1);
        thn.setSelectedIndex(-1);
        jamMulai.setSelectedIndex(-1);
        jamSelesai.setSelectedIndex(-1);
        durasi.setSelectedIndex(-1);
        nama.setText("");
        kontak.setText("");
        uangMuka.setText("");
        sisa.setText("");
        status.setSelectedIndex(-1);
    }
```

---
*Buat konstruksi Tampil* :
```ruby
private void tampil(){
    try{
            Object [] rows={"Kode Booking","Tanggal Booking","Jam Booking","Durasi (jam)","Nama","No. Kontak","Uang Muka","Sisa Pembayaran","Status Pembayaran"};
            dtm=new DefaultTableModel(null,rows);
            tblTampil.setModel(dtm);
            tblTampil.setBorder(null);
            jScrollPane1.setVisible(true);
            jScrollPane1.setViewportView(tblTampil);
            int no = 1;
            String hsl_kode_booking="",hsl_tanggal="",hsl_jam="",hsl_durasi="",hsl_nama=""
                    + "",hsl_kontak="",hsl_dp="",hsl_sisa="",hsl_status="";
            try{
                String sql="select * from data_sewa";
                Statement st=con.createStatement();
                ResultSet rs=st.executeQuery(sql);
                while(rs.next()){
                    hsl_kode_booking=rs.getString("hsl_kode_booking");
                    hsl_tanggal=rs.getString("hsl_tanggal");
                    hsl_jam=rs.getString("hsl_jam");
                    hsl_durasi=rs.getString("hsl_durasi");
                    hsl_nama=rs.getString("hsl_nama");
                    hsl_kontak=rs.getString("hsl_kontak");
                    hsl_dp=rs.getString("hsl_dp");
                    hsl_sisa=rs.getString("hsl_sisa");
                    hsl_status=rs.getString("hsl_status");
                    String [] tampil={""+hsl_kode_booking,hsl_tanggal,hsl_jam,hsl_durasi,hsl_nama
                            ,hsl_kontak,hsl_dp,hsl_sisa,hsl_status
                        };
                    dtm.addRow(tampil);
                }
            } catch(SQLException e){
                e.printStackTrace();
                JOptionPane.showMessageDialog(null,"Ada Kesalahan ! "+e);
            }
        } catch(Exception e){
            e.printStackTrace();
        }
}
```


---
**Pertama, setting event mouse click pada tabel**

Klik kanan pada tabel, pilih Events, Mouse, lalu pilih mouseClicked. lalu masukkan source code berikut.
```ruby
int i = tblTampil.getSelectedRow();
        if(i==-1){
            return;
        }
        String code = (String)tblTampil.getValueAt(i,0);
        String code1 = (String)tblTampil.getValueAt(i,1);
        String code2 = (String)tblTampil.getValueAt(i,2);
        String code3 = (String)tblTampil.getValueAt(i,3);
        String code4 = (String)tblTampil.getValueAt(i,4);
        String code5 = (String)tblTampil.getValueAt(i,5);
        String code6 = (String)tblTampil.getValueAt(i,6);
        String code7 = (String)tblTampil.getValueAt(i,7);
        String code8 = (String)tblTampil.getValueAt(i,8);

        kdtxt.setText(code);
        tanggalBookingtxt.setText(code1);
        jamBookingtxt.setText(code2);
        durasitxt.setText(code3);
        namatxt.setText(code4);
        kontaktxt.setText(code5);
        uangMukatxt.setText(code6);
        sisatxt.setText(code7);
        statustxt.setSelectedItem(code8);
```

---
***Kedua, Kita setting bagian perintah button***

*Masukkan source code pada bagian button Simpan.*
```ruby
try {
    stat.executeUpdate("insert into data_sewa values ("
    + "'" + kd.getText()+"',"
    + "'" + tgl.getSelectedItem()+" "+bln.getSelectedItem()+" "+thn.getSelectedItem()+ "',"
    + "'" + jamMulai.getSelectedItem()+" - "+jamSelesai.getSelectedItem()+ "',"
    + "'" + durasi.getSelectedItem()+ "',"
    + "'" + nama.getText()+"',"
    + "'" + kontak.getText()+"',"
    + "'" + uangMuka.getText()+"',"
    + "'" + sisa.getText()+"',"
    +"'"+ status.getSelectedItem()+ "')");
    kosongkan();
    tampil();
    JOptionPane.showMessageDialog(null, "Data Telah Tersimpan");
} catch (HeadlessException | SQLException e) {
    JOptionPane.showMessageDialog(null, "Perintah Salah : "+e);
}
```
---
*Masukkan source code pada bagian button Refresh.*
```ruby
tampil();
kdtxt.setText("");
tanggalBookingtxt.setText("");
jamBookingtxt.setText("");
durasitxt.setText("");
namatxt.setText("");
kontaktxt.setText("");
uangMukatxt.setText("");
sisatxt.setText("");
```

---
*Masukkan source code pada bagian button Baru.*
```ruby
new UTS_Mapriyatna_181011401125().setVisible(true);
dispose();
```

---
*Masukkan source code pada bagian button Keluar.*
```ruby
JOptionPane.showMessageDialog(null, "Keluar Dari Program?");
System.exit(0);
```

---
*Masukkan source code pada bagian button Search.*
```ruby
try {
    res=stat.executeQuery("select * from data_sewa where "+ "hsl_kode_booking='" +kdtxt.getText()+"'" );
    while (res.next()){
    tanggalBookingtxt.setText(res.getString("hsl_tanggal"));
    jamBookingtxt.setText(res.getString("hsl_jam"));
    durasitxt.setText(res.getString("hsl_durasi"));
    namatxt.setText(res.getString("hsl_nama"));
    kontaktxt.setText(res.getString("hsl_kontak"));
    uangMukatxt.setText(res.getString("hsl_dp"));
    sisatxt.setText(res.getString("hsl_sisa"));
    statustxt.setSelectedItem(res.getString("hsl_status"));
    }
} catch (Exception e) {
    JOptionPane.showMessageDialog(rootPane, e);
}
```

---
*Masukkan source code pada bagian button Proses.*
```ruby
int a= Integer.parseInt(durasi.getText());
        int b= Integer.parseInt(uangMuka.getText());
        int c= 100000;
        int d= a*c;
        int Hasil= d-b;
        sisa.setText(""+Hasil);
```

---
*Masukkan source code pada bagian button Edit Data.*
```ruby
int ok=JOptionPane.showConfirmDialog(null,"Apakah Yakin Untuk Update Record ini???","Confirmation",JOptionPane.YES_NO_OPTION);
try {
String sql="update data_sewa set hsl_kode_booking=?,hsl_tanggal=?,hsl_jam=?,hsl_durasi=?,hsl_nama=?"
                    + ",hsl_kontak=?,hsl_dp=?,hsl_sisa=?,hsl_status=? "
                    + "where hsl_kode_booking='"+kdtxt.getText()+"'";
PreparedStatement st=con.prepareStatement(sql);
if(ok==0) {
    try {
        st.setString(1,kdtxt.getText());
        st.setString(2,tanggalBookingtxt.getText());
        st.setString(3,jamBookingtxt.getText());
        st.setString(4,durasitxt.getText());
        st.setString(5,namatxt.getText());
        st.setString(6,kontaktxt.getText());
        st.setString(7,uangMukatxt.getText());
        st.setString(8,sisatxt.getText());
        st.setString(9, (String) statustxt.getSelectedItem());
        st.executeUpdate();
        kosongkan();
        tampil();
        JOptionPane.showMessageDialog(null,"Update Data Sukses");
    } catch (Exception e) {
        JOptionPane.showMessageDialog(null, "Update Data Gagal");
    }
}
}
```

---
*Masukkan source code pada bagian button Hapus Data.*
```ruby
int ok=JOptionPane.showConfirmDialog(null,"Apakah Yakin Mendelete Record Ini???",
                "Confirmation",JOptionPane.YES_NO_CANCEL_OPTION);
if (ok==0){
    try{
        String sql="delete from data_sewa where hsl_kode_booking='"+kdtxt.getText()+"'";
        PreparedStatement st=con.prepareStatement(sql);
        st.executeUpdate();
        kosongkan();
        tampil();
        JOptionPane.showMessageDialog(null, "Delete Data Sukses");
    } catch (Exception e){
        JOptionPane.showMessageDialog(null, "Delete Data Gagal");
    }
}
```


Setelah semuanya selesai.
Langkah terakhir yaitu kita coba jalankan aplikasinya dengan cara pilih atau klik tombol "Run" juga bisa dengan 'Shift + F6', tunggu beberapa detik dan muncul lah hasil program aplikasi yang kita buat.

***"Tampilan hasil program"***
![](/assets/images/uts3.png).



**Selesai**.

*Selamat kamu berhasil membuat Program Aplikasi Database dengan Java Netbeans & MySQL.*

Untuk source code nya kalian bisa [DOWNLOAD LANGSUNG](http://bit.ly/File_UTS).

Untuk demo aplikasinya, silahkan lihat video dibawah ini :
[![Program Penyewaan Lapangan Futsal](https://res.cloudinary.com/marcomontalbano/image/upload/v1604765554/video_to_markdown/images/youtube--jHS3-TIFesU-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/jHS3-TIFesU "Program Penyewaan Lapangan Futsal").

Terimakasih.
Selamat Mencoba ;)