## *TUGAS PRAKTIKUM {PERTEMUAN 14}*
| Variable       |    DATA DIRI         |
| ---------------| ----------------     |
| Nama           | Lutpiah Ainus Shiddik|                                     
| NIM            | 312310474            |
| Kelas          | TI.23.A.5            |
| Mata Kuliah    |Basis data            |

## *SOAL LATIHAN*
<img width="553" alt="soal praktikum6" src="https://github.com/lutpi9/tugas-pert-13-mysql6/assets/147919251/49eaadb7-0aaf-4023-87d3-3ce9363e0a80">


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
<img width="319" alt="table perusahaan" src="https://github.com/lutpi9/tugas-pert-13-mysql6/assets/147919251/e581adf5-c140-43dd-ba85-b12ee8df90f8">

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
<img width="347" alt="departemen" src="https://github.com/lutpi9/tugas-pert-13-mysql6/assets/147919251/eb0d88b8-b38a-4794-9676-38bc2079363d">

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
<img width="340" alt="image" src="https://github.com/lutpi9/tugas-pert-13-mysql6/assets/147919251/8e8c78e4-8fc7-4487-89dd-b7f861a94cb7">

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
<img width="420" alt="image" src="https://github.com/lutpi9/tugas-pert-13-mysql6/assets/147919251/54c5f3d0-dc94-40d1-ad42-3e7003a9e26e">

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
<img width="490" alt="image" src="https://github.com/lutpi9/tugas-pert-13-mysql6/assets/147919251/91aa2361-0444-40b3-a3d0-d0935eed9d8d">

# *Menampilkan Nama Manajer Tiap Departemen*
```
Select Departemen.nama AS Departemen, Karyawan.nama AS Manajer
FROM Departemen
LEFT JOIN Karyawan ON Karyawan.nik = Departemen.manajer_nik;
```
# outputnya
<img width="466" alt="image" src="https://github.com/lutpi9/tugas-pert-13-mysql6/assets/147919251/789bdf4d-3410-4360-9f82-7605e08ddf3b">

# *Menampilkan Nama Supervisor Tiap Karyawan*
```
SELECT Karyawan.nik, Karyawan.nama, Departemen.nama AS Departemen, Supervisor.nama AS Supervisor
FROM Karyawan
LEFT JOIN Karyawan AS Supervisor ON Supervisor.nik = Karyawan.sup_nik
LEFT JOIN Departemen ON Departemen.id_dept = Karyawan.id_dept;
```
# outputnya
<img width="671" alt="image" src="https://github.com/lutpi9/tugas-pert-13-mysql6/assets/147919251/6c42eb15-5c05-4aa0-8e9b-84e02a32b342">

# *Menampilkan Daftar Karyawan Yang Bekerja Pada Project A*
```
SELECT Karyawan.nik, Karyawan.nama
FROM Karyawan
JOIN Project_detail ON Project_detail.nik = Karyawan.nik
JOIN Project ON Project.id_proj = Project_detail.id_proj
WHERE Project.nama = 'A';
```
# outputnya
<img width="367" alt="image" src="https://github.com/lutpi9/tugas-pert-13-mysql6/assets/147919251/0f7ad4b8-ed08-42e3-9d85-50186361ed56">

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
<img width="544" alt="image" src="https://github.com/lutpi9/tugas-pert-13-mysql6/assets/147919251/1dd8c937-ae11-4417-bd30-0ae9b72dfd19">

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
<img width="635" alt="image" src="https://github.com/lutpi9/tugas-pert-13-mysql6/assets/147919251/7d346e06-613b-4b6d-a92a-e70662228e42">

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
<img width="426" alt="image" src="https://github.com/lutpi9/tugas-pert-13-mysql6/assets/147919251/efc82fcc-71f9-49b3-ab47-0f0c28c2239e">

# 4. Berapa banyak Project yang sedang dikerjakan oleh Ari ?
```
SELECT COUNT(*) AS 'Jumlah Project'
FROM Project_detail
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
WHERE Karyawan.nama = 'Ari' AND Project_detail.id_proj IN (SELECT id_proj FROM Project WHERE status = 1);
```
# outputnya
<img width="647" alt="image" src="https://github.com/lutpi9/tugas-pert-13-mysql6/assets/147919251/501db567-e3b0-4ba5-944f-3ef7d8053b17">

# 5. Siapa Saja Yang Mengerjakan Project B ?
```
SELECT Karyawan.nama
FROM Project_detail
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
WHERE Project_detail.id_proj IN (SELECT id_proj FROM Project WHERE nama = 'B');
```
# outputnya
<img width="485" alt="image" src="https://github.com/lutpi9/tugas-pert-13-mysql6/assets/147919251/1f0d22d1-907b-490f-bc27-e3ccff0163bd">

## *SELESAI SEKIAN TERIMAKASIH*











