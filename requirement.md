# REQUIREMENT FINAL
# Arsitektur AI Agent Berbasis ChatGPT Native + Custom MCP Server + Supabase

**Versi:** 1.0  
**Status:** Draft Final – Menunggu Persetujuan  
**Platform AI:** ChatGPT Native  
**Integrasi:** Custom MCP Server  
**Backend:** Supabase

---

# 1. Tujuan Proyek

Merancang sistem AI Agent yang menggunakan model AI native ChatGPT untuk memahami instruksi, melakukan reasoning, menyusun rencana, mengambil keputusan, dan menjalankan tugas melalui Custom MCP Server yang terhubung dengan Supabase.

Sistem mengadopsi konsep, struktur, dan mekanisme kerja Agents dari dokumentasi resmi OpenAI, tanpa menggunakan Agents API maupun Agents SDK.

Tujuan utama:

1. Memanfaatkan kemampuan reasoning ChatGPT Native.
2. Membangun arsitektur AI Agent yang modular.
3. Menyediakan kemampuan eksekusi melalui MCP Tools.
4. Mengintegrasikan AI Agent dengan Supabase.
5. Mendukung workflow bertahap dan berbasis kondisi.
6. Memungkinkan pengembangan spesialisasi agent.
7. Memastikan seluruh proses memiliki status, validasi, dan mekanisme pemulihan.

# 2. Referensi Dokumentasi Resmi

### 2.1. OpenAI Agents

https://developers.openai.com/api/docs/guides/agents

Digunakan sebagai referensi untuk mempelajari:

- Konsep AI Agent.
- Struktur dan komponen agent.
- Instructions.
- Reasoning dan planning.
- Tool usage.
- Orchestration.
- Handoffs.
- Multi-agent.
- Guardrails.
- State dan context.
- Tracing dan evaluasi.

**Batas penggunaan:** Dokumentasi digunakan sebagai referensi konseptual dan arsitektur, bukan implementasi Agents API atau Agents SDK.

### 2.2. OpenAI Custom MCP Server

https://developers.openai.com/api/docs/guides/custom-mcp-server

Digunakan sebagai referensi untuk:

- Pembuatan Custom MCP Server.
- Integrasi MCP dengan ChatGPT.
- Definisi dan registrasi tools.
- Tool calling.
- Pertukaran data.
- Autentikasi.
- Keamanan dan pembatasan akses.

# 3. Arsitektur Sistem

```text
┌────────────────────────────────────────┐
│             CHATGPT NATIVE             │
│                                        │
│  AI Model                              │
│  Reasoning                             │
│  Decision Making                       │
│  Planning                              │
│  Task Understanding                    │
└────────────────────┬───────────────────┘
                     │
                     ▼
┌────────────────────────────────────────┐
│          AI AGENT ARCHITECTURE         │
│                                        │
│  Agent Instructions                    │
│  Input Understanding                   │
│  Reasoning                             │
│  Planning                              │
│  Tool Selection                        │
│  Orchestration                         │
│  State & Context Management            │
│  Guardrails                            │
└────────────────────┬───────────────────┘
                     │
                     ▼
┌────────────────────────────────────────┐
│           CUSTOM MCP SERVER            │
│                                        │
│  MCP Tools                             │
│  Functions                             │
│  Workflow                              │
│  Data Access                           │
│  Validation                            │
│  Backend Execution                     │
└────────────────────┬───────────────────┘
                     │
                     ▼
┌────────────────────────────────────────┐
│               SUPABASE                 │
│                                        │
│  PostgreSQL                            │
│  Storage                               │
│  Edge Functions                        │
│  State Persistence                     │
│  Execution Logs                        │
│  Configuration                         │
└────────────────────────────────────────┘
```

### 3.1. Prinsip Arsitektur

- ChatGPT Native menjadi pusat kecerdasan sistem.
- Model AI tetap menggunakan model yang tersedia melalui ChatGPT.
- MCP menjadi jembatan komunikasi dengan sistem eksternal.
- Supabase menjadi backend penyimpanan dan pemrosesan data.
- Reasoning dan pengambilan keputusan dilakukan oleh ChatGPT.
- Eksekusi fungsi deterministik dilakukan oleh backend.
- Arsitektur harus modular dan dapat dikembangkan.

# 4. Struktur dan Komponen AI Agent

