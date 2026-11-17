Dokumentasi Referensi – Supabase Edge Functions & OpenAI Custom MCP Server
1. Supabase Edge Functions
Dokumentasi resmi: https://supabase.com/docs/guides/functions
Topik	URL
Dokumentasi utama	https://supabase.com/docs/guides/functions
Quickstart	https://supabase.com/docs/guides/functions/quickstart
Deploy Edge Functions	https://supabase.com/docs/guides/functions/deploy
Local Development	https://supabase.com/docs/guides/functions/local-development
Environment Variables & Secrets	https://supabase.com/docs/guides/functions/secrets
Database Access	https://supabase.com/docs/guides/functions/connect-to-postgres
Background Tasks	https://supabase.com/docs/guides/functions/background-tasks
HTTP Methods	https://supabase.com/docs/guides/functions/http-methods
Examples	https://supabase.com/docs/guides/functions/examples

2. OpenAI Custom MCP Server
Dokumentasi resmi:

https://developers.openai.com/api/docs/guides/custom-mcp-server

Referensi ini membahas integrasi Custom MCP Server dengan ekosistem OpenAI, termasuk bagaimana MCP Server menyediakan tools agar model AI dapat berinteraksi dengan sistem eksternal.
3. Referensi Tambahan
Sumber	URL
Supabase Documentation	https://supabase.com/docs
Supabase GitHub	https://github.com/supabase/supabase
OpenAI Developers	https://developers.openai.com/

4. Fokus Pembelajaran untuk Proyek
Komponen	Fokus
ChatGPT Native	Reasoning, memahami instruksi, perencanaan, dan pengambilan keputusan
Custom MCP Server	Menyediakan tools dan menghubungkan ChatGPT dengan sistem eksternal
Supabase Edge Functions	Menjalankan backend logic dan memproses permintaan
Supabase Database	Menyimpan dan mengelola data aplikasi
Supabase Storage	Menyimpan file dan gambar

Arsitektur integrasi yang menjadi acuan:
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


Catatan: Dokumentasi OpenAI Custom MCP Server digunakan sebagai referensi mekanisme integrasi MCP, bukan sebagai implementasi Agents API atau Agents SDK.
