## *TUGAS PRAKTIKUM {PERTEMUAN 14}*
| Variable       |    DATA DIRI         |
| ---------------| ----------------     |
| Nama           | Lutpiah Ainus Shiddik|                                     
| NIM            | 312310474            |
| Kelas          | TI.23.A.5            |
| Mata Kuliah    |Basis data            |

## *SOAL LATIHAN*
<img width="553" alt="soal praktikum6" src="https://github.com/lutpi9/praktikum6-mysql6/assets/147919251/4912d408-1255-4a5e-b12b-7cddb33430e6">


## Query MySQL Pada Tabel Perusahaan
```
CREATE TABLE Perusahaan(
id_p VARCHAR(10) PRIMARY KEY,
nama VARCHAR(45) NOT NULL,
alamat VARCHAR(45) DEFAULT NULL
);

INSERT INTO Perusahaan VALUES
('P01', 'Kantor Pusat', NULL),
('P02', 'Cabang Bekasi', NULL);
SELECT * FROM Perusahaan;
```
## outputnya
<img width="319" alt="table perusahaan" src="https://github.com/lutpi9/praktikum6-mysql6/assets/147919251/a1ee9633-6814-458a-bbbe-c6cf4676857b">

## Query MySQL Pada Tabel Departemen
```
CREATE TABLE Departemen(
id_dept VARCHAR(10) PRIMARY KEY,
nama VARCHAR(45) NOT NULL,
id_p VARCHAR(10) NOT NULL,
manajer_nik VARCHAR(10) DEFAULT NULL
);

INSERT INTO Departemen VALUES
('D01', 'Produksi', 'P02', 'N01'),
('D02', 'Marketing', 'P01', 'N03'),
('D03', 'RnD', 'P02', NULL),
('D04', 'Logistik', 'P02', NULL);
SELECT * FROM Departemen;
```
## outputnya
<img width="347" alt="departemen" src="https://github.com/lutpi9/praktikum6-mysql6/assets/147919251/5aeeb9af-e269-42b2-afb3-a09166da9692">

## Query MySQL Pada Tabel Karyawan
```
CREATE TABLE Karyawan(
nik VARCHAR(10) PRIMARY KEY,
nama VARCHAR(45) NOT NULL,
id_dept VARCHAR(10) NOT NULL,
sup_nik VARCHAR(10) DEFAULT NULL
);

INSERT INTO Karyawan VALUES
('N01', 'Ari', 'D01', NULL),
('N02', 'Dina', 'D01', NULL),
('N03', 'Rika', 'D03', NULL),
('N04', 'Ratih', 'D01', 'N01'),
('N05', 'Riko', 'D01', 'N01'),
('N06', 'Dani', 'D02', NULL),
('N07', 'Anis', 'D02', 'N06'),
('N08', 'Dika', 'D02', 'N06');
SELECT * FROM Karyawan;
```
# outputnya
<img width="340" alt="karyawan" src="https://github.com/lutpi9/praktikum6-mysql6/assets/147919251/a5a6c00a-a954-4efc-9a60-c68b2977c7fb">

# Query MySQL Pada Tabel Project
```
CREATE TABLE Project(
id_proj VARCHAR(10) PRIMARY KEY,
nama VARCHAR(45) NOT NULL,
tgl_mulai DATETIME,
tgl_selesai DATETIME,
status TINYINT(1)
);

INSERT INTO Project VALUES
('PJ01', 'A', '2019-01-10', '2019-03-10', '1'),
('PJ02', 'B', '2019-02-15', '2019-04-10', '1'),
('PJ03', 'C', '2019-03-21', '2019-05-10', '1');
SELECT * FROM Project;
```
# outputnya
<img width="420" alt="project" src="https://github.com/lutpi9/praktikum6-mysql6/assets/147919251/e3922777-7953-4b20-91fd-05fd96f317d7">

# Query MySQL Pada Tabel Project Deatil
```
CREATE TABLE Project_detail(
id_proj VARCHAR(10) NOT NULL,
nik VARCHAR(10) NOT NULL
);

INSERT INTO Project_detail VALUES
('PJ01', 'N01'),
('PJ01', 'N02'),
('PJ01', 'N03'),
('PJ01', 'N04'),
('PJ01', 'N05'),
('PJ01', 'N07'),
('PJ01', 'N08'),
('PJ02', 'N01'),
('PJ02', 'N03'),
('PJ02', 'N05'),
('PJ03', 'N03'),
('PJ03', 'N07'),
('PJ03', 'N08');
SELECT * FROM Project_detail;
```
# outputnya
<img width="490" alt="project detail" src="https://github.com/lutpi9/praktikum6-mysql6/assets/147919251/166d45c0-e17c-46be-97c4-f31d8067c393">

