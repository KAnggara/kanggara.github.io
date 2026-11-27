---
title: Engineering Roadmap
---

# Engineering Roadmap

Daftar inisiatif arsitektur dan penyempurnaan platform yang masih berjalan:

- [ ] **Verifikasi Backup & Off-Cluster Sync**: Memastikan *scheduled backup CronJob* berjalan normal dan melengkapi konfigurasi secret terenkripsi (`SealedSecret`) untuk sinkronisasi off-cluster.
- [ ] **Formalisasi Standar Reliabilitas**: Menetapkan target **SLA**, **RPO**, dan **RTO** serta jadwal pengujian *restore* backup berkala.
