# Anggota kelompok:
- Muhammad Satria Nurulloh
- Aryan Firmansyah

# Analisis Computational Thinking — Kasir dengan Diskon

## Deskripsi

Program kasir ini dirancang untuk menghitung diskon dan total pembayaran pelanggan berdasarkan tiga *business rule* (aturan bisnis):

| Kode | Business Rule |
|---|---|
| BR-01 | Belanja minimal Rp100.000 mendapat diskon 10%. |
| BR-02 | Member mendapat tambahan diskon 5%, hanya jika BR-01 terpenuhi. |
| BR-03 | Total potongan maksimal Rp25.000. |

Analisis dilakukan menggunakan empat konsep *Computational Thinking*: **Decomposition**, **Pattern Recognition**, **Abstraction**, dan **Algorithm**.

## 1. Decomposition (Memecah Masalah)

Masalah utama dipecah menjadi tiga fungsi sesuai petunjuk soal.

### 1.1 `hitungPersenDiskon()`

Menentukan persentase diskon berdasarkan total belanja dan status member.

- Belanja di bawah Rp100.000: tidak mendapat diskon.
- Belanja minimal Rp100.000 dan bukan member: diskon 10%.
- Belanja minimal Rp100.000 dan member: diskon 15% (10% + tambahan 5%).

### 1.2 `hitungPotongan`

Menghitung nominal potongan dari total belanja dan persentase diskon. Setelah itu, potongan dibatasi agar tidak melebihi Rp25.000.

Contoh: 15% dari Rp300.000 adalah Rp45.000. Karena batas maksimal potongan Rp25.000, potongan yang digunakan adalah Rp25.000.

### 1.3 `hitungTotalBayar`

Menghitung total yang harus dibayar setelah potongan diterapkan.

**Rumus:**

```text
totalBayar = totalBelanja - potongan
```

## 2. Pattern Recognition

Pola yang ditemukan dari business rule:

| Kondisi | Persentase Diskon |
|---|---:|
| Belanja kurang dari Rp100.000 | 0% |
| Belanja minimal Rp100.000, bukan member | 10% |
| Belanja minimal Rp100.000, member | 15% |

catatan:

1. Status member hanya berpengaruh jika total belanja minimal Rp100.000.
2. Nominal potongan tidak boleh melebihi Rp25.000, berapa pun hasil perhitungan diskon awalnya.
3. Total pembayaran selalu dihitung dengan mengurangi total belanja menggunakan potongan akhir.

## 3. Abstraction

Program hanya membutuhkan data yang relevan untuk menghitung pembayaran.

| Variabel | Tipe Data Dart | Kegunaan |
|---|---|---|
| `totalBelanja` | `int` | Menyimpan jumlah belanja pelanggan dalam rupiah. |
| `isMember` | `bool` | Menunjukkan apakah pelanggan merupakan member. |
| `persenDiskon` | `double` atau `int` | Menyimpan persentase diskon yang diperoleh. |
| `potongan` | `int` atau `double` | Menyimpan nominal potongan akhir. |
| `totalBayar` | `int` atau `double` | Menyimpan jumlah akhir yang harus dibayar. |

Untuk skenario pada soal, nominal rupiah berupa bilangan bulat sehingga `int` dapat digunakan untuk nilai uang. Data seperti nama pelanggan, daftar barang, dan metode pembayaran tidak diperlukan karena tidak termasuk aturan yang diminta.

## 4. Algorithm

### 4.1 Menentukan persentase diskon

```text
Jika totalBelanja >= 100000:
    Jika isMember == true:
        persenDiskon = 15
    Jika tidak:
        persenDiskon = 10
Jika tidak:
    persenDiskon = 0
```

Pemeriksaan status member dilakukan setelah syarat minimal belanja terpenuhi. Dengan demikian, member yang belanjanya kurang dari Rp100.000 tetap tidak memperoleh diskon.

### 4.2 Menghitung dan membatasi potongan

```text
potonganAwal = totalBelanja * persenDiskon / 100

Jika potonganAwal > 25000:
    potongan = 25000
Jika tidak:
    potongan = potonganAwal
```

### 4.3 Menghitung total pembayaran

```text
totalBayar = totalBelanja - potongan
```

### 4.4 Alur program

1. Menyiapkan total belanja dan status member.
2. Menentukan persentase diskon.
3. Menghitung nominal potongan awal.
4. Membatasi potongan maksimal Rp25.000.
5. Menghitung total pembayaran.
6. Menampilkan total pembayaran.

## 5. Pengujian Skenario

| Skenario | Total Belanja | Member | Perhitungan Potongan | Potongan Akhir | Expected Total Bayar |
|---|---:|---|---|---:|---:|
| 1 | Rp80.000 | Tidak | Rp80.000 × 0% = Rp0 | Rp0 | Rp80.000 |
| 2 | Rp150.000 | Tidak | Rp150.000 × 10% = Rp15.000 | Rp15.000 | Rp135.000 |
| 3 | Rp150.000 | Ya | Rp150.000 × 15% = Rp22.500 | Rp22.500 | Rp127.500 |
| 4 | Rp300.000 | Ya | Rp300.000 × 15% = Rp45.000, lalu dibatasi | Rp25.000 | Rp275.000 |

**Hasil pengujian:** keempat skenario menghasilkan total pembayaran yang sesuai dengan nilai *expected total bayar* pada soal.

## 6. Konsep Control Flow yang Digunakan

Control flow mengatur jalannya program berdasarkan kondisi dan urutan instruksi.

- **`if-else` bertingkat:** menentukan diskon berdasarkan total belanja dan status member.
- **Percabangan batas potongan:** memeriksa apakah potongan awal melebihi Rp25.000.
- **Urutan proses:** total pembayaran dihitung setelah potongan akhir diketahui.
perhitungan secara berurutan. Rancangan ini dapat digunakan sebagai acuan untuk mengimplementasikan program Dart dan menguji hasilnya menggunakan empat skenario yang tersedia.
