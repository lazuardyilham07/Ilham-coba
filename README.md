README – Deskripsi Dataset
Dataset ini terdiri dari 3 tabel utama yang berhubungan dengan data nasabah, kartu kredit, dan aktivitas transaksi. Data ini bisa digunakan untuk analisis perilaku pengguna, deteksi fraud, segmentasi pelanggan, serta evaluasi risiko kredit.
1. user_data

Menyimpan informasi dasar dan finansial tiap pengguna.

id – Primary key (ID user)

current_age – Usia saat ini

retirement_age – Usia pensiun yang diharapkan

birth_year, birth_month – Data kelahiran

gender – Jenis kelamin

address, latitude, longitude – Lokasi

per_capita_income – Pendapatan per kapita

yearly_income – Pendapatan tahunan

total_debt – Total utang

credit_score – Skor kredit

num_credit_cards – Jumlah kartu yang dimiliki

2. cards

Menyimpan detail kartu kredit yang dimiliki user.

id – Primary key (ID kartu)

client_id – Foreign key → user_data.id

card_brand – Merek kartu (Visa, MasterCard, dsb.)

card_type – Jenis kartu (Debit, Credit, dsb.)

card_number – Nomor kartu

expires – Tanggal kedaluwarsa

cvv – CVV code

chip – Indikasi penggunaan chip

num_cards_issued – Jumlah kartu diterbitkan

credit_limit – Batas kredit

acct_open_date – Tanggal kartu dibuka

year_pin_last_changed – Tahun PIN terakhir diganti

card_on_dark_web – Indikasi kartu pernah ditemukan di dark web

3. transaksi

Menyimpan riwayat transaksi pengguna.

id_transaksi – Primary key (ID transaksi)

date – Tanggal transaksi

client_id – Foreign key → user_data.id

card_id – Foreign key → cards.id

amount – Nilai transaksi

use_chip – Indikasi apakah chip digunakan

merchant_id – ID merchant

merchant_city, merchant_state, zip – Lokasi merchant

mcc – Merchant Category Code

errors – Error pada transaksi (jika ada)

amount_clean – Nilai transaksi bersih (setelah bersih dari error/anomali)

📊 Contoh Analisis

Beberapa analisis yang bisa dilakukan:

Profil Nasabah – Distribusi usia, pendapatan, skor kredit, dan jumlah kartu.

Analisis Kartu – Brand/type kartu populer, kartu yang muncul di dark web.

Analisis Transaksi – Total transaksi per kota, rata-rata nilai transaksi, error/anomali.

Gabungan – Hubungan skor kredit dengan aktivitas transaksi, kartu di dark web tapi tetap digunakan.

⚡ Potensi Ekstensi Analisis

Selain query dasar di atas, masih banyak analisis lain yang bisa dieksplor sesuai kebutuhan, seperti:

Segmentasi nasabah berdasarkan skor kredit dan pendapatan.

Deteksi fraud dengan melihat pola error transaksi dan kartu yang muncul di dark web.

Analisis geografis transaksi berdasarkan lokasi merchant dan user.

Time series tren transaksi dari waktu ke waktu.

Clustering perilaku belanja untuk rekomendasi produk.

🚀 Catatan

Dataset ini dapat digunakan untuk analisis eksploratif maupun pembangunan model machine learning (contoh: fraud detection, credit scoring).

Hasil analisis sangat fleksibel dan bisa disesuaikan dengan tujuan bisnis atau penelitian.