| Komponen | Tanggung Jawab |
|---|---|
| Agent Instructions | Menentukan identitas, peran, dan aturan agent |
| Input Understanding | Memahami instruksi pengguna |
| Reasoning | Menganalisis kebutuhan dan menentukan tindakan |
| Planning | Menyusun langkah penyelesaian |
| Tool Selection | Memilih tools yang sesuai |
| Tool Execution | Menjalankan tools melalui MCP |
| Orchestration | Mengatur urutan dan koordinasi pekerjaan |
| State Management | Mempertahankan status dan progres tugas |
| Context Management | Mengelola informasi yang diperlukan |
| Guardrails | Membatasi tindakan yang tidak diizinkan |
| Error Handling | Menangani kegagalan dan pemulihan |
| Output Generation | Menyampaikan hasil kepada pengguna |

# 5. Mekanisme Kerja AI Agent

AI Agent menggunakan siklus kerja berikut:

### 5.1. Receive Input

Menerima instruksi pengguna melalui percakapan ChatGPT.

### 5.2. Understand Request

Mengidentifikasi:

- Tujuan pengguna.
- Kebutuhan pekerjaan.
- Parameter yang diperlukan.
- Batasan pekerjaan.
- Hasil yang diharapkan.

### 5.3. Analyze & Plan

Melakukan analisis dan menyusun rencana kerja.

### 5.4. Select Tools

Menentukan MCP Tools yang diperlukan berdasarkan tujuan pekerjaan.

### 5.5. Execute

Menjalankan tools melalui Custom MCP Server.

### 5.6. Evaluate Result

Menganalisis hasil eksekusi dan memeriksa kesesuaiannya dengan tujuan.

### 5.7. Continue or Recover

Jika pekerjaan belum selesai:

- Melanjutkan ke langkah berikutnya.
- Memperbaiki parameter jika diperlukan.
- Mengulangi operasi sesuai kebijakan retry.
- Menangani kesalahan.
- Meminta konfirmasi pengguna jika diperlukan.

### 5.8. Deliver Result

Menyampaikan hasil akhir kepada pengguna.

Siklus tersebut dapat berulang sampai pekerjaan selesai atau membutuhkan keputusan pengguna.

# 6. Konsep Pembagian Agent

Sistem dirancang agar mendukung pembagian tanggung jawab berdasarkan spesialisasi.

Contoh struktur konseptual:

```text
                 ORCHESTRATOR
                      │
          ┌───────────┼───────────┐
          │           │           │
          ▼           ▼           ▼
      RESEARCH       DATA      EXECUTION
       AGENT         AGENT       AGENT
          │           │           │
          └───────────┼───────────┘
                      │
                      ▼
                  REVIEW
                   AGENT
                      │
                      ▼
                 FINAL RESULT
```

### 6.1. Orchestrator Agent

Bertanggung jawab untuk:

- Memahami tujuan keseluruhan.
- Membagi pekerjaan.
- Menentukan urutan pekerjaan.
- Menentukan spesialisasi yang dibutuhkan.
- Mengelola hasil pekerjaan.
- Memeriksa penyelesaian tugas.

### 6.2. Research Agent

Bertanggung jawab untuk:

- Mengumpulkan informasi.
- Melakukan riset.
- Menganalisis informasi.
- Menyiapkan data untuk tahap berikutnya.

### 6.3. Data Agent

Bertanggung jawab untuk:

- Membaca data Supabase.
- Mengolah data.
- Memvalidasi data.
- Menyimpan hasil sesuai instruksi.

### 6.4. Execution Agent

Bertanggung jawab untuk:

- Menjalankan MCP Tools.
- Melaksanakan workflow.
- Memproses permintaan backend.
- Mengembalikan hasil eksekusi.

### 6.5. Review Agent

Bertanggung jawab untuk:

- Memeriksa hasil pekerjaan.
- Memvalidasi output.
- Mengidentifikasi kesalahan.
- Memberikan rekomendasi perbaikan.

**Catatan:** Pembagian ini merupakan spesialisasi konseptual. Tidak mewajibkan setiap spesialis memiliki model AI atau runtime terpisah.

# 7. Orchestration dan Koordinasi

Orchestration mengatur hubungan dan urutan pekerjaan antarkomponen.

Sistem perlu mendukung konsep berikut:

### 7.1. Sequential Workflow

Pekerjaan dijalankan secara berurutan.

Contoh:

```text
Input
  ↓
Analysis
  ↓
Planning
  ↓
Execution
  ↓
Review
  ↓
Output
```

### 7.2. Parallel Workflow

Pekerjaan yang tidak saling bergantung dapat dirancang untuk diproses secara paralel melalui backend.

### 7.3. Conditional Workflow

Langkah berikutnya ditentukan berdasarkan kondisi atau hasil sebelumnya.

### 7.4. Handoff

Penyerahan tanggung jawab atau hasil pekerjaan kepada spesialis lain.

