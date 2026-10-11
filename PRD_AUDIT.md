# CAStudio PRD Audit — Vault prd.md (FR-01..21) + omni-channel-automation-prd.md vs Implementasi

> Audit: 2026-10-11 · Base: `/home/cecepazhar/Product/castudio` · Metode: statis

## Hasil: 16/21 FR (76%) · Design Compliance: PASS (kecuali i18n)

### Gap

| FR | Gap | Detail | Severity |
|---|---|---|---|
| FR-06 | Marketing generator TIDAK ADA | Tak ada copy generator pemasaran di core. | P1 |
| FR-11 | Social Hub TIDAK ADA | Tak ada module social scheduling/queue terdedikasi. | P0 |
| FR-12 | Clipper desktop TIDAK ADA | Tak ada clipper (web→draft). | P0 |
| FR-18 | i18n TIDAK ADA (0 file) | PRD v1 wajib dwibahasa; castudio 0 file i18n. | P1 |
| FR-05 | Webinar/E-Course parsial | `templates.rs` slide deck ada; webinar & e-course belum lengkap. | P1 |
| FR-09 | Kalender konten parsial | `automation/scheduler.rs` drip calendar; tanpa route UI khusus. | P2 |
| FR-13 | Media generation parsial | Video-script generator = promp→naskah, bukan render media nyata. | P2 |
| FR-14 | `.castudio` bundle parsial | Export per-dokumen; format bundel proyek terpadu belum ada. | P2 |

### Omni-Channel PRD (Tahap 5: 5 platform target)
Dispatcher nyata: **WordPress, Ghost, Telegram, n8n_webhook, custom_webhook** (5 target terpenuhi secara teknis, tapi bukan daftar PRD).
PRD minta: **WP, Ghost, Astro, Telegram, X/Twitter** → **Astro ❌**, **X/Twitter ❌** (grep `document.rs`/`repurposing.rs` hanya mention, bukan adapter). **2/5 platform PRD absen.**

### Bukti Implementasi (key)
- Core modules: `project.rs` (Project Bible), `ai.rs` (provider hub), `export.rs` (epub/html), `repurposing.rs` (Launch Pack), `templates.rs` (presentation, pitchdeck, cover), `document.rs` (Content Builder blocks: paragraph, heading, list, image, quote, callout, code, button), `prompt_studio.rs` (multi-persona prompt chains + variable injection), `automation/{inbound_server (webhook+auth), dispatcher (WP/Ghost/Telegram/n8n/webhook), scheduler (drip), adapters: wordpress, ghost, telegram, n8n_webhook, custom_webhook, formatter}`.
- Frontend routes: content, ebook, repurpose, pitchdeck, prompt-studio, instagram + components ContentBuilder.svelte (block canvas), InstagramStudio.svelte (carousel/reels/feed/stories 4:5), FloatingAiCard.svelte.

### Rekomendasi
1. P0: FR-11 Social Hub + FR-12 Clipper — inti "content automation" PRD.
2. P1: FR-06 marketing generator; FR-18 i18n (elemen wajib PRD v1).
3. P1: Adapter Astro (static deploy) + X/Twitter API v2 thread — 2/5 target omni-channel.
4. P2: Bundle `.castudio` terpadu + media render nyata (FR-13/14).