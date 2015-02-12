# Konsep Database

Singkatnya, **database merupakan kumpulan dari data-data yang bisa diolah menjadi informasi**

Perkembangan file database sampai saat sekarang ini antara lain:
* text file --> misalnya file dengan ekstensi .txt, .dat, .go, dll.
* DBMS (*Database Management System*), DBF
* MySQL
* RDBMS (*Relational Database Management System*) --> seperti SQLServer, Ms. Access, dll.

pada tulisan ini kami akan mencoba menjelaskan pengolahan database menggunakan SQL Server Management Studio

didalam database terdapat perintah-perintah utama yang biasa digunakan dalam pengolahan data, seperti :
  - *select*          : perintah untuk mengekstrak data dari database
  - *update*          : perintah untuk memperbarui data di dalam database
  - *delete*          : perintah untuk menghapus data dari database
  - *insert into*     : perintah untuk memasukan data baru ke dalam database
  - *create database* : perintah untuk membuat database 
  - *alter database*  : perintah untuk memodifikasi database
  - *drop table*      : perintah untuk menghapus tabel
  - *create index*    : perintah untuk membuat index
  - *drop index*      : perintah untuk menghapus index
  
##Membuat Database di *SQLServer*

Membuat database di SQLServer dapat menggunakan script dan dapat juga dibuat langsung tanpa script.

Disini saya akan menjelaskan langkah-langkah membuat database di SQLServer menggunakan script, *so check this out* :)


![](http://gibraltardatabases.com/images/databases.jpg)

* Buka program SQL Server Management Studio
* Buat database baru dengan cara klik kanan pada `Databases` --> klik `New Database...` --> ketikkan nama database kamu pada kolom `Database name` --> klik `Ok`. Database baru kamu akan muncul di `Object Explorer`
* Untuk mengisi database, kamu harus membuat tabel terlebih dahulu. Klik kanan pada nama database kamu di `Object Explorer` --> klik `New Query` --> ketikkan code berikut:

Contoh database sederhana yaitu tabel data `mahasiswa` yang berisi daftar nim, nama, tanggal lahir, tempat lahir, kode jurusan, jurusan, kode fakultas, dan fakultas.

```sql
--membuat tabel mahasiswa
CREATE TABLE [dbo].[mahasiswa](
	[nim] [char](10) NOT NULL,
	[nama] [varchar](50) NULL,
	[tgllahir] [date] NULL,
	[tmplahir] [varchar](50) NULL,
	[kodejurusan] [char](2) NOT NULL,
 CONSTRAINT [PK_mahasiswa] PRIMARY KEY CLUSTERED 
(
	[nim] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]
```

* Blok semua code diatas, lalu tekan tombol `F5` untuk menjalankannya. Refresh `Tables` lalu tabel `dbo.mahasiswa` akan muncul di `Object Explorer`.
* Lakukan langkah 3 dan 4 untuk membuat tabel jurusan dan fakultas.


```sql
--membuat tabel jurusan
CREATE TABLE [dbo].[jurusan](
	[kodejurusan] [char](2) NOT NULL,
	[namajurusan] [varchar](50) NOT NULL,
	[kodefakultas] [char](2) NOT NULL,
 CONSTRAINT [PK_jurusan] PRIMARY KEY CLUSTERED 
(
	[kodejurusan] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]


--membuat tabel fakultas
CREATE TABLE [dbo].[fakultas](
	[kodefakultas] [char](2) NOT NULL,
	[namafakultas] [varchar](50) NOT NULL,
 CONSTRAINT [PK_fakultas] PRIMARY KEY CLUSTERED 
(
	[kodefakultas] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]
```

* Isi tabel dengan data seperti berikut:

```sql
--mengisi data tabel fakultas
insert fakultas values ('01', 'FAPERTA')
insert fakultas values ('02', 'FKH')
insert fakultas values ('03', 'FPIK')
insert fakultas values ('04', 'FAPET')
insert fakultas values ('05', 'FAHUTAN')
insert fakultas values ('06', 'FATETA')
insert fakultas values ('07', 'FMIPA')
insert fakultas values ('08', 'FEM')
insert fakultas values ('09', 'FEMA')

--mengisi data tabel jurusan
insert jurusan values ('01', 'Fisika', '07')
insert jurusan values ('02', 'TMB', '06')
insert jurusan values ('03', 'BDP', '03')
insert jurusan values ('04', 'Ilkom', '07')
insert jurusan values ('05', 'INTP', '04')
insert jurusan values ('06', 'FKH', '02')
insert jurusan values ('07', 'AGH', '01')
insert jurusan values ('08', 'SVK', '05')
insert jurusan values ('09', 'Eksyar', '08')
insert jurusan values ('10', 'Gizi', '09')
insert jurusan values ('11', 'Matematika', '07')

--mengisi tabel mahasiswa
insert mahasiswa values ('001', 'Abdika', '1990-01-22', 'Jakarta', '01')
insert mahasiswa values ('002', 'Permana', '1990-01-22', 'Jakarta', '02')
insert mahasiswa values ('003', 'Putra', '1990-01-22', 'Jakarta', '03')
insert mahasiswa values ('004', 'Tiara', '1990-01-22', 'Jakarta', '03')
insert mahasiswa values ('005', 'Amelia', '1990-01-22', 'Jakarta', '05')
insert mahasiswa values ('006', 'Dhini', '1990-01-22', 'Jakarta', '05')
insert mahasiswa values ('007', 'Wulan', '1990-01-22', 'Jakarta', '03')
insert mahasiswa values ('008', 'Elsa', '1990-01-22', 'Jakarta', '07')
insert mahasiswa values ('009', 'Lulu', '1990-01-22', 'Jakarta', '06')
insert mahasiswa values ('010', 'Hadi', '1990-01-22', 'Jakarta', '09')
```

* Blok code dan tekan `F5`.
* Untuk menampilkan data tabel-tabel tersebut dapat dilakukan menggunakan perintah berikut:

```sql
--menampilkan data fakultas
select * from fakultas

--menampilkan data jurusan
select * from jurusan

--menampilkan data mahasiswa
select * from mahasiswa
```

* Blok code dan tekan `F5`, lalu akan muncul data tabel fakultas, jurusan, dan mahasiswa.
* Kita ingin menampilkan data mahasiswa disertai dengan nama jurusan dan fakultasnya tanpa harus mengetikkan lagi datanya pada tabel mahasiswa tapi dengan memanggilnya dari tabel jurusan dan tabel fakultas. Caranya adalah dengan mengetikkan code berikut:

```sql
--joining semua tabel
select nim, nama, namajurusan, namafakultas from 
mahasiswa inner join jurusan on mahasiswa.kodejurusan=jurusan.kodejurusan
inner join fakultas on jurusan.kodefakultas=fakultas.kodefakultas
```

* Blok code lalu tekan `F5` maka secara otomatis akan ditampilkan data yang berisi nim, nama, nama jurusan, dan nama fakultas mahasiswa tanpa kita mengetikkan lagi data jurusan dan fakultas nya pada tabel mahasiswa.

  
  
