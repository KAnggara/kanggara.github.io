---
title: Engineering Roadmap
---

# Engineering Roadmap

Daftar inisiatif arsitektur dan penyempurnaan platform yang direncanakan:

## 1. Platform & GitOps Consolidation
- [ ] **Konsolidasi Repositori GitOps**: Menyatukan struktur definisi deployment dan workload ke dalam satu pola *single source of truth* berbasis ArgoCD.
- [ ] **Standarisasi Enkripsi Secret**: Menyelesaikan adopsi penuh **Sealed Secrets** di seluruh workload klaster.
- [ ] **Integrasi Config Service**: Menyempurnakan integrasi alur konfigurasi terpusat per environment (`local`, `dev`, `stg`, `prd`).

## 2. Documentation & Reliability
- [ ] **Migrasi Konten Wiki**: Memindahkan dokumentasi teknis yang relevan ke portal **Quartz** (`kanggara.github.io`) dan mengarsipkan platform wiki lama.
- [ ] **Formalisasi Standar Reliabilitas**: Menetapkan target SLA, RPO, dan RTO serta jadwal pengujian *restore* berkala.
- [ ] **Standarisasi Dokumentasi Repo**: Melengkapi `README.md` di seluruh repositori pendukung agar konsisten.
