Cetak Biru Sistem & Spesifikasi Teknis
Dashboard KPI Sales & Marketing (Hierarki HQM)
Konsep Aplikasi Web Berbasis GitHub Pages untuk Monitoring Kinerja Field Force, Supervisor, Area Manager, dan Area Sales Manager

1. Tujuan & Arsitektur Aplikasi (GitHub Deployment)
Aplikasi dirancang sebagai Single-Page Application (SPA) berbasis web yang responsif untuk perangkat seluler maupun desktop, sehingga dapat langsung dipublikasikan melalui GitHub Pages menggunakan tumpukan teknologi HTML5, Tailwind CSS, JavaScript, dan pustaka grafik Chart.js.

kpi-sales-hqm/
├── index.html          # Struktur antarmuka lengkap (Login, Dashboard, Input, SWOT, Pareto, Admin)
├── app.js              # Logika RBAC, kalkulasi bobot KPI, CRUD data, & rendering grafik
└── README.md           # Dokumentasi struktur organisasi, rumus KPI, & panduan deployment
Ketentuan Teknis Antarmuka & Sinkronisasi Data
Navigasi Bebas Muat Ulang (Anti-Reload): Seluruh formulir masukan menggunakan kontainer blok standar dan tombol aksi langsung tanpa pengiriman formulir tradisional agar tidak memicu muat ulang halaman maupun kesalahan jalur berkas pada peramban seluler.
Kontrol Visibilitas Sandi: Tombol ikon mata pada halaman masuk mengubah tipe masukan sandi secara langsung dengan area sentuh minimal 44 × 44 piksel agar nyaman digunakan pada layar sentuh ponsel.
Penyimpanan & Sinkronisasi Lintas Perangkat: Penyimpanan lokal peramban (localStorage) dapat dihubungkan ke Firebase Firestore atau Google Sheets API (Apps Script) agar pembaruan data lapangan terbaca secara waktu nyata oleh seluruh jajaran pimpinan.
2. Struktur Hierarki Organisasi & Hak Akses (RBAC)
Sistem menerapkan pembatasan akses berjenjang (Role-Based Access Control) dalam 5 tingkatan jabatan untuk menjamin kerahasiaan data antar tim:

Spesifikasi Sistem Dashboard KPI Sales & Marketing (Hierarki HQM)
Page 1 of 6
Lvl	Jabatan	Nama Personel	Username / Kode	Sandi	Hak Akses & Isolasi Dashboard
0	Admin	Admin Sistem	adm_sys	Adm#2026	Akses penuh: kelola akun (tambah, ubah, ganti, hapus semua level), atur target per FF, koreksi manual beserta Audit Trail, serta sakelar Geotagging.
1	Area Sales Manager (ASM)	Adi Kurniawan	asm_adi	Asm#2026	Melihat agregat seluruh tim nasional, seluruh AM/SPV/FF, mengisi keterangan evaluasi SWOT level ASM, serta mengontrol sakelar Geotagging.
2	Area Manager (AM)	Vacant (dapat diubah Admin)	am_vacant	Am#2026	Melihat agregat seluruh SPV dan FF di bawah koordinasinya serta mengisi keterangan evaluasi SWOT level AM.
3	Supervisor (SPV)	Abdullah	spv_abdullah	Spv#101	Terkunci pada tim sendiri: Hanya melihat agregat tim dan FF bawahannya (HQM003, HQM004, HQM007). Mengisi Joint Visit & keterangan SWOT level SPV.
3	Supervisor (SPV)	Yunianto	spv_yunianto	Spv#102	Terkunci pada tim sendiri: Hanya melihat agregat tim dan FF bawahannya (HQM002, HQM005). Tidak dapat melihat dashboard SPV lain.
3	Supervisor (SPV)	Ari Partanto	spv_ari	Spv#103	Terkunci pada tim sendiri: Hanya melihat agregat tim dan FF bawahannya (HQM006, HQM008). Tidak dapat melihat dashboard SPV lain.
Spesifikasi Sistem Dashboard KPI Sales & Marketing (Hierarki HQM)
Page 2 of 6
Lvl	Jabatan	Nama Personel	Username / Kode	Sandi	Hak Akses & Isolasi Dashboard
4	Field Force (FF)	Dedi Heriyanto	hqm003 (HQM003)	Sales#003	Terkunci pada diri sendiri: Hanya melihat dashboard pribadi, input aktivitas harian, dan mengisi SWOT pribadi (Tim SPV Abdullah).
4	Field Force (FF)	Abdul Hakim	hqm004 (HQM004)	Sales#004	Terkunci pada diri sendiri: Hanya melihat dashboard pribadi & SWOT pribadi (Tim SPV Abdullah).
4	Field Force (FF)	Sandi	hqm007 (HQM007)	Sales#007	Terkunci pada diri sendiri: Hanya melihat dashboard pribadi & SWOT pribadi (Tim SPV Abdullah).
4	Field Force (FF)	Egi Priagunawan	hqm002 (HQM002)	Sales#002	Terkunci pada diri sendiri: Hanya melihat dashboard pribadi & SWOT pribadi (Tim SPV Yunianto).
4	Field Force (FF)	Suyadi	hqm005 (HQM005)	Sales#005	Terkunci pada diri sendiri: Hanya melihat dashboard pribadi & SWOT pribadi (Tim SPV Yunianto).
4	Field Force (FF)	Dewi	hqm006 (HQM006)	Sales#006	Terkunci pada diri sendiri: Hanya melihat dashboard pribadi & SWOT pribadi (Tim SPV Ari Partanto).
4	Field Force (FF)	Andhi	hqm008 (HQM008)	Sales#008	Terkunci pada diri sendiri: Hanya melihat dashboard pribadi & SWOT pribadi (Tim SPV Ari Partanto).
Spesifikasi Sistem Dashboard KPI Sales & Marketing (Hierarki HQM)
Page 3 of 6
3. Struktur KPI & Pembobotan (Total = 100%)
Parameter penilaian berfokus penuh pada efektivitas komersial dan pemerataan kinerja tim, dengan batas atas penilaian (capping) sebesar 120% pada setiap parameter agar satu pencapaian ekstrem tidak menutupi parameter lain yang belum terpenuhi.

