# 🏥 Fine-Tuning LLM untuk Regulasi Kesehatan Indonesia

Fine-tuning Large Language Model menggunakan **PEFT (Parameter-Efficient Fine-Tuning)** dan **QLoRA** pada Permenkes No. 10 Tahun 2024.

## 📋 Ringkasan

| Spesifikasi | Nilai |
|-------------|-------|
| **Model Dasar** | `unsloth/llama-3-8b-bnb-4bit` |
| **Teknik** | QLoRA dengan kuantisasi 4-bit |
| **Hardware** | Google Colab T4 GPU (16GB VRAM) |
| **Python** | 3.12.12 |
| **pip** | 24.1.2 |
| **Dataset** | 50 pasang Q&A instruksi |
| **Framework** | Unsloth + TRL + PEFT |

## 📁 Struktur Proyek

```
Project/
├── data/
│   ├── raw/permenkes-no-10-tahun-2024.pdf   # PDF sumber
│   └── dataset.jsonl                         # Dataset pelatihan
├── outputs/                                  # Adapter LoRA terlatih setelah training
├── notebook.ipynb                            # Notebook pipeline lengkap
├── requirements.txt                          # Dependensi
└── README.md
```

## 🚀 Cara Penggunaan

### Jalankan di Google Colab (Disarankan)
1. Buka `notebook.ipynb` di Google Colab
2. Pilih runtime **T4 GPU**: `Runtime → Change runtime type → T4 GPU`
3. Install dependensi dengan menjalankan cell pertama:
   ```python
   !pip install -r requirements.txt
   ```
4. Jalankan semua cell secara berurutan

### Jalankan di Lokal
1. Clone repository:
   ```bash
   git clone https://github.com/mpfordreamer/paperlesshospital-test.git
   cd paperlesshospital-test
   ```
2. Install dependensi dari `requirements.txt`:
   ```bash
   pip install -r requirements.txt
   ```
3. Jalankan notebook:
   ```bash
   jupyter notebook notebook.ipynb
   ```

> **Catatan:** Diperlukan GPU NVIDIA dengan CUDA untuk training lokal.

## 📓 Struktur Notebook

| Fase | Deskripsi |
|------|-----------|
| **Setup** | Install unsloth, import library |
| **Fase 1** | Preprocessing Data (PDF → JSONL) |
| **Fase 2** | Training Model (QLoRA fine-tuning) |
| **Fase 3** | Demo Inferensi & Evaluasi ROUGE |

## ⚙️ Konfigurasi Training

| Parameter | Nilai |
|-----------|-------|
| LoRA Rank (r) | 16 |
| LoRA Alpha | 32 |
| LoRA Dropout | 0 |
| Batch Size | 2 |
| Gradient Accumulation | 4 |
| Learning Rate | 2e-4 |
| Max Steps | 100 |
| Max Seq Length | 512 |
| Kuantisasi | 4-bit (BitsAndBytes) |
| Optimizer | paged_adamw_8bit |

## 📊 Hasil Training

| Metrik | Nilai |
|--------|-------|
| Training Steps | 100 |
| Waktu Training | ~13 menit |
| Final Loss | 0.0144 |
| Epochs | ~14 |

## 📈 Skor Evaluasi (ROUGE)

| Metrik | Skor |
|--------|------|
| ROUGE-1 (Unigram) | 0.2402 |
| ROUGE-2 (Bigram) | 0.1421 |
| ROUGE-L (LCS) | 0.2009 |

## 📚 Perbandingan Sebelum vs Sesudah Fine-Tuning

| Fitur | Model Dasar (Llama-3-8B) | Model Fine-Tuned (Ours) |
| :--- | :--- | :--- |
| **Pengetahuan** | Pengetahuan Umum (Tidak tahu Permenkes No. 10/2024) | Pengetahuan Spesifik (Paham Pasal 1-11) |
| **Gaya Output** | Verbose, Bahasa Inggris/Indonesia campur | Terstruktur, mengutip Pasal spesifik |
| **Halusinasi** | Tinggi (Mengarang pasal yang tidak ada) | Rendah (Grounding ke dokumen latih) |

> **Catatan:** Kode inferensi sebelum fine-tuning tidak disertakan karena model dasar tidak memiliki pengetahuan tentang regulasi spesifik tahun 2024 ini.

## 📝 Format Dataset

```json
{
  "instruction": "Jelaskan isi Pasal 1 dalam Permenkes No 10 Tahun 2024.",
  "input": "Konteks: Permenkes No. 10 Tahun 2024, Pasal 1",
  "output": "Jawaban: Berdasarkan regulasi, Pasal 1 mengatur..."
}
```

## ✅ Persyaratan Terpenuhi

- [x] Ekstraksi teks PDF dan pembersihan
- [x] Generasi dataset JSONL (50 contoh)
- [x] Optimasi memori T4 GPU (kuantisasi 4-bit)
- [x] Fine-tuning QLoRA dengan PEFT + Unsloth
- [x] Sitasi Pasal dalam output model
- [x] Evaluasi skor ROUGE
- [x] Dokumentasi lengkap

## 🔗 Referensi

- [Unsloth](https://github.com/unslothai/unsloth) - 2x faster LLM fine-tuning
- [TRL](https://github.com/huggingface/trl) - Transformer Reinforcement Learning
- [PEFT](https://github.com/huggingface/peft) - Parameter-Efficient Fine-Tuning

---

<p align="center">
  Made with ❤️ by <strong>Dewa Mahesta</strong>
</p>

<p align="center">
  © 2026. All rights reserved.
</p>
