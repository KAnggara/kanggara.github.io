---
title: Project Context
---

# Project Context (`KAnggara`)

## 1. Project Purpose
Ekosistem rekayasa platform **KAnggara** bertujuan menstandarkan proses CI/CD, provisioning infrastruktur, orkestrasi Kubernetes berbasis GitOps, manajemen konfigurasi terpusat, dan dokumentasi teknis dalam satu kerangka kerja yang terotomasi.

## 2. System Boundary
- **In-Scope**:
  - *Reusable* GitHub Composite Actions untuk build, test, dan deployment.
  - Otomasi provisioning server dan jaringan mesh privat.
  - Orkestrasi klaster K3s, ArgoCD control plane, Ingress Traefik, Cert-Manager, RBAC, dan Admission Policies.
  - Shared Helm chart, manajemen konfigurasi per environment, migrasi skema database, dan definisi topik Kafka.
  - Dokumentasi teknis publik berbasis Quartz SSG.
- **External Systems**:
  - Cloud DNS & ACME Certificate Authority (Cloudflare & Let's Encrypt).
  - Container Registry (`ghcr.io`) & penyimpanan backup cloud.
  - Managed backing services (database & cache eksternal).

## 3. Main Actors
- **Platform Engineer / Developer**: Mengelola kode infrastruktur, Pull Request GitOps, dan pipeline CI/CD.
- **GitHub Actions Runner**: Menjalankan pipeline pengujian, container build, dan publikasi dokumentasi statis.
- **ArgoCD Controller**: Melakukan sinkronisasi deklaratif state klaster Kubernetes dari repositori Git.

## 4. Domain Concepts & Glossary
- **App-of-Apps**: Pola ArgoCD untuk mem-bootstrap komponen platform inti dan workload aplikasi secara berjenjang.
- **Shared Single-Chart Pattern**: Penggunaan satu chart Helm generik yang dikustomisasi melalui file values per layanan.
- **ValidatingAdmissionPolicy**: Kebijakan validasi native Kubernetes untuk menegakkan aturan penempatan workload (*pod placement*) dan keamanan klaster.
- **Sealed Secrets**: Mekanisme enkripsi satu arah untuk menyimpan Kubernetes `Secret` secara aman di repositori Git.

## 5. Runtime Environment & Constraints
- **Container & Orchestration**: Kubernetes **K3s** dengan Rancher System Upgrade Controller, Longhorn Storage, dan Traefik Ingress.
- **Networking**: Jaringan mesh VPN privat antar node serta `ExternalName` Services untuk integrasi layanan eksternal.
- **Static Docs Runtime**: Node.js `>=22.22` & npm `>=10.9.2` untuk Quartz `v5.2.2`.

## 6. Coding Conventions & Standards
- **Commit Message**: Mengikuti spesifikasi **Conventional Commits** (`feat`, `fix`, `refactor`, `docs`, `test`, `chore`, `perf`, `ci`).
- **Sync Policy ArgoCD**: Standarisasi `Validate=true` dan `PruneLast=true`.
- **Dokumentasi**: Menggunakan relative Markdown file path yang portabel untuk Obsidian, Quartz, dan Git preview.
