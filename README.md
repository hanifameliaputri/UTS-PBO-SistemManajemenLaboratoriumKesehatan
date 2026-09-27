# UTS-PBO-SistemManajemenLaboratoriumKesehatan

**Nama:** Hanif Amelia Putri  

**Kelas:** B  

**NIM:** 2509116075  

## 1. Deskripsi Program

Sistem Manajemen Laboratorium Kesehatan adalah program berbasis Java (console/command line) yang digunakan untuk mengelola data operasional sebuah laboratorium kesehatan, meliputi data **pasien**, **petugas** (Dokter dan Analis), **jenis pemeriksaan**, dan **hasil pemeriksaan**.

Program ini dibuat untuk memenuhi tugas UTS Pemrograman Berorientasi Objek (PBO), dengan menerapkan konsep-konsep dasar OOP secara nyata dalam sebuah studi kasus, yaitu:

- **Inheritance** (minimal 2 tipe subclass)
- **Polymorphism** (Method Overriding dan Overloading)
- **Condition** (if-else)
- **Looping**

Selain empat elemen wajib tersebut, program juga menerapkan `encapsulation`, `constructor`, `access modifier`, `ArrayList`, validasi input, serta struktur package (MVC-like: model, view, controller).

Kegunaan program: memungkinkan petugas administrasi lab mencatat pendaftaran pemeriksaan pasien (siapa diperiksa apa oleh siapa), lalu mencatat dan menelusuri hasil pemeriksaannya, tanpa perlu sistem manual berbasis kertas.

---

## 2. Fitur Program

Program memiliki beberapa fitur utama, yaitu:

- Pendaftaran pemeriksaan
- Mengelola data pasien
- Mengelola data petugas
- Mengelola data pemeriksaan
- Mengelola hasil pemeriksaan
- Menambah, melihat, mencari, mengubah, dan menghapus data tertentu
- Validasi input pengguna
- Menampilkan riwayat hasil pemeriksaan berdasarkan pasien
- Menggunakan dummy data pada saat program pertama kali dijalankan

---

## 3. Alur Program

Program dijalankan melalui class `Main.java`. Class tersebut memanggil `LaboratoriumController` untuk menjalankan program.

Alur utama program:

```text
Main
  ↓
LaboratoriumController
  ↓
Menu Utama
  ├── 1. Pendaftaran Pemeriksaan
  ├── 2. Kelola Pasien
  ├── 3. Kelola Petugas
  ├── 4. Kelola Pemeriksaan
  ├── 5. Kelola Hasil Pemeriksaan
  └── 6. Keluar
```

### 1. Pendaftaran Pemeriksaan

Pada menu ini pengguna dapat melakukan pendaftaran pemeriksaan.

Pengguna dapat memilih:

- Pasien baru
- Pasien yang sudah terdaftar

Setelah pasien dipilih, pengguna memilih jenis pemeriksaan dan petugas yang menangani pemeriksaan.

Setelah semua data dipilih, sistem menampilkan konfirmasi pendaftaran.

### 2. Kelola Pasien

Menu ini digunakan untuk mengelola data pasien.

Fitur yang tersedia:

- Tambah pasien
- Lihat semua pasien
- Cari pasien
- Hapus pasien

### 3. Kelola Petugas

Menu ini digunakan untuk mengelola data petugas laboratorium.

Pengguna dapat menambahkan:

- Analis
- Dokter

Data kedua jenis petugas tersebut disimpan dalam satu `ArrayList<Petugas>`.

### 4. Kelola Pemeriksaan

Menu ini digunakan untuk mengelola jenis pemeriksaan laboratorium.

Fitur yang tersedia:

- Tambah pemeriksaan
- Lihat semua pemeriksaan
- Cari pemeriksaan
- Ubah pemeriksaan
- Hapus pemeriksaan

### 5. Kelola Hasil Pemeriksaan

Menu ini digunakan untuk mencatat dan melihat hasil pemeriksaan pasien.

Fitur yang tersedia:

- Input hasil pemeriksaan
- Lihat semua hasil
- Lihat riwayat hasil berdasarkan pasien

### 6. Keluar

