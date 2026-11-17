# Dokumentasi Proyek agent-gantulu

Dokumen ini menjadi indeks dokumentasi dan kumpulan referensi teknis untuk repository **agent-gantulu**.

## 1. Tujuan Dokumentasi

Repository ini mendokumentasikan arsitektur AI Agent yang menggunakan ChatGPT Native sebagai pusat reasoning dan pengambilan keputusan, Custom MCP Server sebagai penghubung tools, serta Supabase sebagai backend dan lapisan persistensi.

Repository juga memuat aset dokumentasi untuk template prompt, data produk, dan spesifikasi pengisian variable oleh Prompt Builder.

## 2. Dokumen Proyek

| File | Fungsi | Status |
|---|---|---|
| [requirement.md](./requirement.md) | Sumber kebenaran kebutuhan dan batasan arsitektur proyek | Requirement baseline |
| [ai-agent.md](./ai-agent.md) | Identitas, peran, alur kerja, kebijakan tools, state, dan guardrails AI Agent | Draft |
| [template-prompt.md](./template-prompt.md) | Template statis untuk menghasilkan prompt AI image generation | Template |
| [products.json](./products.json) | Data produk dan daftar fitur produk | Data |
| [variable-filling-spec.md](./variable-filling-spec.md) | Aturan sumber, pemetaan, pengisian, dan validasi variable template | Approved V1.0 |

### 2.1 Prioritas Dokumen

1. `requirement.md` adalah acuan utama untuk kebutuhan dan batasan arsitektur proyek.
2. `ai-agent.md` menjabarkan perilaku dan tanggung jawab AI Agent, dan tidak boleh bertentangan dengan `requirement.md`.
3. `variable-filling-spec.md` menjadi acuan pengisian variable Prompt Builder V1.0.
4. `template-prompt.md` adalah template statis. Pengisian placeholder dilakukan oleh Prompt Builder, bukan dengan mengubah template.
5. `products.json` adalah sumber data produk untuk variable produk dan fitur.

Jika ditemukan konflik antardokumen, ikuti dokumen dengan prioritas lebih tinggi dan selesaikan konflik melalui revisi yang disetujui. Jangan mengasumsikan keputusan baru.

## 3. Arsitektur Integrasi

### 3.1 Komponen

| Komponen | Tanggung jawab |
|---|---|
| ChatGPT Native | Memahami instruksi, reasoning, perencanaan, dan pengambilan keputusan |
| Custom MCP Server | Menyediakan tools dan menjembatani ChatGPT dengan sistem eksternal |
| Supabase Edge Functions | Menjalankan backend logic dan memproses permintaan |
| Supabase Database | Menyimpan dan mengelola data serta state |
| Supabase Storage | Menyimpan file dan gambar |

### 3.2 Alur Integrasi

```text
ChatGPT Native
      |
      v
Custom MCP Server
      |
      v
Supabase Edge Functions
      |
      +------ Supabase Database
      |
      +------ Supabase Storage
```

Diagram ini menunjukkan alur integrasi konseptual. Detail implementasi tetap mengikuti `requirement.md` dan keputusan teknis yang telah disetujui.

## 4. Referensi Supabase Edge Functions

Dokumentasi resmi: https://supabase.com/docs/guides/functions

| Topik | Referensi |
|---|---|
| Dokumentasi utama | https://supabase.com/docs/guides/functions |
| Quickstart | https://supabase.com/docs/guides/functions/quickstart |
| Deploy Edge Functions | https://supabase.com/docs/guides/functions/deploy |
| Local Development | https://supabase.com/docs/guides/functions/local-development |
| Environment Variables & Secrets | https://supabase.com/docs/guides/functions/secrets |
| Database Access | https://supabase.com/docs/guides/functions/connect-to-postgres |
| Background Tasks | https://supabase.com/docs/guides/functions/background-tasks |
| HTTP Methods | https://supabase.com/docs/guides/functions/http-methods |
| Examples | https://supabase.com/docs/guides/functions/examples |

Referensi umum:
- Supabase Documentation: https://supabase.com/docs
- Supabase GitHub: https://github.com/supabase/supabase

## 5. Referensi OpenAI Custom MCP Server

Dokumentasi resmi: https://developers.openai.com/api/docs/guides/custom-mcp-server

Referensi ini digunakan untuk memahami integrasi Custom MCP Server dengan ekosistem OpenAI, termasuk penyediaan tools agar model AI dapat berinteraksi dengan sistem eksternal.

Referensi tambahan:
- OpenAI Developers: https://developers.openai.com/

**Batas penggunaan referensi:** Dokumentasi Custom MCP Server digunakan sebagai referensi mekanisme integrasi MCP. Referensi ini bukan persetujuan untuk menggunakan OpenAI Agents API, Agents SDK, atau memindahkan runtime percakapan dari ChatGPT Native. Batasan arsitektur yang berlaku tetap mengacu pada `requirement.md`.

## 6. Fokus Pembelajaran

| Area | Fokus |
|---|---|
| ChatGPT Native | Reasoning, memahami instruksi, perencanaan, dan pengambilan keputusan |
| Custom MCP Server | Penyediaan tools dan integrasi dengan sistem eksternal |
| Supabase Edge Functions | Backend logic dan pemrosesan permintaan |
| Supabase Database | Persistensi data, status, dan konteks |
| Supabase Storage | Penyimpanan file dan gambar |

## 7. Status Implementasi

Dokumentasi ini tidak menyatakan bahwa komponen arsitektur telah diimplementasikan atau terhubung. Status implementasi harus diverifikasi dari kode, konfigurasi, dan deployment yang sebenarnya.

Perubahan arsitektur, penambahan komponen, atau perubahan ruang lingkup harus melalui proses review dan persetujuan sesuai `requirement.md`.

## 8. Prinsip Pemeliharaan Dokumentasi

- Pertahankan nama file, field, komponen, endpoint, dan istilah yang telah ditetapkan.
- Perbarui indeks ini ketika dokumen proyek ditambah, dihapus, atau berganti status.
- Jangan menyalin seluruh isi dokumen lain ke file ini; gunakan tautan dan ringkasan fungsi dokumen.
- Bedakan dengan jelas antara requirement yang disetujui, draft, referensi, dan implementasi aktual.
- Jangan menganggap contoh atau referensi teknis sebagai keputusan implementasi tanpa persetujuan.
