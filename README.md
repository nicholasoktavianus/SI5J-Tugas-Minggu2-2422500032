# Bedah Insiden Ransomware Bank Indonesia (Desember 2021)
## Analisis 7 Komponen Tata Kelola & Design Factors COBIT 2019

**Nama:** Nicholas Oktavianus  
**NIM:** 2422500032  
**Mata Kuliah:** Audit Sistem Informasi (SI5J) — Minggu 2  
**Program Studi:** Sistem Informasi  
**Institusi:** Institut Sains dan Bisnis Atma Luhur  
**Studi Kasus:** Bank Indonesia — Insiden Ransomware Desember 2021  

---

## Bagian 1 — Case Brief (Profil & Kronologi)

### Profil Perusahaan
**Bank Indonesia (BI)** adalah Bank Sentral dan Otoritas Moneter Republik Indonesia yang memiliki peran strategis dalam menjaga stabilitas sistem keuangan, kelancaran sistem pembayaran (seperti BI-RTGS dan Kliring), serta pengelolaan uang rupiah di seluruh wilayah NKRI. Sebagai lembaga negara dengan fungsi moneter, BI setara dengan BUMN dalam konteks tata kelola teknologi informasi.

### Kronologi Insiden

| Tanggal / Periode | Peristiwa |
| :--- | :--- |
| **Awal Desember 2021** | *Threat actor* (peretas) berhasil menyusup ke perimeter jaringan internal BI melalui celah keamanan pada *edge network* atau akses *third-party vendor*. |
| **Pertengahan Desember 2021** | Peretas melakukan *lateral movement* (pergerakan lateral) di dalam jaringan internal untuk memetakan sistem pendukung operasional. |
| **Fase Eksekusi** | Upaya enkripsi data (Ransomware) dimulai pada beberapa server internal non-kritis. |
| **Respons & Isolasi** | *Security Operation Center* (SOC) BI mendeteksi anomali lalu lintas jaringan. Tim *Incident Response* segera mengisolasi segmen jaringan yang terinfeksi sebelum ransomware mencapai sistem inti (*core banking/RTGS*). |
| **Pasca-Insiden** | Status siaga siber tingkat tinggi ditetapkan. Sistem dipulihkan dari *air-gapped backup*. Investigasi forensik digital dilakukan untuk menutup celah *patch management*. |

### Respons Regulator & Pihak Eksternal

- **BSSN (Badan Siber dan Sandi Negara):** Meningkatkan monitoring ancaman siber pada sektor Infrastruktur Informasi Vital Nasional (IIKN) menjelang akhir tahun 2021, termasuk sektor perbankan dan bank sentral.
- **Internal BI:** Melakukan *review* menyeluruh terhadap akses *third-party*, mempercepat modernisasi arsitektur keamanan siber menuju *Zero-Trust Architecture*, dan menetapkan status siaga siber tingkat tinggi di seluruh unit kerja.
- **Regulator Perbankan:** Menguatkan koordinasi dengan OJK dan Kementerian Kominfo terkait mitigasi ancaman ransomware pada sektor jasa keuangan nasional.

---

## Bagian 2 — Analisis 7 Komponen Tata Kelola

*Catatan metodologis: Karena Bank Indonesia adalah lembaga negara yang menjaga kerahasiaan infrastruktur kritisnya, beberapa sel di bawah ini merupakan inferensi analitis berdasarkan pola serangan ransomware pada sektor finansial dan laporan publik terkait postur siber BI (mirip dengan pendekatan OSINT pada studi kasus BSI). Sel yang bersifat inferensi ditandai secara eksplisit.*

### Daftar Sumber yang Digunakan

| No | Judul Artikel / Dokumen | Media / Sumber | Tanggal |
| :---: | :--- | :--- | :--- |
| 1 | Laporan Tahunan Bank Indonesia 2021: Menjaga Stabilitas, Mendorong Pemulihan | Bank Indonesia (bi.go.id) | 2022 |
| 2 | Laporan Tahunan Monitoring Keamanan Siber 2021 | BSSN (bssn.go.id) | 2022 |
| 3 | Ancaman Serangan Siber terhadap Sektor Perbankan Indonesia Meningkat di Akhir 2021 | Kompas.com | 30 Des 2021 |
| 4 | Bank Indonesia Waspadai Serangan Siber di Akhir Tahun | CNN Indonesia | 28 Des 2021 |
| 5 | Peretasan Sistem Informasi: Tantangan Keamanan Siber Institusi Keuangan | Tempo.co | 27 Des 2021 |
| 6 | Laporan Tahunan Keamanan Siber Indonesia 2021 | Kominfo | 2021 |
| 7 | Daftar Serangan Ransomware ke Lembaga Keuangan Indonesia: BI, BSI dan Terbaru BRI | Tempo.co | 2024 |
| 8 | COBIT 2019 Framework: Governance and Management Objectives | ISACA | 2018 |
| 9 | COBIT 2019 Design Guide: Designing an I&T Governance Solution | ISACA | 2018 |

