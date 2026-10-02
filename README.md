# dart-week-2-cashier
# Anggota kelompok: M. Satria Nurulloh, Aryan Firmansyah

# 1. Atruan Logika
BR-01	= Belanja minimal Rp100.000 mendapat diskon 10%.
BR-02	= Member mendapat tambahan diskon 5% (hanya jika BR-01 terpenuhi).
BR-03	= Total potongan maksimal Rp25.000.

# 2. Input, Output, Abstraction
Input	= totalBelanja (double), membership (bool)
Output	= totalBayar (double)
Abstraction	= hitungPersenDiskon(totalBelanja, membership), hitungPotongan(diskon, totalBelanja), hitungTotalBayar(totalBelanja, membership)
