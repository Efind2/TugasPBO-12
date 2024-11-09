# Upload File Csv
Hallo Semua 😄👋 Pada Tugas Pemograman Berorientasi Objek ini, saya menerapkan program CRUD (Create, Read, Update, Delete)  dan  penggunaan jasper juga upload file csv pada java GUI(Graphical User Interfaces) dengan IDE netbeans. Untuk mengimplementasikan program tersebut saya menggunakan bahasa pemrograman java dan menggunakan aplikasi pengelola database yaitu postgreSQL dan juga plugin iReport.
dan saya menggunakan tabel  entitas Matakuliah dengan atribut Kode MK, SKS, NamaMk, Semester Ajar.
## Aplikasi
- IDE NetBeans 16
- PostgreSql
- Java Development Kit 11
## Plugin
- [IReport 5.6.0](https://drive.google.com/drive/folders/1gbbMttGeyns5mqb-_hfIAuMjkTzb-XPZ?usp=sharing)
## Library
- PostgreSQL JDBC Driver
- [JasperReport](https://drive.google.com/drive/folders/1_i8xBCdLXeMcGdmnTWa2SEnL4oc2sW78?usp=sharing)
## Feature
-  Melakukan insert data
-  Melakukan update data
-  Menghapus data
-  Menampilkan data ke tabel
-  Melakukan import file csv
-  Mencetak laporan data

## Cara Instalasi 
Install Plugin Ireport di IDE Netbeans dengan mencari menu tools > plugins > donload > add plugins . Tambahkan plugins ireport yang ada di dalam folder yang memiliki tipe file nbm jika tterjadi error install dulu `org-jdeskop-layout-realese.nbm` kemudian baru instal file nbm yang ada didalam folder ireport
## Membuat File jasper
Klik kiri pada package project anda kemudian new > cari report wizard jika belum ada klik other pilih report wizard ![Cuplikan layar 2024-10-26 220058](https://github.com/user-attachments/assets/e4b2bb54-2e9c-4253-8e91-ebbe55364533) 
Kemudain next pilih layout kemudain sesuaikan nama file jasper dengan apa yang anda inginkan kemudian sambungkan query database disini saya menggunkan database Mahasiswa dengan SQL Query `SELECT * FROM mahasiswa` ![image](https://github.com/user-attachments/assets/eae7b901-3c6a-41ce-a468-80a2c77e999c)
kemudian next pindah seluruh kolom ke kiri dan next lagi --finish.
Setelah File jadi anda bisa membuat tampilan layout anda sesuka hati, namun layout anda harus berisi tabel yang ingin anda tampilkan atau cetak
![image](https://github.com/user-attachments/assets/7fd7d5f1-db54-43d7-bdac-57ac60bf4a10)

## Cara Penggunaan
Buat java frame yang berisi program untuk CRUD (create, read, update, delete) Cetak dan Upload(untuk button mengimport file csv)  kemudian hubungkan Netbeans dengan database di PostgreSql dan juga tambahkan liblary di projeck yang digunakan. tambahkan kode dibawah ini pada button Upload

    JFileChooser jfc = new JFileChooser(FileSystemView.getFileSystemView().getHomeDirectory());
        int returnValue = jfc.showOpenDialog(null);
        if (returnValue == JFileChooser.APPROVE_OPTION) {
            File filePilihan = jfc.getSelectedFile();
            System.out.println("yang dipilih : " + filePilihan.getAbsolutePath());
            try {
                BufferedReader br = new BufferedReader(new FileReader(filePilihan));
                String baris = new String("");
                String pemisah = ";";
                while ((baris = br.readLine()) != null) //returns a Boolean value
                {
                    String[] dataMhs = baris.split(pemisah);
                    String kodemk = dataMhs[0];
                    String sks = dataMhs[1];
                    String namamk = dataMhs[2];
                    String semester = dataMhs[3];
                    
                    if (!kodemk.isEmpty() && !namamk.isEmpty()) {
                        conn = DriverManager.getConnection(koneksi, user, password);
                        conn.setAutoCommit(false);
                        String sql = "INSERT INTO matakuliah VALUES(?,?,?,?)";
                        pstmt = conn.prepareStatement(sql);
  
                        pstmt.setString(1, kodemk);
                        pstmt.setInt(2, Integer.parseInt(sks));
                        pstmt.setString(3, namamk);
                        pstmt.setInt(4, Integer.parseInt(semester));
                        pstmt.executeUpdate();
                        conn.commit();
                        pstmt.close();
                        conn.close();
                    }
                }
                JOptionPane.showMessageDialog(null, "Data berhasil diupload");
                tampil();
            } catch (FileNotFoundException ex) {
                Logger.getLogger(ReportMataKuliah.class.getName()).log(Level.SEVERE, null, ex);
            } catch (IOException ex) {
                Logger.getLogger(ReportMataKuliah.class.getName()).log(Level.SEVERE, null, ex);
            } catch (SQLException ex) {
                Logger.getLogger(ReportMataKuliah.class.getName()).log(Level.SEVERE, null, ex);
            }
        }                       
     
Saat button upload di klik maka tampilan akan muncul seperti ini
![image](https://github.com/user-attachments/assets/f209e6b2-9ede-4b0e-99a0-ffb93dbac167)
carilah file csv yang akan anda upload usahakan file csvnya sesuai dengan database anda dan tidak ada data primary key yang sama


mungkin itu saya yang dapat saya jelaskan 😄



