Dokumentasi Proyek Database Perbankan

Deskripsi
Proyek ini berisi tiga tabel utama yang digunakan untuk menyimpan data terkait nasabah, kartu, dan transaksi. Struktur tabel ini dapat digunakan untuk berbagai analisis keuangan, terutama dalam melihat perilaku transaksi, penggunaan kartu, dan profil nasabah.

Struktur Tabel
1. cards
   Menyimpan informasi detail kartu nasabah.
   Kolom:
   - id, client_id, card_brand, card_type, card_number, expires, cvv, chip, num_cards_issued, credit_limit, acct_open_date, year_pin_last_changed, card_on_dark_web

2. user_data
   Menyimpan informasi pribadi nasabah.
   Kolom:
   - id, current_age, retirement_age, birth_year, birth_month, gender, address, latitude, longitude, per_capita_income, yearly_income, total_debt, credit_score, num_credit_cards

3. transaksi
   Menyimpan informasi transaksi.
   Kolom:
   - id_transaksi, date, client_id, card_id, amount, use_chip, merchant_id, merchant_city, merchant_state, zip, mcc, errors, amount_clean

Contoh Query Analisis : 

1. Total jumlah transaksi per nasabah
SELECT 
    u.id AS user_id,
    COUNT(t.id_transaksi) AS jumlah_transaksi,
    SUM(t.amount_clean) AS total_pengeluaran
FROM transaksi t
JOIN user_data u ON t.client_id = u.id
GROUP BY u.id;

2. Rata-rata pengeluaran per brand kartu
SELECT 
    c.card_brand,
    AVG(t.amount_clean) AS rata_pengeluaran
FROM transaksi t
JOIN cards c ON t.card_id = c.id
GROUP BY c.card_brand;

3. Distribusi transaksi berdasarkan kota merchant
SELECT 
    merchant_city,
    COUNT(id_transaksi) AS jumlah_transaksi,
    SUM(amount_clean) AS total_pengeluaran
FROM transaksi
GROUP BY merchant_city
ORDER BY total_pengeluaran DESC;

4. Analisis pendapatan tahunan dan total utang nasabah
SELECT 
    id AS user_id,
    yearly_income,
    total_debt,
    credit_score
FROM user_data;

5. Tren transaksi per bulan
SELECT 
    DATE_FORMAT(date, '%Y-%m') AS bulan,
    COUNT(id_transaksi) AS jumlah_transaksi,
    SUM(amount_clean) AS total_pengeluaran
FROM transaksi
GROUP BY DATE_FORMAT(date, '%Y-%m')
ORDER BY bulan;

**Catatan
Masih banyak analisis lain yang bisa dieksplorasi tergantung kebutuhan, misalnya:
- Analisis gender terhadap jumlah transaksi.
- Perbandingan pengeluaran nasabah dengan skor kredit.
- Deteksi anomali transaksi berdasarkan error code.

Semua query di atas dapat langsung dieksekusi, lalu hasilnya dihubungkan ke Looker Studio untuk divisualisasikan sesuai kebutuhan.