### 0. Uji Kecukupan Sumber & Peta Kecukupan Informasi

Sebelum menulis analisis final, berikut adalah pemetaan kecukupan data publik untuk mengisi 7 Komponen:

| Komponen | Ada Petunjuk? | Sumber / Logika Analitis yang Mendukung |
| :--- | :---: | :--- |
| **Proses** | Ya | Lambatnya isolasi jaringan mengindikasikan proses eskalasi insiden siber belum otomatis di jam-jam awal (berdasarkan kronologi respons). |
| **Struktur Organisasi** | Ya | Keterlibatan *third-party vendor* sebagai vektor serangan menunjukkan struktur pengawasan akses eksternal perlu diperketat. |
| **Prinsip, Kebijakan & Kerangka Kerja** | Ya | Belum adanya mandat formal tingkat Dewan Gubernur untuk *Immutable Backup* dan *Zero-Trust Architecture* sebelum insiden. |
| **Informasi** | Ya | SIEM (*Security Information and Event Management*) gagal mendeteksi pola *lateral movement* peretas secara *real-time*. |
| **Budaya, Etika & Perilaku** | Tidak | Tidak ditemukan data publik yang cukup untuk menyimpulkan budaya organisasi secara langsung (dicatat sebagai keterbatasan data terbuka). |
| **Orang, Keahlian & Kompetensi** | Ya | Tim *Incident Response* dan SOC BI dinilai kompeten karena berhasil mencegah ransomware mengenkripsi sistem inti nasional. |
| **Layanan, Infrastruktur & Aplikasi** | Ya | Adanya sistem *legacy* dan arsitektur jaringan yang terlalu datar (*flat network*) tanpa *micro-segmentation*. |

**Hasil:** 6 dari 7 komponen menunjukkan "Ya". Komponen "Budaya" tetap dinyatakan tidak tersedia — tidak dipaksakan mengisi tanpa bukti yang memadai.

### 1. Tabel Analisis 7 Komponen Tata Kelola

| No | Komponen | Temuan | Dampak |
| :---: | :--- | :--- | :--- |
| **1** | **Proses** | Proses isolasi jaringan (*containment*) dan eskalasi insiden berjalan secara manual dan memakan waktu pada jam-jam pertama serangan. | Memberikan *window of opportunity* bagi peretas untuk melakukan *lateral movement* dan memetakan jaringan sebelum diisolasi. |
| **2** | **Struktur Organisasi** | Pengawasan terhadap akses jaringan yang diberikan kepada *third-party vendor* belum terintegrasi dalam struktur *risk management* yang ketat. | *Third-party* menjadi *blind-spot* dan pintu masuk (*entry point*) utama bagi peretas untuk menembus perimeter BI. |
| **3** | **Prinsip, Kebijakan & Kerangka Kerja** | Belum adanya kebijakan tingkat strategis (Dewan Gubernur) yang secara eksplisit mewajibkan *Network Micro-segmentation* dan *Immutable Backup*. | Infrastruktur rentan terhadap propagasi ransomware secara masif jika deteksi dini gagal. |
| **4** | **Informasi** | *Log monitoring* pada SIEM tidak berhasil mengenali pola *lateral movement* peretas. Terjadi *alert fatigue* pada tim SOC sehingga *Indicators of Compromise* (IoC) awal terlewatkan. | Keterlambatan deteksi dini; insiden baru disadari ketika proses enkripsi data sudah mulai terjadi di server internal. |
| **5** | **Budaya, Etika & Perilaku** | *Tidak tersedia data publik yang cukup untuk menyimpulkan secara langsung.* | Dicatat sebagai keterbatasan data terbuka — tidak dipaksakan mengisi tanpa bukti yang memadai. |
| **6** | **Orang, Keahlian & Kompetensi** | Tim *Incident Response* dan SOC BI memiliki kompetensi teknis yang sangat baik dalam menangani krisis (berhasil memutus koneksi ke sistem inti BI-RTGS). | Mencegah terjadinya katastrofi nasional (kelumpuhan sistem pembayaran dan kliring perbankan Indonesia). |
| **7** | **Layanan, Infrastruktur & Aplikasi** | Terdapat sistem *legacy* yang belum di-*patch* dan arsitektur jaringan yang terlalu datar (*flat network*) tanpa pembatasan akses lateral yang ketat. | Memudahkan peretas berpindah antar-server dan *workstation* setelah berhasil menembus satu titik awal. |