Menu ini digunakan untuk menghentikan program.

---

## 4. Struktur Program

Program menggunakan pembagian package untuk memisahkan bagian-bagian program.

```text
LaboratoriumKesehatan
│
├── Main
│   └── Main.java
│
├── controller
│   └── LaboratoriumController.java
│
├── model
│   ├── Pasien.java
│   ├── Petugas.java
│   ├── Analis.java
│   ├── Dokter.java
│   ├── Pemeriksaan.java
│   └── HasilPemeriksaan.java
│
└── view
    └── LaboratoriumView.java
```

### Fungsi setiap package

**Main**

Digunakan sebagai titik awal program. `Main.java` membuat objek `LaboratoriumController` dan menjalankan program.

**Controller**

`LaboratoriumController` mengatur proses program, seperti input data, pengelolaan `ArrayList`, pencarian, penambahan, perubahan, penghapusan, serta proses pendaftaran pemeriksaan.

**Model**

Berisi class yang merepresentasikan data dalam program, yaitu pasien, petugas, analis, dokter, pemeriksaan, dan hasil pemeriksaan.

**View**

`LaboratoriumView` digunakan untuk menampilkan menu, judul, pilihan, informasi data, dan pesan kepada pengguna.

---

## 5. Penerapan Elemen Wajib UTS

### a. Inheritance (2 tipe)

Class `Petugas` berperan sebagai **superclass**, dengan dua **tipe subclass**: `Analis` dan `Dokter`.

```text
          Petugas
          /     \
      Analis    Dokter
```

```java
public class Petugas {
    private String id;
    private String nama;
    private int umur;
    private String jenisKelamin;
    // ...
}

public class Analis extends Petugas {
    private String spesialisasiBidang;
    // ...
}

public class Dokter extends Petugas {
    private String nomorSTR;
    // ...
}
```

`Analis` dan `Dokter` mewarisi seluruh atribut dan method umum dari `Petugas` (id, nama, umur, jenis kelamin beserta getter/setter-nya), lalu masing-masing menambahkan atribut khusus miliknya sendiri.

### b. Polymorphism — Overriding

Method `tampilkanInfo()` didefinisikan di `Petugas`, lalu **di-override** oleh `Analis` dan `Dokter` agar menampilkan info tambahan sesuai perannya:

```java
// Petugas
public String tampilkanInfo() {
    return "ID: " + id + " | Nama: " + nama;
}

// Analis (override)
@Override
public String tampilkanInfo() {
    return super.tampilkanInfo() + " | Peran: Analis | Spesialisasi/Bidang: " + spesialisasiBidang;
}

// Dokter (override)
@Override
public String tampilkanInfo() {
    return super.tampilkanInfo() + " | Peran: Dokter | No. STR: " + nomorSTR;
}
```

Karena `Analis` dan `Dokter` disimpan bersama dalam satu `ArrayList<Petugas>`, saat program melakukan perulangan dan memanggil `p.tampilkanInfo()`, Java akan otomatis menjalankan versi method sesuai objek aslinya (Analis atau Dokter) walaupun tipe referensinya `Petugas` — inilah *dynamic method dispatch*, inti dari polymorphism lewat overriding.

### c. Polymorphism — Overloading

Selain overriding, program juga menerapkan **overloading** (nama method sama, parameter berbeda):

```java
public String tampilkanInfo() {
    return "ID: " + id + " | Nama: " + nama;
}

public String tampilkanInfo(boolean detail) {
    if (!detail) {
        return tampilkanInfo();
    }
    return "ID: " + id + " | Nama: " + nama
            + " | Umur: " + umur + " | Jenis Kelamin: " + jenisKelamin;
}
```

Contoh lain ada di `LaboratoriumController`, method `bacaInt()` di-*overload* menjadi dua versi — tanpa batas rentang (dipakai untuk pilihan menu) dan dengan batas rentang minimal-maksimal (dipakai misalnya oleh `bacaUmur()`):

```java
private int bacaInt(Scanner scanner) {
    return bacaInt(scanner, Integer.MIN_VALUE, Integer.MAX_VALUE);
}

private int bacaInt(Scanner scanner, int min, int max) {
    // ... validasi angka dalam rentang min-max
}
```