# *Menampilkan Nama Manajer Tiap Departemen*
```
Select Departemen.nama AS Departemen, Karyawan.nama AS Manajer
FROM Departemen
LEFT JOIN Karyawan ON Karyawan.nik = Departemen.manajer_nik;
```
# outputnya
<img width="466" alt="nama manajer" src="https://github.com/lutpi9/praktikum6-mysql6/assets/147919251/db1ff24a-c8b7-472d-a594-87c2cbd08671">

# *Menampilkan Nama Supervisor Tiap Karyawan*
```
SELECT Karyawan.nik, Karyawan.nama, Departemen.nama AS Departemen, Supervisor.nama AS Supervisor
FROM Karyawan
LEFT JOIN Karyawan AS Supervisor ON Supervisor.nik = Karyawan.sup_nik
LEFT JOIN Departemen ON Departemen.id_dept = Karyawan.id_dept;
```
# outputnya
<img width="671" alt="nama supervisor" src="https://github.com/lutpi9/praktikum6-mysql6/assets/147919251/8c3a8118-30e3-4ce4-ab66-583da282d556">

# *Menampilkan Daftar Karyawan Yang Bekerja Pada Project A*
```
SELECT Karyawan.nik, Karyawan.nama
FROM Karyawan
JOIN Project_detail ON Project_detail.nik = Karyawan.nik
JOIN Project ON Project.id_proj = Project_detail.id_proj
WHERE Project.nama = 'A';
```
# outputnya
<img width="367" alt="daftar karyawan" src="https://github.com/lutpi9/praktikum6-mysql6/assets/147919251/3c8f56bb-db4f-47cf-94e8-33a9f82f8f5a">

# *Soal Latihan Praktikum*
# 1. Departemen Apa Saja Yang Terlibat Dalam Tiap-tiap Project.
```
SELECT Project.nama AS Project, GROUP_CONCAT(Departemen.nama) AS Departemen
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
INNER JOIN Departemen ON Karyawan.id_dept = Departemen.id_dept
GROUP BY Project.id_proj;
```
# outputnya 
<img width="544" alt="1" src="https://github.com/lutpi9/praktikum6-mysql6/assets/147919251/0bfb7dad-26f9-4e7d-8437-cb16bec52403">

# 2. Jumlah Karyawan Tiap Departemen Yang Bekerja Pada Tiap-tiap Project.
```
SELECT Project.nama AS Project, Departemen.nama AS Departemen, COUNT(*) AS 'Jumlah Karyawan'
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
INNER JOIN Departemen ON Karyawan.id_dept = Departemen.id_dept
GROUP BY Project.id_proj, Departemen.id_dept;
```
# outputnya
<img width="635" alt="2" src="https://github.com/lutpi9/praktikum6-mysql6/assets/147919251/1b283a86-acd3-40ed-926e-98ba7cfbf8f1">

# 3. Ada Berapa Project Yang Sedang Dikerjakan Oleh Departemen RnD? (ket: project berjalan adalah yang statusnya 1).
```
SELECT COUNT(*) AS 'Jumlah Project'
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
INNER JOIN Departemen ON Karyawan.id_dept = Departemen.id_dept
WHERE Departemen.nama = 'RnD' AND Project.status = 1;
```
# outputnya
<img width="426" alt="3" src="https://github.com/lutpi9/praktikum6-mysql6/assets/147919251/17c7a66c-aae0-4d68-88f0-1c05cd0e83a9">

# 4. Berapa banyak Project yang sedang dikerjakan oleh Ari ?
```
SELECT COUNT(*) AS 'Jumlah Project'
FROM Project_detail
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
WHERE Karyawan.nama = 'Ari' AND Project_detail.id_proj IN (SELECT id_proj FROM Project WHERE status = 1);
```
# outputnya
<img width="647" alt="4" src="https://github.com/lutpi9/praktikum6-mysql6/assets/147919251/a1987c77-cc61-44e4-a0d9-b4da89586374">

# 5. Siapa Saja Yang Mengerjakan Project B ?
```
SELECT Karyawan.nama
FROM Project_detail
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
WHERE Project_detail.id_proj IN (SELECT id_proj FROM Project WHERE nama = 'B');
```
# outputnya
<img width="485" alt="5" src="https://github.com/lutpi9/praktikum6-mysql6/assets/147919251/2817d920-1a9f-471e-b70c-ccb465f49728">

## *SELESAI SEKIAN TERIMAKASIH*