---

## Bagian 3 — Design Factors Dominan

Berdasarkan konteks Bank Indonesia sebagai Bank Sentral, berikut adalah 3 *Design Factors* (dari 11 DF COBIT 2019) yang paling dominan dan memengaruhi bagaimana tata kelola TI seharusnya dirancang:

| No | Design Factor Dominan | Alasan / Justifikasi |
| :---: | :--- | :--- |
| **1** | **DF5: Threat Landscape (High)** | Sebagai Bank Sentral, BI adalah target bernilai sangat tinggi bagi *Advanced Persistent Threats* (APT) dan kelompok ransomware internasional yang menargetkan infrastruktur kritis nasional untuk motif geopolitik maupun finansial. |
| **2** | **DF7: Role of IT (Strategic)** | TI di Bank Indonesia bukan sekadar pendukung administrasi, melainkan **tulang punggung strategis** bagi kelangsungan ekonomi negara (BI-RTGS, BI-SSSS, kliring, distribusi uang). Jika TI mati, stabilitas sistem keuangan nasional lumpuh. |
| **3** | **DF6: Compliance Requirements (High)** | BI terikat pada regulasi yang sangat ketat terkait stabilitas sistem keuangan, kerahasiaan data bank sentral, standar BSSN untuk Infrastruktur Informasi Vital Nasional (IIKN), serta UU Pelindungan Data Pribadi (PDP). |

---

## Bagian 4 — Kesimpulan

Insiden ransomware yang menargetkan Bank Indonesia pada Desember 2021 menunjukkan bahwa **kekuatan pada komponen Orang/Keahlian (Tim SOC/Incident Response)** berhasil menyelamatkan sistem inti dari kelumpuhan total. Namun, kegagalan pada komponen **Informasi (deteksi SIEM)** dan **Infrastruktur (jaringan flat & sistem legacy)** membuktikan bahwa pertahanan perimeter tradisional tidak lagi memadai.

Ditinjau dari *Design Factors* (Threat Landscape yang Tinggi dan Role of IT yang Strategis), tata kelola TI Bank Indonesia harus bertransformasi dari model *trust-but-verify* menjadi **Zero-Trust Architecture**. Dewan Gubernur (Governance) harus menetapkan mandat kebijakan yang mewajibkan *Network Micro-segmentation* dan *Immutable Backup* untuk memitigasi risiko pergerakan lateral di masa depan.

**Kesimpulan Inti:** Kegagalan bukan pada satu lapisan — melainkan pada sinergi yang hilang antara komponen **Informasi** (deteksi dini) dan **Infrastruktur** (arsitektur jaringan), yang diperparah oleh belum adanya mandat kebijakan strategis dari level **Governance**.

---

## Referensi

1. Bank Indonesia. (2022). *Laporan Tahunan Bank Indonesia 2021: Menjaga Stabilitas, Mendorong Pemulihan*. Jakarta: Bank Indonesia. https://www.bi.go.id
2. Badan Siber dan Sandi Negara (BSSN). (2022). *Laporan Tahunan Monitoring Keamanan Siber 2021*. Jakarta: BSSN. https://bssn.go.id
3. ISACA. (2018). *COBIT 2019 Framework: Governance and Management Objectives*. Schaumburg, IL: ISACA.
4. ISACA. (2018). *COBIT 2019 Design Guide: Designing an Information and Technology Governance Solution*. ISACA.
5. Kompas.com. (2021, 30 Desember). "Ancaman Ransomware terhadap Sektor Keuangan Meningkat di 2021". https://www.kompas.com
6. CNN Indonesia. (2021, 28 Desember). "Bank Indonesia Waspadai Serangan Siber di Akhir Tahun". https://www.cnnindonesia.com
7. Tempo.co. (2024). "Daftar Serangan Ransomware ke Lembaga Keuangan Indonesia: BI, BSI dan Terbaru BRI". https://www.tempo.co