### d. Condition (if-else)

Percabangan `if-else` dipakai secara luas untuk validasi input, misalnya pada setter `Petugas`:

```java
public void setNama(String nama) {
    if (nama != null && !nama.trim().isEmpty()) {
        this.nama = nama;
    } else {
        System.out.println(">> ERROR: Nama tidak boleh kosong!");
    }
}

public void setUmur(int umur) {
    if (umur > 0) {
        this.umur = umur;
    } else {
        System.out.println(">> ERROR: Umur harus lebih dari 0!");
    }
}
```

`if-else` juga dipakai untuk mengecek hasil pencarian data (null-check) sebelum data ditampilkan atau diproses lebih lanjut, misalnya saat mencari pasien/pemeriksaan/petugas berdasarkan ID.

### e. Looping

- **`while`** — dipakai supaya menu utama dan setiap sub-menu terus berjalan berulang sampai pengguna memilih opsi keluar/kembali.
- **`for`** — dipakai untuk menelusuri isi `ArrayList` saat menampilkan seluruh data (misalnya `tampilkanSemuaPasien()`, `tampilkanSemuaPetugas()`, `tampilkanSemuaPemeriksaan()`).

```java
for (Petugas p : daftarPetugas) {
    view.tampilkanBaris(p.tampilkanInfo(true));
}
```


### Validasi Biaya

Biaya pemeriksaan tidak boleh negatif:

```java
if (biaya >= 0) {
    this.biaya = biaya;
}
```

### Validasi Input Teks

Program juga memiliki method untuk memastikan input teks tidak kosong sehingga pengguna tidak dapat memasukkan data kosong pada bagian yang diperlukan.

Validasi ini membantu mengurangi kesalahan ketika pengguna memasukkan data ke dalam program.

---

## 6. Dummy Data

Program menyediakan dummy data yang dimasukkan ketika program pertama kali dijalankan.

Dummy data digunakan agar data sudah tersedia ketika pengguna memilih menu lihat tanpa harus memasukkan data terlebih dahulu.

Data awal yang disediakan mencakup:

- Data pasien
- Data analis
- Data dokter
- Data pemeriksaan
- Data hasil pemeriksaan

Contoh data petugas disimpan dalam:

```java
ArrayList<Petugas>
```

Sedangkan data pasien, pemeriksaan, dan hasil pemeriksaan masing-masing disimpan dalam `ArrayList` sesuai dengan class-nya.

---

## 7. Konsep PBO yang Diterapkan

Program ini menerapkan beberapa konsep Pemrograman Berorientasi Objek, yaitu:

| Konsep | Penerapan |
|---|---|
| Class & Object | Digunakan pada `Pasien`, `Petugas`, `Analis`, `Dokter`, `Pemeriksaan`, dan `HasilPemeriksaan` |
| Constructor | Digunakan untuk membuat object dan mengisi data awal |
| Access Modifier | Atribut menggunakan `private` dan method menggunakan `public` |
| Encapsulation | Data diakses melalui getter dan setter |
| Inheritance | `Analis` dan `Dokter` mewarisi `Petugas` |
| Overriding | `tampilkanInfo()` dioverride pada `Analis` dan `Dokter` |
| Polymorphism | `Analis` dan `Dokter` disimpan dalam `ArrayList<Petugas>` |
| ArrayList | Digunakan untuk menyimpan data selama program berjalan |
| Validasi | Digunakan untuk memeriksa input pengguna |
| MVC | Program dibagi menjadi bagian Main, Controller, Model, dan View |

---

## 8. Hasil Output Program 

Berikut tampilan program saat dijalankan, berurutan dari menu utama sampai keluar.

### Menu Utama

Tampilan pertama saat program dijalankan.

<img height="200" alt="image" src="https://github.com/user-attachments/assets/e08d72bc-32c8-4a46-bfd7-ce88df167df1" />


### Menu 1 - Pendaftaran Pemeriksaan

Pendaftaran dengan **pasien baru**: pengguna mengisi data pasien, lalu memilih pemeriksaan dan petugas.

