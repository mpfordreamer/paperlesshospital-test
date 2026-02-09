# 🏥 LLM Fine-Tuning for Indonesian Health Regulations

Fine-tuning a Large Language Model using **PEFT (Parameter-Efficient Fine-Tuning)** and **QLoRA** on Permenkes No. 10 Tahun 2024 (Indonesian Health Regulation).

## 📋 Overview

| Specification | Value |
|---------------|-------|
| **Base Model** | `unsloth/llama-3-8b-bnb-4bit` |
| **Technique** | QLoRA with 4-bit quantization |
| **Target Hardware** | Google Colab T4 GPU (16GB VRAM) |
| **Dataset** | 58 instruction-tuning examples |
| **Framework** | Unsloth + TRL + PEFT |

## 📁 Project Structure

```
Project/
├── data/
│   ├── raw/permenkes-no-10-tahun-2024.pdf   # Source PDF
│   └── dataset.jsonl                         # Generated training data
├── outputs/
│   └── lora_adapter/                         # Trained LoRA adapters
├── notebook.ipynb                            # Complete pipeline notebook
├── requirements.txt                          # Dependencies
└── README.md
```

## 🚀 Quick Start

### 1. Run on Google Colab (Recommended)
1. Open `notebook.ipynb` in Google Colab
2. Select **T4 GPU** runtime: `Runtime → Change runtime type → T4 GPU`
3. Run all cells sequentially

### 2. Install Dependencies (Local)
```bash
pip install unsloth rouge_score pdfplumber
```

## 📓 Notebook Structure

| Phase | Description |
|-------|-------------|
| **Setup** | Install unsloth, import libraries |
| **Phase 1** | Data Preprocessing (PDF → JSONL) |
| **Phase 2** | Model Training (QLoRA fine-tuning) |
| **Phase 3** | Inference Demo & ROUGE Evaluation |

## ⚙️ Training Configuration

| Parameter | Value |
|-----------|-------|
| LoRA Rank (r) | 16 |
| LoRA Alpha | 32 |
| LoRA Dropout | 0 |
| Batch Size | 2 |
| Gradient Accumulation | 4 |
| Learning Rate | 2e-4 |
| Max Steps | 200 |
| Max Seq Length | 512 |
| Quantization | 4-bit (BitsAndBytes) |
| Optimizer | paged_adamw_8bit |

## 📊 Dataset Format

```json
{
  "instruction": "Jelaskan isi Pasal 1 dalam Permenkes No 10 Tahun 2024.",
  "input": "Konteks: Permenkes No. 10 Tahun 2024, Pasal 1",
  "output": "Isi Pasal 1 ..."
}
```

## 📈 Evaluation Metrics

Model performance evaluated using ROUGE scores:
- **ROUGE-1** (Unigram overlap)
- **ROUGE-2** (Bigram overlap)
- **ROUGE-L** (Longest Common Subsequence)

## ✅ Requirements Met

- [x] PDF text extraction and cleaning
- [x] JSONL dataset generation (58 examples)
- [x] T4 GPU memory optimization (4-bit quantization)
- [x] QLoRA fine-tuning with PEFT + Unsloth
- [x] Article citation in model outputs
- [x] ROUGE score evaluation
- [x] Comprehensive documentation

## 🔗 References

- [Unsloth](https://github.com/unslothai/unsloth) - 2x faster LLM fine-tuning
- [TRL](https://github.com/huggingface/trl) - Transformer Reinforcement Learning
- [PEFT](https://github.com/huggingface/peft) - Parameter-Efficient Fine-Tuning
