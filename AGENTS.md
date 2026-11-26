# AGENTS.md — KAnggara Workspace Guidelines

Panduan operasional dan standar rekayasa untuk ekosistem infrastruktur, CI/CD, GitOps Kubernetes, dan dokumentasi **KAnggara**.

---

## 1. Baseline Architecture & Wiki (`.context/`)
Baca dokumen arsitektur di direktori `.context/` sebelum melakukan perubahan lintas modul:

1. [Codebase Navigation Map](.context/CODEBASE_MAP.md) — Peta kapabilitas sistem dan komponen utama.
2. [Architecture Overview](.context/ARCHITECTURE.md) — Diagram komponen, alur CI/CD & GitOps, kebijakan klaster, dan observabilitas.
3. [Project Context](.context/PROJECT_CONTEXT.md) — Tujuan sistem, batasan, glossary, dan standar runtime.
4. [Architecture Decision Records](.context/DECISIONS.md) — Catatan keputusan arsitektur (*append-only*).
5. [Engineering Roadmap](.context/TODO.md) — Daftar inisiatif pengembangan dan penyempurnaan arsitektur.

---

## 2. Aturan Keamanan & Operasional
- **Zero Plaintext Secrets**: Dilarang keras menyimpan token, password, `kubeconfig`, atau kredensial mentah di repositori mana pun. Gunakan enkripsi berbasis **Sealed Secrets** (ADR-002).
- **Declarative Kubernetes**: Seluruh perubahan klaster dikelola secara deklaratif melalui GitOps (ArgoCD / Kustomize / Helm) dan mematuhi kebijakan *admission policy* klaster.
- **Tautan Dokumentasi**: Gunakan relative Markdown file path yang portabel untuk Obsidian, Quartz, dan Git preview. Hindari path absolut mesin lokal atau link langsung ke folder tanpa nama file.

---

## 3. Standar Delivery & Konvensi
- **Commit Message**: Gunakan **Conventional Commits** (`feat`, `fix`, `refactor`, `docs`, `test`, `chore`, `perf`, `ci`).
- **Validasi Sebelum Push**:
  - Untuk chart Helm: validasi rendering template sebelum commit.
  - Untuk situs wiki Quartz (`kanggara.github.io`): verifikasi dengan `npx quartz build` atau `npm run check`.
- **Workspace Skills**: Gunakan `/ka-git-commit`, `/ka-review`, `/ka-pr`, atau `/ka-context` sesuai alur kerja pengembangan.
