---
title: Codebase Navigation Map
---

# Ecosystem Map (`KAnggara`)

Dokumen ini memetakan komponen dan kapabilitas utama dalam ekosistem infrastruktur, CI/CD, GitOps Kubernetes, dan dokumentasi **KAnggara**.

## 1. CI/CD & Container Build

### Reusable DevOps Actions (Public)
- **Responsibility**: Koleksi *reusable GitHub Composite Actions* untuk build Docker BuildKit, GHCR image pruning, deployment Helm, build Maven, laporan coverage LCOV, unit test multi-runtime (Bun, Go, Maven, Node.js), dan semantic versioning via GitVersion.
- **Reference**: [KAnggara/DevOps](https://github.com/KAnggara/DevOps)
- **External Integrations**: GitHub Container Registry (`ghcr.io`), Kubernetes API.

### Container Images
- **Responsibility**: Kumpulan definisi `Dockerfile` dan konfigurasi runtime layanan pendukung untuk kebutuhan build dan deployment container.

---

## 2. Kubernetes & GitOps

### GitOps Control Plane
- **Responsibility**: Pusat orkestrasi deklaratif klaster berbasis **ArgoCD (App-of-Apps)** dan **Kustomize** untuk manajemen `AppProject` multitenancy (`core`, `data`, `observability`, `apps`), partisi namespace beserta `LimitRange`/`ResourceQuota`, serta bootstrap aplikasi.

### Cluster Core Infrastructure
- **Responsibility**: Fondasi klaster Kubernetes (K3s) meliputi **Traefik Ingress**, otomasi sertifikat TLS (**Cert-Manager**), kebijakan *admission control* (`ValidatingAdmissionPolicy`), **RBAC**, *rolling upgrade* node via Rancher System Upgrade Controller, serta integrasi *backing services*.

### Application Workloads & Deployment Charts
- **Responsibility**: Pengelolaan deployment aplikasi menggunakan pola **Shared Single-Chart Pattern** (Helm chart reusable dengan values terpisah per lingkungan) serta sinkronisasi ArgoCD untuk layanan produksi, staging, dan stack observabilitas.

---

## 3. Infrastructure & Provisioning

### Server Provisioning
- **Responsibility**: Panduan dan skrip otomasi (Bash & Ansible) untuk penyiapan server dari awal, meliputi hardening OS, setup container runtime, manajemen user/SSH, serta konfigurasi jaringan mesh VPN privat.

---

## 4. Application Configuration, Data & Jobs

### Externalized Configuration
- **Responsibility**: Manajemen konfigurasi aplikasi berbasis YAML yang dipisahkan berdasarkan lingkungan (`local`, `dev`, `stg`, `prd`) dan disajikan melalui layanan konfigurasi terpusat.

### Database & Schema Migrations
- **Responsibility**: Pengelolaan skema dan migrasi database terstruktur menggunakan **Flyway** serta otomasi backup berkala melalui Kubernetes `CronJob` menuju penyimpanan cloud eksternal.

### Event Streaming
- **Responsibility**: Definisi deklaratif topik **Apache Kafka** untuk arsitektur *event-driven*.

---

## 5. Documentation & Org Profile

### Public Wiki (`kanggara.github.io`)
- **Responsibility**: Portal wiki & dokumentasi publik berbasis **Quartz v5.2.2** yang dibangun dan dipublikasikan secara otomatis ke GitHub Pages melalui GitHub Actions.
- **Reference**: [index.md](index.md)