<img height="500" alt="image" src="https://github.com/user-attachments/assets/d0c6835f-c0f3-4ae4-9a47-479a10919cc6" />

Penjelasan alur pada gambar di atas:

1. Pengguna memilih menu **1. Pendaftaran Pemeriksaan**, lalu memilih **1. Pasien Baru**.
2. Program meminta data pasien: nama, umur, jenis kelamin, dan keluhan. Setiap input divalidasi, misalnya jenis kelamin hanya menerima `Laki-laki` atau `Perempuan` (huruf besar/kecil tidak dibedakan).
3. Setelah data valid, pasien disimpan dan mendapat **ID otomatis** (`P2`, karena `P1` sudah dipakai dummy data).
4. Program menampilkan daftar pemeriksaan beserta biayanya, lalu pengguna memasukkan ID pemeriksaan (`PM1`).
5. Program menampilkan daftar petugas, lalu pengguna memasukkan ID petugas (`PT2`). Tampilan daftar ini memperlihatkan hasil **overriding**: `Analis` menampilkan spesialisasi, sedangkan `Dokter` menampilkan nomor STR.

Tampilan **konfirmasi pendaftaran** setelah semua data dipilih.

<img height="215" alt="image" src="https://github.com/user-attachments/assets/6221e7de-250e-428c-8675-93c7998378e2" />


Pendaftaran dengan **pasien yang sudah terdaftar** dan tampilan konfirmasi pendaftaran.

<img height="600" alt="image" src="https://github.com/user-attachments/assets/f9554086-2e57-4a52-80f7-2771cd47b236" />


Penjelasan alur pada gambar di atas:

1. Pengguna memilih **2. Pasien Sudah Terdaftar**, lalu program menampilkan semua pasien (`P1` dan `P2`). Pasien `P2` adalah pasien yang sebelumnya didaftarkan sebagai pasien baru, sehingga terlihat bahwa data tersimpan di `ArrayList`.
2. Pengguna memasukkan ID pasien (`p1`). Pencarian tidak membedakan huruf besar dan kecil (`equalsIgnoreCase`), sehingga `p1` tetap ditemukan sebagai `P1`.
3. Pengguna memilih pemeriksaan (`PM1`) dan petugas (`PT1`). Daftar petugas menampilkan hasil **overriding**: `Analis` menampilkan spesialisasi, sedangkan `Dokter` menampilkan nomor STR.
4. Program menampilkan **konfirmasi pendaftaran** berisi ID dan nama pasien, jenis pemeriksaan, biaya, petugas, serta status `Terdaftar`.
5. Data pendaftaran disimpan pada `pasienTerdaftar`, `pemeriksaanTerdaftar`, dan `petugasTerdaftar` untuk dipakai pada menu **Input Hasil Pemeriksaan**.



### Menu 2 - Kelola Pasien

**Menu 2**

<img height="205" alt="image" src="https://github.com/user-attachments/assets/8bf91a83-2c9f-47aa-8841-f9337e5d3e0c" />

**Tambah pasien.**

<img height="200" alt="image" src="https://github.com/user-attachments/assets/9456b43d-2908-4bd4-9cf2-805b9c8e4f2a" />


**Lihat semua pasien.**

<img height="200" alt="image" src="https://github.com/user-attachments/assets/e69c3b35-7371-4439-b58e-ac83c7d6180a" />



**Cari pasien berdasarkan ID.**

<img height="200" alt="image" src="https://github.com/user-attachments/assets/a63b2cdb-bf74-4d28-b62b-39b92a2b11d3" />


**Hapus pasien.**

<img height="300" alt="image" src="https://github.com/user-attachments/assets/8b07226f-a16f-4626-b5b1-056b92ec2431" />


### Menu 3 - Kelola Petugas

**Menu Petugas**

<img height="200" alt="image" src="https://github.com/user-attachments/assets/f894cbeb-39ae-4cf6-965c-41068a27e47f" />


**Tambah analis.**

<img height="200" alt="image" src="https://github.com/user-attachments/assets/6e467abc-22a5-450a-a7ad-5cd4de95b1d5" />