Level Jabatan	Parameter KPI	Bobot	Standar Pengukuran
Field Force (FF)
Eksekusi Harian & Akuisisi	1. Sales Achievement	40%	Akumulasi omzet dari 3 kategori perusahaan (RSN, NN, Vitashopindo) dibanding target bulanan.
2. Kunjungan (Visit)	25%	Realisasi jumlah kunjungan lapangan harian dibanding target call plan bulanan.
3. New Open Outlet (NOO)	15%	Jumlah pelanggan atau outlet baru yang berhasil diakuisisi dan bertransaksi.
4. Sales Conversion Rate	10%	Persentase kunjungan lapangan yang menghasilkan pesanan transaksi (Effective Call / Closing).
5. Entertainment & Relasi	10%	Efektivitas pemanfaatan plafon biaya entertaint terhadap transaksi penutupan (closing).
Supervisor (SPV)
Supervisi & Pemerataan Tim	1. Team Sales Achievement	40%	Akumulasi realisasi omzet seluruh anggota Field Force di bawah koordinasinya dibanding target tim.
2. Kunjungan (Joint & Key Account)	20%	Pendampingan lapangan (coaching) bersama Field Force serta kunjungan strategis Key Account.
3. Team Active Outlet & NOO	15%	Tingkat keaktifan database outlet bertransaksi dan pencapaian target NOO tim.
4. Entertainment Budget Control	15%	Pengendalian rasio pengeluaran biaya entertaint tim agar tetap berada di dalam batas plafon.
5. Team Target Achievement Rate	10%	Pemerataan kinerja tim (persentase anggota tim yang mencapai minimal 85% target individu).
Spesifikasi Sistem Dashboard KPI Sales & Marketing (Hierarki HQM)
Page 4 of 6
Level Jabatan	Parameter KPI	Bobot	Standar Pengukuran
Area Manager (AM) & ASM
Strategi & Profitabilitas	1. Total Revenue & Growth	35%	Pencapaian omzet gabungan area/nasional serta pertumbuhan penjualan periode berjalan.
2. Gross Profit Margin & Efisiensi	25%	Menjaga margin keuntungan dan rasio efisiensi biaya promosi serta entertaint.
3. Market Expansion & ROI	20%	Perluasan cakupan area/segmen pasar baru dan efektivitas program pemasaran.
4. Key Account Retention	10%	Tingkat retensi pelanggan utama (outlet VIP / Pareto Kelas A) dan kunjungan strategis.
5. Team Productivity & Turnover	10%	Persentase total personel tim yang mencapai skor KPI standar perusahaan (≥ 80%).
4. Modul Fitur Utama Aplikasi
Pembagian Omzet 3 Kategori Perusahaan (RSN, NN, dan Vitashopindo): Setiap pencatatan penjualan harian oleh Field Force maupun penetapan target bulanan oleh Admin dipecah secara eksplisit ke dalam entitas RSN, NN, dan Vitashopindo dengan akumulasi total otomatis ke atasan berjenjang.
Kontrol Sakelar Geotagging & Foto Bukti Kunjungan: Fitur ini bersifat toggle (Aktif / Nonaktif) yang hanya dapat diubah oleh Admin dan Area Sales Manager (ASM). Saat status Aktif, formulir kunjungan Field Force mewajibkan pengambilan titik koordinat GPS (HTML5 Geolocation API) dan unggah foto bukti lapangan; saat Nonaktif, kunjungan langsung diproses tanpa hambatan izin lokasi maupun foto.
Modul Analisis SWOT & Kolom Keterangan Berjenjang: Setiap Field Force mengisi 4 kuadran (Strengths, Weaknesses, Opportunities, Threats) yang dilengkapi contoh realistis berwarna abu-abu dengan gaya huruf miring sebagai panduan pengisian. Di bawah hasil SWOT tersedia 3 kolom keterangan evaluasi terpisah untuk SPV, AM, dan ASM yang dapat dibaca langsung oleh Field Force bersangkutan.
Modul Pareto Outlet (Analisis Kontribusi 80/20): Sistem memeringkat seluruh outlet berdasarkan kontribusi omzetnya ke dalam Kelas A (Top 80% kontribusi omzet), Kelas B (80%–95%), dan Kelas C (>95%), yang otomatis terbarui setiap kali Field Force mencatat transaksi pada nama outlet terkait.
Spesifikasi Sistem Dashboard KPI Sales & Marketing (Hierarki HQM)
Page 5 of 6
Panel Kendali Penuh Admin & Audit Trail: Admin dapat menambah, mengubah, mengganti nama/jabatan/atasan, maupun menghapus personel pada level FF, SPV, AM, dan ASM, menetapkan target spesifik per Field Force, serta melakukan penyesuaian angka manual yang seluruhnya tercatat otomatis di riwayat Audit Trail.
5. Spesifikasi Visualisasi Grafik Dashboard
Nama Grafik	Tipe Visual	Fungsi Analitik & Konfigurasi Data
1. Grafik Laba-Laba Bobot KPI	Radar / Spider Chart	Menampilkan keseimbangan skor pada 5 parameter bobot KPI milik pengguna/tim dibandingkan dengan poligon rata-rata tim pada level jabatan yang sama.
2. Grafik Sales vs Target Periodik	Clustered Bar Chart	Membandingkan realisasi omzet aktual terhadap target dengan tombol filter interaktif untuk periode Bulanan, Triwulan (Q1–Q4), dan Tahunan.
3. Grafik Sales Mingguan	Stacked Bar + Target Line	Memantau tren pencapaian omzet dari Minggu 1 hingga Minggu 4 yang terpecah per kategori (RSN, NN, Vitashopindo) terhadap garis target mingguan.
4. Perbandingan Kategori Perusahaan	Clustered Bar Chart	Membandingkan langsung target vs aktual serta porsi kontribusi persentase penjualan antara RSN, NN, dan Vitashopindo.
5. Grafik Kunjungan FF & SPV	Clustered Bar Chart	Membandingkan Target Visit, Aktual Visit, dan Effective Call (untuk Field Force) serta porsi Joint Visit dan Solo Visit (untuk Supervisor).
6. Grafik Kurva Pareto Outlet	Combo Bar + Line Chart	Menampilkan peringkat omzet setiap outlet (batang) beserta garis persentase kontribusi kumulatif hingga titik batas 80% Pareto Utama.
Catatan Skoring Penilaian Akhir: Skor KPI akhir dikategorikan menjadi 4 predikat kinerja: Exceed Expectation (>100%), Meet Expectation (85%–100%), Need Improvement (70%–84%), dan Underperformance (<70%).
Spesifikasi Sistem Dashboard KPI Sales & Marketing (Hierarki HQM)
Page 6 of 6 MR-Radiant-Group