### 7.5. Retry

Mengulangi operasi yang gagal dengan batas percobaan tertentu.

# 8. State dan Context Management

Sistem harus membedakan:

| Jenis | Fungsi |
|---|---|
| Context | Informasi yang diperlukan untuk memahami pekerjaan |
| State | Status dan progres pekerjaan |

### 8.1. Contoh Struktur State

```json
{
  "task_id": "task_001",
  "status": "in_progress",
  "current_step": "generate_image",
  "completed_steps": [
    "understand_request",
    "select_product",
    "prepare_prompt"
  ],
  "pending_steps": [
    "generate_image",
    "upload_image",
    "save_public_url"
  ],
  "error": null
}
```

### 8.2. Ketentuan State

- Setiap pekerjaan memiliki task_id.
- Status pekerjaan harus dapat diperiksa.
- Progres pekerjaan harus dapat disimpan.
- Hasil eksekusi harus dapat diambil kembali.
- State harus dapat digunakan untuk pemulihan pekerjaan.
- Data penting tidak boleh hanya bergantung pada konteks percakapan.

### 8.3. Status Pekerjaan

- pending
- in_progress
- completed
- failed
- waiting_for_user

# 9. Guardrails dan Keamanan

Ketentuan keamanan:

1. Agent hanya menggunakan tools yang diizinkan.
2. Setiap tool memiliki deskripsi dan parameter yang jelas.
3. Input divalidasi sebelum eksekusi.
4. Operasi berisiko membutuhkan persetujuan sesuai kebijakan.
5. Backend memvalidasi setiap operasi penting.
6. Tidak menganggap operasi berhasil sebelum menerima hasil keberhasilan.
7. Kredensial Supabase tidak boleh diekspos kepada pengguna.
8. Akses database harus mengikuti prinsip least privilege.
9. Operasi sensitif harus memiliki logging.
10. Penanganan error tidak boleh menghilangkan data penting.

# 10. Logging dan Evaluasi

Sistem perlu menyediakan pencatatan:

- Instruksi awal.
- Rencana pekerjaan.
- Tools yang dipanggil.
- Parameter yang dikirim.
- Hasil eksekusi.
- Status setiap langkah.
- Error dan percobaan ulang.
- Hasil akhir.

Tujuannya:

- Mempermudah debugging.
- Melacak proses eksekusi.
- Memeriksa kegagalan.
- Mengukur kualitas hasil.
- Meningkatkan keandalan workflow.

# 11. Batasan Implementasi (Non-goals)

Hal-hal yang tidak termasuk dalam proyek:

- Tidak menggunakan OpenAI Agents API.
- Tidak menggunakan OpenAI Agents SDK.
- Tidak menggunakan Responses API sebagai runtime agent.
- Tidak membuat model AI sendiri.
- Tidak memindahkan proses percakapan dari ChatGPT.
- Tidak mewajibkan setiap spesialis menggunakan model AI terpisah.
- Tidak membangun sistem reasoning terpisah di backend.

# 12. Prinsip Implementasi

| Bagian | Teknologi / Pendekatan |
|---|---|
| AI Model | ChatGPT Native |
| Reasoning | Model ChatGPT |
| Agent Instructions | Instruksi dan konfigurasi agent |
| Orchestration | Workflow yang diarahkan ChatGPT |
| Tool Integration | Custom MCP Server |
| Backend | Supabase |
| Database | Supabase PostgreSQL |
| File Storage | Supabase Storage |
| Backend Processing | Supabase Edge Functions |
| State Persistence | Supabase |
| Execution Logging | Supabase |

# 13. Tahapan Pengembangan

1. Menentukan arsitektur AI Agent.
2. Menentukan struktur dan tanggung jawab komponen.
3. Merancang mekanisme reasoning dan planning.
4. Merancang orchestration dan handoff.
5. Merancang state dan context management.
6. Menentukan struktur MCP Tools.
7. Merancang integrasi Supabase.
8. Menentukan guardrails dan error handling.
9. Menentukan logging dan evaluasi.
10. Melakukan pengujian keseluruhan workflow.

# 14. Ketentuan yang Harus Dipertahankan

1. ChatGPT Native tetap menjadi pusat kecerdasan sistem.
2. Agents digunakan sebagai referensi arsitektur dan pola kerja.
3. Custom MCP Server menjadi jembatan komunikasi dengan sistem eksternal.
4. Supabase menjadi backend.
5. Arsitektur memungkinkan pengembangan dari single-agent menjadi spesialisasi multi-agent.
6. Sistem modular agar tools dan kemampuan baru dapat ditambahkan.
7. Proses yang membutuhkan eksekusi deterministik harus ditangani backend.
8. State dan riwayat pekerjaan harus dapat dipertahankan di Supabase.