**Tambah dokter.**

<img height="200" alt="image" src="https://github.com/user-attachments/assets/9ef3e20d-ba4c-493a-9c07-bc76a0bc945b" />


**Lihat semua petugas.** Pada tampilan ini terlihat hasil **overriding**: `Analis` menampilkan spesialisasi, sedangkan `Dokter` menampilkan nomor STR.

<img height="200" alt="image" src="https://github.com/user-attachments/assets/2541d238-741b-4295-adb2-553c22211133" />


### Menu 4 - Kelola Pemeriksaan

**Menu Pemeriksaan**

<img height="300" alt="image" src="https://github.com/user-attachments/assets/1d988ff6-93f9-4cdd-b66e-975602c74b5f" />


**Tambah pemeriksaan.**

<img height="300" alt="image" src="https://github.com/user-attachments/assets/a96b2a2e-fc24-435e-bc07-5c3fa097019d" />


**Lihat semua pemeriksaan.**

<img height="300" alt="image" src="https://github.com/user-attachments/assets/4df5db88-4ea8-4e59-b67d-69aafd375d37" />


**Cari pemeriksaan.**

<img height="300" alt="image" src="https://github.com/user-attachments/assets/eecdf32a-d036-4861-ac4a-fc36a4e3faff" />


**Ubah pemeriksaan.**

<img height="400" alt="image" src="https://github.com/user-attachments/assets/62de538f-b1dd-4389-8f37-c4f3fa8423d4" />

**Hapus pemeriksaan.**

<img height="400" alt="image" src="https://github.com/user-attachments/assets/2a21e46a-a9bf-4de2-a2f9-ee1684ea5011" />

### Menu 5 - Kelola Hasil Pemeriksaan

**Menu Hasil Pemerikasaan**

<img height="200" alt="image" src="https://github.com/user-attachments/assets/71dece68-9187-43c3-b493-39cf59267399" />

**Input hasil pemeriksaan.**

<img height="300" alt="image" src="https://github.com/user-attachments/assets/c1702f36-0e91-4faf-899a-e27454e18335" />


**Lihat semua hasil.**

<img height="400" alt="image" src="https://github.com/user-attachments/assets/2ec5fbac-5815-4fa6-a40a-1c1406d6c424" />


**Lihat riwayat hasil per pasien.**

<img height="400" alt="image" src="https://github.com/user-attachments/assets/cae10999-f5d9-4f28-91bd-71c9ccc1051f" />


### Validasi Input

Contoh ketika pengguna memasukkan input yang salah (misalnya huruf pada kolom umur, atau jenis kelamin yang tidak valid). Program meminta input diulang dan tidak berhenti.

**contoh pada umur:**

<img height="200" alt="image" src="https://github.com/user-attachments/assets/2b3287a8-a402-4cb8-81f9-6f301150e1fa" />

**contoh pada jenis kelamin:**

<img height="200" alt="image" src="https://github.com/user-attachments/assets/f0d20258-6276-439c-baf2-865dc61df61d" />

**contoh pada nama:**

<img height="200" alt="image" src="https://github.com/user-attachments/assets/52eea062-1202-49e4-af27-3ba4c36a9144" />



### Menu 6 - Keluar

**Program menampilkan pesan penutup dan berhenti.**

<img height="200" alt="image" src="https://github.com/user-attachments/assets/4cd9ff28-b650-4b05-82ce-36129abfd574" />


---

## 9. Kesimpulan

Program Sistem Manajemen Laboratorium Kesehatan ini dibuat untuk memenuhi tugas UTS Pemrograman Berorientasi Objek, dengan menerapkan inheritance, polymorphism (overriding dan overloading), percabangan if-else, dan perulangan secara nyata.

Program tidak hanya mengelola data pemeriksaan, tetapi juga menghubungkan data pasien, petugas, pemeriksaan, dan hasil pemeriksaan dalam satu alur kerja. Penerapan encapsulation, inheritance, overriding, overloading, validasi input, ArrayList, serta struktur MVC membuat program menjadi lebih terstruktur dan sesuai dengan konsep PBO yang dipelajari.
