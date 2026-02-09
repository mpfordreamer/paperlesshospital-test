# 🏥 LLM Fine-Tuning for Indonesian Health Regulations

Fine-tuning a Large Language Model using **PEFT (Parameter-Efficient Fine-Tuning)** and **QLoRA** on Permenkes No. 10 Tahun 2024 (Indonesian Health Regulation).

## 📋 Overview

| Specification | Value |
|---------------|-------|
| **Base Model** | `unsloth/llama-3-8b-bnb-4bit` |
| **Technique** | QLoRA with 4-bit quantization |
| **Target Hardware** | Google Colab T4 GPU (16GB VRAM) |
| **Dataset** | 10+ instruction-tuning examples |

## 📁 Project Structure

```
Project/
├── data/raw/permenkes-no-10-tahun-2024.pdf   # Source PDF
├── outputs/                                    # Trained LoRA adapters
├── notebook.ipynb                              # Complete pipeline notebook
├── dataset.jsonl                               # Generated training data
├── requirements.txt                            # Dependencies
└── README.md
```

## 🚀 Quick Start

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Run on Google Colab
1. Upload `notebook.ipynb` to Google Colab
2. Upload `data/raw/permenkes-no-10-tahun-2024.pdf`
3. Select **T4 GPU** runtime: `Runtime → Change runtime type → T4 GPU`
4. Run all cells

### 3. Local Development
```bash
jupyter notebook notebook.ipynb
```

## 📓 Notebook Structure

| Phase | Description |
|-------|-------------|
| **Setup** | Install dependencies, import libraries |
| **Phase 1** | Data Preprocessing (PDF → JSONL) |
| **Phase 2** | Model Training (QLoRA fine-tuning) |
| **Phase 3** | Inference Demo (Q&A with citations) |

## ⚙️ Training Configuration

| Parameter | Value |
|-----------|-------|
| LoRA Rank (r) | 16 |
| LoRA Alpha | 32 |
| Batch Size | 2 |
| Gradient Accumulation | 4 |
| Learning Rate | 2e-4 |
| Max Steps | 60 |
| Quantization | 4-bit (BitsAndBytes) |

## 📊 Dataset Format

```json
{
  "instruction": "Jelaskan isi dari Pasal 1 dalam Permenkes No. 10 Tahun 2024.",
  "input": "Konteks: Pasal 1",
  "output": "Berdasarkan Pasal 1: ..."
}
```

## ✅ Requirements Met

- [x] PDF text extraction and cleaning
- [x] JSONL dataset generation (10+ examples)
- [x] T4 GPU memory optimization (4-bit quantization)
- [x] QLoRA fine-tuning with PEFT
- [x] Article citation in model outputs
- [x] Comprehensive documentation
