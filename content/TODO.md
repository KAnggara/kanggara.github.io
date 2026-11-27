---
title: Engineering Roadmap
---

# Engineering Roadmap

Daftar inisiatif arsitektur dan penyempurnaan platform:

## 1. Platform & GitOps Consolidation *(Selesai)*
- [x] **Konsolidasi Repositori GitOps**: Menyatukan struktur definisi deployment dan workload ke dalam satu pola *single source of truth* berbasis ArgoCD.
- [x] **Standarisasi Enkripsi Secret**: Mengadopsi **Bitnami Sealed Secrets** di klaster dan mengenkripsi secret GitOps.
- [x] **Integrasi Config Service**: Mengalihkan konsumsi konfigurasi per environment ke layanan konfigurasi terpusat.

## 2. Documentation & Reliability *(Aktif)*
- [x] **Migrasi Konten Wiki**: Mengimplementasikan portal dokumentasi **Quartz** (`kanggara.github.io`) dan menghentikan platform wiki lama.
- [ ] **Verifikasi Backup & Off-Cluster Sync**: Memastikan *scheduled backup CronJob* berjalan normal dan melengkapi konfigurasi secret terenkripsi (`SealedSecret`) untuk sinkronisasi off-cluster.
- [ ] **Formalisasi Standar Reliabilitas**: Menetapkan target **SLA**, **RPO**, dan **RTO** serta jadwal pengujian *restore* backup berkala.
- [ ] **Standarisasi Dokumentasi Repo**: Melengkapi `README.md` di seluruh repositori pendukung agar konsisten.
