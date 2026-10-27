# Update 13 (di atas Update 12)

## SQL — Supabase SQL Editor, berurutan 13, 14, 14b, 14c, 15; satu file satu kali Run (aman diulang). Dipecah karena SQL Editor memotong skrip ±20.000 karakter.
| # | File | Isi |
|---|------|-----|
| 1 | `sql/koin-usdt-13-preorder-per10k.sql` | Harga Pre Order = per **10.000 barang** |
| 2 | `sql/koin-usdt-14-modal.sql` | Tabel Modal + daftar barang (menu **Modal**) |
| 2b | `sql/koin-usdt-14b-modal-bsl.sql` | Modal -> BSL Profit + Catat Penjualan Barang |
| 2c | `sql/koin-usdt-14c-modal-cashflow.sql` | Modal & profit di CashFlow |
| 3 | `sql/koin-usdt-15-bulk-order.sql` | **Bulk Order** (BEM+SEM+LEM 1 pesanan) + harga tier |

Jangan menjalankan ulang `bot-order.sql` / `bsl-profit.sql` / `bot-order-kirim-arsip.sql` setelah #2 dan #3 (akan menimpa fungsi modal dengan versi lama).

## 1. Pre Order per 10.000 barang
- Admin (Supply & Stock → Pre Order): angka harga = koin untuk 10.000 barang. Pelanggan membayar `barang × harga ÷ 10.000` (dibulatkan ke atas per batch).
- Harga lama (per barang) dan Custom Price / Harga Pelanggan Pre Order otomatis dikali 10.000 SEKALI saja, jadi nilai riil tetap sama. Riwayat pesanan lama tetap benar.
- Tampilan pelanggan (5 bahasa), daftar harga item, dan menu Order → Pre Order ikut menampilkan "/ 10.000 barang".

## 2. Menu Modal (DIRECTORY → Modal)
- Satu tempat untuk semua modal: Farm, Hav Token, Product (tiap tier 100/500/1000), Koin/Voucher/kategori lain, Pre Order, ditambah modal BSL (BEM/SEM/LEM harian dan Bot). Barang baru di etalase otomatis muncul.
- Modal yang dulu ada di BSL Profit dipindahkan otomatis ke menu Modal. Panel modal di BSL Profit kini hanya ringkasan + tombol ke menu Modal.
- BSL Profit → **Catat Penjualan Barang**: pilih barang + jumlah → omset (harga etalase, bisa diubah), modal (dari menu Modal), profit otomatis.
- CashFlow: form punya **Pilih Barang (etalase)**; harga jual & modal terisi otomatis, kolom Modal/Profit ada di tabel, batch, dan ringkasan.
- Modal disimpan sebagai snapshot saat transaksi; mengubah modal tidak mengubah transaksi lama.
- Jumlah barang berupa bilangan bulat. Untuk Pre Order, 1 jumlah = 10.000 barang.

## 3. Bulk Order (BEM + SEM + LEM dalam 1 pesanan)
- **Pelanggan** (dashboard → Bot Order / Order): tombol **Pesan Bulk Order**. Isi tagar BEM, SEM, LEM (boleh sebagian dikosongkan), maks. 100 tagar total, plus catatan. Total harga tampil langsung, tabel tier bisa dibuka. Bayar dengan koin seperti Bot Order; ditolak / dihapus saat menunggu → koin kembali.
- **Admin → Price → Harga Bulk Order**: harga per tagar untuk BEM/SEM/LEM pada 4 tier jumlah total tagar: 1–5, 6–10, 11–50, 51–100 (12 angka) + saklar tersedia. Paket yang dipakai pelanggan wajib berharga > 0.
- **Admin → Order**: tab **🤖 Bot Order** dan **🧺 Bulk Order** terpisah (daftar, badge, filter, dan "arsipkan semua terkirim" masing-masing sendiri, jadi tidak tertukar). Pesanan bulk tampil dengan jumlah per paket + tier. Klik jumlah tagar untuk melihat daftar tagar per paket (BEM/SEM/LEM, tombol salin per paket/semua) dan catatan pelanggan. Alur Setujui → Dikirim → Arsip sama dengan Bot Order.
- Setujui otomatis tercatat di BSL Profit (kategori "BULK Bot"): omset = total, modal = jumlah tagar tiap paket × modal Bot paket itu (menu Modal).
- Harga Bulk tidak terpengaruh Custom Price / Harga Pelanggan.

## 4. Menu Price bisa di-minimize
Klik judul panel mana pun di Price untuk minimize / buka; ada tombol Minimize semua / Buka semua. Status diingat di browser.

- Sisi pelanggan: di tab Bot Order ada filter Semua / Bot / Bulk. Di form Bulk Order, pelanggan bebas memilih paket BEM, SEM, dan/atau LEM (isi tagar hanya pada paket yang diinginkan).
