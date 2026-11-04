# 📑 Subsistem Penerimaan Donasi Luring — Baitulmal Tazkia (BMTZ)

[![Document ID](https://img.shields.io/badge/Document%20ID-BMTZ--SRS--OFFLINE--001-blue.svg)](docs/srs.md)
[![SRS Version](https://img.shields.io/badge/Version-0.3-emerald.svg)](docs/srs.md)
[![Standard](https://img.shields.io/badge/Standard-ISO%2FIEC%2FIEEE%2029148%3A2018-orange.svg)](https://www.iso.org/standard/72089.html)
[![Quality Standard](https://img.shields.io/badge/Quality-ISO%2FIEC%2025010%3A2023-purple.svg)](https://www.iso.org/standard/78176.html)
[![Architecture](https://img.shields.io/badge/Architecture-Offline--First%20PWA-darkgreen.svg)](#-arsitektur--teknologi)
[![License](https://img.shields.io/badge/License-Academic%20STMIK%20Tazkia-gray.svg)](#)

> **Dokumentasi Resmi & Spesifikasi Kebutuhan Perangkat Lunak (SRS)**  
> Digitalisasi pencatatan donasi luring (*booth* & event) berarsitektur *offline-first* dengan sinkronisasi otomatis, deduplikasi `UUID v7`, log operasi *Last-Write-Wins*, dan *audit trail* serah-terima kas berjenjang.

---

## 📌 Ringkasan Eksekutif

**Subsistem Penerimaan Donasi Luring** adalah salah satu modul dari ekosistem digital **Baitulmal Tazkia (Sentul, Bogor)** yang dikembangkan oleh **Kelompok 6 (Klaster Kanal dan Luring)**. 

Sistem ini dirancang berbasis *Progressive Web App* (PWA) *offline-first* untuk menyelesaikan masalah pencatatan manual di lapangan saat sinyal internet buruk atau mati total (seperti di mal, masjid, dan lokasi acara pameran).

### 🎯 Fitur Utama & Keunggulan Arsitektur
* 📵 **Offline-First & PWA:** Transaksi tetap lancar tanpa koneksi internet menggunakan penyimpanan lokal `IndexedDB`.
* 🆔 **Idempotensi & Deduplikasi Client-Side:** Generasi ID berbasis **UUID v7** (*time-ordered*) di sisi klien mencegah duplikasi data saat pengiriman ulang.
* 🔄 **Operation Log & Conflict Resolution:** Mengadopsi mekanisme *Last-Write-Wins* (LWW) per-field serta penampungan otomatis transaksi konflik ke **Antrean Rekonsiliasi** (`CONFLICT_QUEUED`).
* 💵 **Serah-Terima Uang Tunai Berjenjang 2 Tahap:** Pencatatan otomatis alur pertanggungjawaban fisik kas: `Petugas Booth ➔ Koordinator Lapangan ➔ Bagian Keuangan & Setor Bank` dilengkapi kalkulasi selisih (*discrepancy note*).
* 🛡️ **Kepatuhan UU PDP No. 27/2022:** Minimalisasi pengumpulan data pribadi di *booth* & fitur *auto-purge* cache lokal setelah sinkronisasi.

---

## 👥 Tim Pengembang (Kelompok 6)

| No | Nama | NPM | Peran / Tanggung Jawab Utama | Kontak |
| :---: | :--- | :---: | :--- | :---: |
| **1** | **Dieria Febrianti** | `251572010043` | Business Analyst & Requirement Manager | [![GitHub](https://img.shields.io/badge/-GitHub-181717?style=flat&logo=github)](https://github.com/) |
| **2** | **Naisyra Mazeela Putri Yusman** | `251572010027` | Data Analyst & Repository Owner | [![GitHub](https://img.shields.io/badge/-GitHub-181717?style=flat&logo=github)](https://github.com/) |
| **3** | **Muhamad Fuadi Ma'suf** | `251572010035` | Lead Developer (Full Stack & Architecture) | [![GitHub](https://img.shields.io/badge/-GitHub-181717?style=flat&logo=github)](https://github.com/fuaditech) |
| **4** | **M. Jusan Bahrudin** | `251572010022` | Core Developer (Full Stack Implementation) | [![GitHub](https://img.shields.io/badge/-GitHub-181717?style=flat&logo=github)](https://github.com/) |

* **Tim Pendamping (RC):** Tim 2 — Kanal dan Operasional (Semester 5)
* **Dosen Pengampu:** Endy Muhardin

---

## 📂 Struktur Repositori

```text
.
├── 📄 README.md                   # Dokumentasi utama & lanskap repositori
├── 📂 docs/                       # Seluruh artefak dokumentasi resmi
│   ├── 📄 srs.md                  # Dokumen SRS Lengkap (BMTZ-SRS-OFFLINE-001 v0.3)
│   ├── 📄 stakeholder-register.md # Daftar pemangku kepentingan & RACI matrix
│   ├── 📂 bpmn/                   # Model proses bisnis (OMG BPMN 2.0)
│   │   └── 📄 as-is-penerimaan-donasi-luring.bpmn
│   ├── 📂 api/                    # Spesifikasi antarmuka & OpenAPI contract
│   │   ├── 📄 dependency-map.md   # Peta ketergantungan hulu/hilir
│   │   └── 📄 openapi-offline-donation.yaml
│   └── 📂 elicitation/            # Hasil wawancara verbatim & bukti observasi
└── 📂 src/                        # Kode sumber aplikasi (Backend & Frontend PWA)
