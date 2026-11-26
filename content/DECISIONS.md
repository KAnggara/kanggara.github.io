---
title: Architecture Decision Records
---

# Architecture Decision Records (ADRs)

Dokumen ini mencatat keputusan arsitektur utama ekosistem **KAnggara** secara *append-only*.

---

## ADR-001: Adopsi GitOps K3s dengan ArgoCD App-of-Apps dan Traefik Ingress

- **Status**: Accepted
- **Date**: 2026-11-26
- **Context**: Infrastruktur membutuhkan pengelolaan klaster Kubernetes multi-tenant beserta sertifikat TLS otomatis dan ingress routing yang ringkas tanpa lapisan proxy VM tambahan.
- **Decision**: Menggunakan **ArgoCD** dengan pola *App-of-Apps* untuk mengorkestrasi komponen platform inti dan workload aplikasi berbasis *Shared Single-Chart Pattern*. Seluruh trafik masuk ditangani langsung oleh **Traefik Ingress** dan **Cert-Manager** (`DNS-01`).
- **Consequences**: Konfigurasi klaster menjadi deklaratif, mendukung *self-healing*, dan mengurangi kompleksitas hop jaringan di depan klaster.

---

## ADR-002: Standarisasi Manajemen Secret Menggunakan Sealed Secrets

- **Status**: Accepted
- **Date**: 2026-11-26
- **Context**: Alur GitOps membutuhkan mekanisme penyimpanan secret di repositori Git yang aman, terenkripsi, dan terintegrasi langsung dengan Kubernetes tanpa bergantung pada server secret eksternal berbayar.
- **Decision**: Menetapkan **Bitnami Sealed Secrets** (`kubeseal` + in-cluster controller) sebagai standar enkripsi Kubernetes Secret di repositori GitOps.
- **Consequences**: Seluruh kredensial di Git tersimpan dalam bentuk terenkripsi (`SealedSecret`) dan hanya dapat didekripsi oleh controller di dalam klaster target.

---

## ADR-003: Konsolidasi Layanan Konfigurasi Aplikasi

- **Status**: Accepted
- **Date**: 2026-11-26
- **Context**: Konfigurasi YAML per environment sebelumnya dilayani oleh Spring Cloud Config Server berbasis JVM yang membutuhkan resource lebih besar.
- **Decision**: Mengalihkan konsumsi repositori konfigurasi YAML per environment ke layanan konfigurasi yang lebih ringan ([conflect](https://github.com/KAnggara75/conflect)).
- **Consequences**: Jejak memori (*memory footprint*) komponen konfigurasi lebih efisien dengan pemisahan environment (`local`, `dev`, `stg`, `prd`) yang tetap terjaga.

---

## ADR-004: Migrasi Dokumentasi Publik ke Quartz (GitHub Pages)

- **Status**: Accepted
- **Date**: 2026-11-26
- **Context**: Platform wiki dinamis sebelumnya membutuhkan server runtime terpisah, sedangkan dokumentasi teknis berbasis Markdown dapat di-publish secara statis.
- **Decision**: Mengimplementasikan **Quartz** pada `kanggara.github.io` dengan workflow CI/CD otomatis ke GitHub Pages, menggantikan platform wiki berbasis PHP/Laravel.
- **Consequences**: Hosting gratis, performa tinggi, zero server maintenance, serta mendukung fitur wiki modern (pencarian teks penuh, backlinks, dan *graph view*).

---

## ADR-005: Backup Terjadwal Menggunakan Kubernetes CronJob

- **Status**: Accepted
- **Date**: 2026-11-26
- **Context**: Basis data operasional membutuhkan mekanisme backup otomatis di luar klaster Kubernetes.
- **Decision**: Menjalankan backup database terjadwal menggunakan Kubernetes `CronJob` yang dikelola via ArgoCD dengan sinkronisasi off-cluster ke penyimpanan cloud.
- **Consequences**: Proses backup terotomasi, terjadwal, dan mudah diaudit melalui log serta status job di Kubernetes.