# 15. Catatan Kelayakan Teknis

Konsep multi-agent, parallel workflow, handoff, dan koordinasi merupakan target desain.

Kemampuan ChatGPT Native untuk menjalankan setiap pola tersebut harus divalidasi berdasarkan fitur MCP dan mekanisme interaksi yang tersedia.

Tidak boleh mengasumsikan bahwa kemampuan tersebut identik dengan runtime Agents SDK.

# 16. Pembagian Tanggung Jawab Sistem

### 16.1. ChatGPT Native

Bertanggung jawab untuk:

- Memahami instruksi.
- Melakukan reasoning.
- Menyusun rencana.
- Mengambil keputusan.
- Memilih tools.
- Mengevaluasi hasil.
- Menentukan langkah lanjutan.
- Menyampaikan hasil.

### 16.2. Custom MCP Server

Bertanggung jawab untuk:

- Menyediakan tools.
- Memvalidasi parameter.
- Menjalankan fungsi backend.
- Mengakses database.
- Mengakses storage.
- Menjalankan workflow deterministik.
- Mengembalikan hasil eksekusi.
- Menyediakan informasi status.

### 16.3. Supabase

Bertanggung jawab untuk:

- Menyimpan data.
- Menyimpan state.
- Menyimpan konfigurasi.
- Menyimpan riwayat eksekusi.
- Menjalankan Edge Functions.
- Menyediakan backend processing.
- Menyimpan hasil pekerjaan.

# 17. Batas Kemampuan ChatGPT Native

## 17.1. Prinsip Dasar

ChatGPT Native berfungsi sebagai pusat kecerdasan sistem.

ChatGPT dapat memahami instruksi, melakukan reasoning, menyusun rencana, memilih tools, memanggil MCP, mengevaluasi hasil, dan menentukan tindakan berikutnya.

Namun, ChatGPT Native bukan runtime AI Agent yang dapat diprogram secara bebas seperti Agents SDK.

Sistem harus menggunakan kemampuan bawaan ChatGPT dan tidak mengasumsikan adanya kontrol internal yang tidak disediakan platform.

## 17.2. Matriks Kemampuan

| Kemampuan | Status | Keterangan |
|---|---|---|
| Memahami instruksi | Didukung | Memahami permintaan pengguna |
| Reasoning | Didukung | Menganalisis dan mengambil keputusan |
| Planning | Didukung | Menyusun rencana kerja |
| Tool selection | Didukung | Memilih tools yang tersedia |
| Tool calling | Didukung | Memanggil MCP Tools sesuai akses |
| Evaluasi hasil | Didukung | Menganalisis hasil eksekusi |
| Multi-step execution | Didukung dengan batasan | Menjalankan beberapa tahapan |
| Sequential workflow | Dapat diterapkan | Menjalankan pekerjaan berurutan |
| Conditional workflow | Dapat diterapkan | Menentukan langkah berdasarkan hasil |
| Parallel execution | Tidak dijamin | Membutuhkan dukungan mekanisme eksekusi |
| Multi-agent orchestration | Tidak tersedia sebagai runtime kustom | Membutuhkan mekanisme tambahan |
| Agent handoff | Tidak tersedia sebagai mekanisme kustom yang dapat diprogram | Dapat dimodelkan melalui workflow |
| Persistent state | Memerlukan implementasi tambahan | Menggunakan Supabase |
| Background execution | Tidak dijamin | Membutuhkan backend asynchronous |
| Scheduled execution | Memerlukan mekanisme tambahan | Menggunakan scheduler |
| Retry mechanism | Terbatas | Retry deterministik harus ditangani backend |
| Logging | Memerlukan implementasi tambahan | Menggunakan Supabase |
| Guardrails | Sebagian didukung | Instruksi dan validasi backend |
| Kontrol model dan runtime | Terbatas | Tidak memiliki kontrol programatik penuh |

## 17.3. Tanggung Jawab ChatGPT Native

ChatGPT Native bertanggung jawab untuk:

1. Memahami instruksi pengguna.
2. Menentukan tujuan pekerjaan.
3. Melakukan reasoning.
4. Menyusun rencana.
5. Menentukan urutan pekerjaan.
6. Memilih MCP Tools.
7. Memproses hasil dari MCP.
8. Menentukan langkah lanjutan.
9. Mengevaluasi hasil.
10. Menyampaikan hasil akhir.

## 17.4. Pembatasan Multi-Agent

Sistem tidak boleh mengasumsikan bahwa ChatGPT Native dapat membuat, menjalankan, dan mengoordinasikan beberapa instance AI Agent secara mandiri seperti Agents SDK.

Konsep spesialisasi dapat diterapkan melalui:

- Satu model ChatGPT sebagai pusat reasoning.
- Instruksi spesialisasi untuk setiap jenis pekerjaan.
- Pembagian pekerjaan berdasarkan fungsi.
- MCP Tools sebagai kemampuan spesialis.
- Supabase sebagai penyimpanan status dan hasil.
- ChatGPT sebagai pengambil keputusan dan evaluator.

Pembagian tersebut merupakan spesialisasi workflow, bukan jaminan adanya beberapa model AI yang berjalan independen.

## 17.5. Pembatasan Eksekusi Workflow

ChatGPT Native dapat menentukan urutan pekerjaan dan memanggil tools secara bertahap.

Namun, sistem tidak boleh mengandalkan ChatGPT untuk:

- Menjalankan proses tanpa batas waktu.
- Mempertahankan eksekusi ketika sesi tidak lagi aktif.
- Menjalankan tugas terjadwal tanpa scheduler.
- Menjamin seluruh proses selesai dalam satu respons.
- Menjamin retry otomatis terprogram.
- Menjamin beberapa agent berjalan secara paralel.

Untuk kebutuhan tersebut, mekanisme backend harus disediakan melalui MCP Server dan Supabase.

## 17.6. Pembatasan State dan Context

Konteks percakapan tidak boleh dianggap sebagai database state yang dapat dikendalikan sepenuhnya oleh developer MCP.

Ketentuan:

- State pekerjaan disimpan di Supabase.
- Context penting dapat diambil kembali melalui MCP.
- Setiap pekerjaan memiliki task_id.
- Setiap tahapan memiliki status.
- Hasil eksekusi disimpan.
- ChatGPT dapat meminta status pekerjaan melalui MCP.

## 17.7. Prinsip Mengatasi Keterbatasan

1. ChatGPT Native menjadi pengambil keputusan.
2. MCP menjadi penghubung ChatGPT dengan backend.
3. Supabase menjadi penyimpan state dan data.
4. Workflow deterministik diprogram di backend.
5. Workflow yang membutuhkan reasoning diarahkan ChatGPT.
6. Proses yang berjalan lama menggunakan mekanisme asynchronous.
7. Hasil backend dikembalikan kepada ChatGPT untuk dievaluasi.
8. Setiap proses memiliki status dan mekanisme pemulihan.

## 17.8. Ketentuan Wajib

Arsitektur tidak boleh bergantung pada kemampuan internal ChatGPT yang tidak dapat dikendalikan melalui MCP.

Semua kemampuan yang membutuhkan:

- Eksekusi deterministik.
- Persistensi.
- Penjadwalan.
- Retry.
- Koordinasi proses.
- Background processing.

Harus memiliki implementasi yang jelas di backend.

**Tujuan akhir:** Memanfaatkan kecerdasan dan fleksibilitas ChatGPT Native tanpa menjadikan ChatGPT sebagai satu-satunya komponen yang bertanggung jawab atas seluruh proses eksekusi sistem.

---

# 18. Status Requirement

| Komponen | Status |
|---|---|
| Tujuan proyek | Dirancang |
| Referensi dokumentasi | Ditentukan |
| Arsitektur sistem | Dirancang |
| Struktur Agent | Dirancang |
| Mekanisme kerja | Dirancang |
| Pembagian spesialisasi | Dirancang |
| Orchestration | Dirancang |
| State & Context | Dirancang |
| Guardrails | Dirancang |
| Logging & Evaluasi | Dirancang |
| Integrasi MCP | Dirancang |
| Integrasi Supabase | Dirancang |
| Batas ChatGPT Native | Dirinci |
| Implementasi teknis | Belum dimulai |

# 19. Ketentuan Persetujuan

Dokumen ini menjadi acuan utama dalam pengembangan AI Agent berbasis ChatGPT Native, Custom MCP Server, dan Supabase.

Implementasi hanya dilakukan setelah requirement disetujui.

Setiap perubahan arsitektur, penambahan kemampuan, atau perubahan tanggung jawab komponen harus melalui proses diskusi, penyusunan requirement, dan konfirmasi.

**STATUS DOKUMEN: DRAFT FINAL v1.0 – MENUNGGU PERSETUJUAN PENGGUNA.**

---

## Referensi

1. https://developers.openai.com/api/docs/guides/agents
2. https://developers.openai.com/api/docs/guides/custom-mcp-server
